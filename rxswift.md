## RxSwift

### 1. Reactive Programming이 무엇인지 설명하시오.

-

### 2. RxSwift를 왜 사용하는지 설명하시오.
### 3. RxSwift의 단점을 설명하시오.
### 4. Subject의 종류와 차이점에 대해 설명하시오.

- PublishSubject, BehaviorSubject, ReplaySubject 가 있습니다.
- PublishSubject는 구독이 시작된 이후에 방출된 이벤트를 구독자에게 전달합니다.
- BehaviorSubject는 구독이 시작되기 전 방출되었던 가장 최근 값을 새로운 구독자에게 방출합니다. 첫 구독자라면 지정된 기본값을 방출합니다.
- ReplaySubject는 버퍼크기를 정해두고 새로운 구독이 시작되면 버퍼 크기만큼의 최근에 방출되었던 값을 모아두었다가 새로운 구독자에게 방출합니다.

</br>
