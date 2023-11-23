### Jest메소드 정리
Jest에서 사용되는 다른 주요 메소드들 중에는 다음과 같은 것들이 있습니다. <br>
- mockReturnValue: 함수가 호출될 때 항상 동일한 값을 반환하도록 지정합니다.
- mockResolvedValueOnce: 여러 번 호출되는 함수 중에서 첫 번째 호출에 대해서만 특정 값을 반환하도록 지정합니다.
- mockRejectedValue: Promise를 반환하는 함수의 reject 상황을 모킹할 때 사용합니다.
- mockImplementation: 함수가 호출될 때 사용자가 정의한 구현을 실행하도록 지정합니다.


### 테스트 명령어
pnpm test ~~.service 이러면 spec달린거 실행해주는듯
