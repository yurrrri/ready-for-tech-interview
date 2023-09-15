## RxSwift

### 1. Reactive Programming이 무엇인지 설명하시오.

- 비동기적 데이터 흐름과 전달에 관한 프로그래밍 패러다임

### 2. RxSwift를 왜 사용하는지 설명하시오.

- 콜백함수를 통해 비동기 프로그래밍을 하였을 때 콜백에 따른 처리가 많아진다면 코드가 지저분해지는데, 코드의 구독성을 높이고 일관된 코드로 비동기 프로그래밍을 할 수 있도록 도와주기에 사용함
- 또한 operator가 다양하여 상황에 따른 비동기 프로그래밍을 간편하게 구현할 수 있음

### 3. RxSwift의 단점을 설명하시오.

- 클로저의 사용이 많아서 순환 참조 이슈가 있기 때문에 이를 신경써야함

### 4. Subject의 종류와 차이점에 대해 설명하시오.

- PublishSubject, BehaviorSubject, AsyncSubject, ReplaySubject 가 있습니다.
- PublishSubject는 구독이 시작된 이후에 방출된 이벤트를 구독자에게 전달합니다.
- BehaviorSubject는 구독이 시작되기 전 일단 기본값을 가지고 있으며, 이후 구독한 객체에게는 가장 최근의 데이터와 그 이후의 데이터를 전달합니다.
- AsyncSubject는 complete 되는 시점에 마지막 데이터만 구독 객체에게 전달합니다.
- ReplaySubject는 버퍼크기를 정해두고 새로운 구독이 시작되면 버퍼 크기만큼의 최근에 방출되었던 값을 모아두었다가 새로운 구독자에게 방출합니다.

### RxSwift에서 Hot Observable과 Cold Observable의 차이를 설명하시오.
### Subject와 Driver의 차이를 설명하시오.
### Single, Completable, Maybe의 차이점에 대해 설명하고, 언제 적용하면 좋을지 설명하시오.
### RxSwift는 왜 MVC가 아닌 MVVM과 잘 어울릴까요?

- RxSwift의 핵심은 로직의 변화를 관찰하여 변화 내용을 바로 UI에 바인딩함에 있기 때문에, ViewModel이 Model을 변화시킬 때 뷰가 이를 반영하는 로직에 잘 어울리게 됩니다.

### 데이터 바인딩에 대해 아는만큼 설명해달라
### 데이터의 양방향 VS 단방향 소통
