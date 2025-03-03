# Existing Constructions Analysis
## Parameter 정리 
- **com**: commitment size를 의미함. SHA-256을 이용한 경우 256, KZG10을 이용한 경우 spec에 맞는 사이즈를 입력함
- **encoding size**: 아래 수식을 따름

$$
|\text{Encode}| = \text{(코드워드의 길이) } \times \text{ (오프닝 오버헤드 } + \text{ 코드 심볼 크기)}
$$
- **Comm.p.q**: 크게 *쿼리 요청(client upload)* 과 *응답 크기(client download)* 로 나뉘지만, dominant 한 값은 client download임 (쿼리 요청은 단순히 bit indexing 정도이기 때문)
$$
|Comm.p.q.| = \log_2 \text{(코드워드의 길이) } + \text{ 오프닝 오버헤드 } + \text{ 코드 심볼 크기}
$$
- **Reception**: DAS Scheme에 사용된 `Code`에 이론적으로 정의된 코드 복원을 위해 필요한 샘플의 수
- **Samples**: Reception 값과 *generalized coupon collector* 알고리즘을 활용하여 계산한 실제로 필요한 샘플의 개수
- **Comm Total**: 통신의 전체 비용, 근데 samples는 $8,000,000$ 이상이 아닌 다음에야 MB 단위로 환산했을 때 소수가 되어버려서 결국 dominant 한 $Comm.p.q.$ 크기가 중요함
$$
|Comm. Total| = |Comm. p. q.| \; + \; |Samples|
$$
## 구조별 분석
- `datasize` 가 128MB 일 때
![[Pasted image 20250226104022.png]]

- `Naive`: code를 사용하지 않고 그냥 데이터 그 자체를 사용하는 방식임. 이름 그대로 naive한 구조임.
	- com: SHA-256으로 커밋함
	- Encoding: 모든 데이터를 하나의 심볼로 간주함. Code가 아니라 그냥 데이터 그 자체를 사용한다고 보면 됨
	- Comm.p.q.: 전체 데이터를 나타내는 하나의 심볼만 통신으로 다운로드 하면 되므로 128,000 KB (=128MB) 를 다운받음, 더불어 indexing이나 opening_overhead도 존재하지 않음. 딱 128MB 만 cost로 계산됨
	- Reception: 코드 전체를 한 번만 받으면 복원이 되므로 $1$ 임
	- Sapmles: Reception과 마찬가지로 코드 전체를 한 번만 받으면 되므로 $1$임
	- Comm.total: comm.p.q 값과 마찬가지인 128MB
---
- `Merlke`: 데이터는 `naive`와 동일하게 별도의 code를 사용하지 않지만, commitment로 hash-based인 merkle tree를 사용함. 따라서, opening_overhead가 발생하고 samples에도 영향을 줌. 구체적으로, chunksize를 $1024$ (1kb)로 정하여 128,000 개의 leaf를 가진 merkle tree 구조로 DAS Scheme을 구현했다고 보면 됨
	- com: SHA-256을 사용하므로 여전히 크기는 256bit 수준임
	- encoding: "오프닝 오버헤드"가 발생함. 여기서 오프닝 오버헤드란, `merkle proof` 를 말한다고 이해하면 됨. 즉, 각 심볼(merkle tree의 leaf)에 대한 `merkle proof`의 크기는 $\log_2(\text{leaf 개수}) \times 256(hash \;\; size)$가 됨. 참고로 leaf 개수는 100,000개 인데 `k = math.ceil(datasize / chunksize)` 로 계산되고 수식으로 나타내면 $\lceil \big( \frac{128,000,000}{1024} \big) \rceil$ 이기 때문임.
	- Comm.p.q.: 쿼리 한 번당 오버헤드는 엄청나게 줄어듦. 왜냐하면 128,000,000 bit 였던 코드 심볼의 크기를 1024 bits로 줄이고, 코드워드 길이가 1에서 100,000이 되었지만, $\log_2$ 로 크기가 줄어들기 때문임... (정의에 따라 줄어든다고 보면 됨). "오프닝 오버헤드" 도 $\log_2(100,000) \times 256 = 4343.240 \cdots$ 이기 때문에 크지 않음
	- Reception: `Naive` 때와 마찬가지로 code를 사용하지 않기 때문에 100,000개의 데이터를 **모두** 다운로드 받아야지만 전체 데이터를 복원할 수 있습니다.
	- Samples: coupon collector 이론을 기반으로 값을 계산합니다. 식은 아래와 같습니다. 코드에서는 $\lambda$ 값을 40으로 잡고 있습니다.
$$
s = \lceil \frac{n}{\log_2 e} \times (log_2 n + \lambda)\rceil
$$
	- Comm.total: 쿼리 한 번 당 드는 비용은 줄어들었지만, Samples 수가 엄청나게 커지면서 결국 전체적인 통신 비용 전체는 증가한 것으로 해석할 수 있습니다.
---
- `RS`: $(n, k)$ Reed-Solomon Code 를 이용하고, KZG10 Polynomial commitment scheme을 이용합니다. 코드에서는 `makeKZGScheme` 이라는 이름으로 구현되어 있으며, $n = k \times 4$ 로 설정되어 있습니다.
	- com: `BLS_GE_SIZE` 값으로 설정됩니다. KZG10의 commitment 구현을 따르는 것을 보입니다.
	- encoding: 인코딩 공식을 다시 적어보면 아래와 같습니다. 코드워드의 길이는 data size크기인 128MB를 KZG10 에서 사용하는 `BLS_FE_SIZE`로 나눈 값입니다. 이는 $2,666,667$ 로 계산됩니다. `BLS_FE_SIZE` 가 코드 심볼의 크기가 되는데 이는 $384$ 입니다. 오프닝 오버헤드는 `BLS_GE_SIZE` 값으로 설정됩니다. 따라서, k * (BLS_GE_SIZE + BLS_FE_SIZE) 입니다. k * BLS_FE_SIZE 는 128MB 이고, k * BLS_GE_SIZE = 7 * 128MB 입니다.
$$
|\text{Encode}| = \text{(코드워드의 길이) } \times \text{ (오프닝 오버헤드 } + \text{ 코드 심볼 크기)}
$$
		