# iOS & Swift & CS

## 📚 운영체제, Swift Concurrency, GCD, 동기/비동기 등
## [운영체제 CS](https://github.com/yurrrri/ready-for-tech-interview/blob/main/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C.md)

### 동시성 프로그래밍에서 동기(Synchronous)와 비동기(Asynchronous)의 차이점은 무엇인가요?

- 동기는 요청한 작업이 끝날 때까지 기다렸다가 끝나면 다음 작업을 실행하는 것이고, 비동기는 기다리지 않고 다음 작업을 실행하는 점에서 차이가 있습니다.
- 네트워크 작업 등과 같이 시간이 오래걸리는 작업을 동기처리하게 될 경우, UI를 그리기 전까지 기다리므로 사용자 입장에서 사용성이 좋지 않지만 비동기 처리하게 될 경우, 네트워크 작업을 진행하며 UI를 처리하므로 사용성이 부드러집니다.

#### iOS에서 비동기 작업을 처리하는 방법은 무엇인가요?

- GCD와 async/await이 있습니다.
- GCD에서는 async 코드를 통해 비동기 작업을 수행하며, async/await은 비동기 흐름을 마치 동기처럼 읽기 쉬운 코드로 표현할 수 있는 방법입니다.

#### 동시성(Concurrency)과 병렬성(Parallelism)의 차이점을 설명해주세요.

- 병렬: 실제로 다중 스레드에서 작업을 동시에 실행하는것 (= 알바생 8명)
- 동시: 하나 혹은 다중 스레드에서 작업을 분산하면서, 매우 빠른 속도로 작업을 switching함으로써 일을 처리하여 동시에 일을 수행하는 것처럼 보이는 개념 (= 알바생 1명이 8개의 작업을 매우 빠르게 처리함)

#### iOS 기기는 여러 개의 CPU 코어를 가지고 있는데, 이것이 동시성/병렬성 구현과 어떤 관련이 있나요?

- 병렬은 멀티 코어 환경에서 여러 코어가 동시적으로 작동하게 함으로써 성능을 극대화할 수 있고,
- 동시성은 멀티 코어를 활용하여 여러 스레드에 작업을 적절하게 분배함으로써 1개의 코어보다 성능을 극대화할 수 있습니다.

### iOS 앱에서 Thread Sanitizer를 사용하여 동시성 문제를 탐지하고 해결하는 방법을 설명해주세요.

### 프로세스와 스레드의 차이점, 그리고 iOS에서의 프로세스와 스레드 관리 방법에 대해 설명해주세요.

- 프로세스는 메모리에 적재되어 현재 CPU에 의해 할당받아 실행되고 있는 프로그램을 의미합니다. 스레드는 한 프로세스 내에서 실행되는 동작의 단위를 의미합니다.
- iOS에서는 각 앱을 별도의 프로세스로 실행하며, GCD를 통해 스레드를 관리합니다.
- GCD란 개발자가 큐에 작업을 추가하면, 시스템이 알아서 적절한 스레드를 할당하여 일을 처리할 수 있도록 하는 기법입니다.

#### 하나의 앱 내에서 여러 프로세스를 사용하는 경우가 흔한가요? 아니라면 왜 스레드를 주로 사용할까요?

- 하나의 앱은 하나의 프로세스를 할당받아 실행되므로, 여러 프로세스를 사용하는 경우는 흔치 않습니다.
- 스레드는 하나의 프로세스 내에서 메모리를 공유하므로, 메모리 사용량이 적으며 통신 속도가 빠르기 때문에 멀티 스레드를 주로 사용합니다.

#### 멀티스레딩이 필요한 이유는 무엇인가요?

- 하나의 앱(프로세스)에서 여러 작업을 동시에 처리함으로써 성능을 향상시키고, 응답성 향상을 위해 멀티스레딩이 필요합니다.

#### Main 스레드에서 시간이 오래 걸리는 작업을 처리하면 어떤 문제가 발생할 수 있나요? 구체적인 예를 들어 설명해주세요.

- Main 스레드에서 시간이 오래 걸리는 작업을 진행하게 되면, 메인 스레드는 직렬 큐이기 떄문에 UI 관련한 작업은 메인 스레드에서만 처리할 수 있으므로 UI 응답성이 저하되어 사용자 경험에 안좋은 영향을 미칠 수 있습니다.
- 또한, Main 스레드가 장기간 응답하지 않으면 프로세스가 앱을 강제로 종료할 수 있으므로 이 또한 사용자 경험에 안좋은 영향을 끼칠 수 있습니다.

#### 메인 스레드에서 UI 업데이트를 해야 하는 이유는 무엇인가요?

- 메인 스레드에서만 UI 업데이트를 해야하는 이유는 Apple에서 의도적으로 Thread-safe 하지 않도록 설계한 것으로, Thread-safe하게 설계한다면 여러 스레드에서 UI 작업을 실행함으로써 사용자에게 일관되지 않은 UI를 보여줄 수 있게 됨
- 따라서 메인 스레드에서 UI 업데이트를 하도록 강제함으로써 여러 스레드에서 접근하는 데이터 충돌을 방지하고 UI 작업을 순차적으로 진행하여 일관된 사용자 경험을 제공하도록 되어있습니다.

#### 동시성 프로그래밍 시 발생할 수 있는 문제점은 무엇이며, 이를 해결하기 위한 방법에는 어떤 것들이 있나요?

- 동시성 프로그래밍 시 발생할 수 있는 문제점으로 Race Condition과 Deadlock이 있습니다.
- **Race Condition** 이란 여러 스레드에서 하나의 메모리에 접근하고자 할 때, 먼저 메모리를 사용하고자 하는 경쟁 상황을 의미합니다.
- **데드락(Deadlock)** 은 여러 스레드에서 하나의 메모리에 접근하고자 할 때, 해당 메모리를 다른 스레드에서 이미 점유하고 있어 해당 자원을 사용하고자 무한히 기다리는 상태를 의미합니다.
- 동기화 문제를 해결하기 위한 방식으로 대표적으로 mutex, semaphore가 있습니다.
- **Mutex**란, 공유 자원에 스레드 1개만이 접근할 수 있도록 하여 경쟁상황을 방지하는 기법입니다. 공유 자원을 점유하는 스레드가 lock을 걸면, 다른 스레드는 unlock이 될 때까지 기다려야합니다.
- **Semaphore**란, S개의 thread만이 공유 자원에 접근할 수 있도록 제어하는 동기화기법입니다.
우선 S라는 세마포 값을 가용한 자원의 수로 초기화를 한 다음, 자원에 접근 시 S— 연산, 방출 할 때는 S++ 연산을 수행하여 세마포 값을 증가시킵니다. 0인 경우에는 가용한 모든 자원이 사용중임을 의미하며, 이후 자원을 사용하고자 시도하는 프로세스는 세마포 값이 0보다 커지기 전까지 자원을 사용할 수 없습니다. 

#### 세마포어(Semaphore)와 뮤텍스(Mutex)의 차이점은 무엇인가요?

- mutex는 오직 1개의 프로세스/스레드만이 공유 자원에 접근할 수 있고, Semaphore는 세마포 변수 크기만큼만 공유자원에 접근할 수 있습니다.

### GCD(Grand Central Dispatch)의 주요 개념과 사용 방법을 설명해주세요.

- 멀티코어 프로세서 환경에서 동시성을 구현하기 위한 개념으로, 개발자가 큐에 작업을 할당하면 운영체제는 해당 큐에 있는 작업들을 알아서 다른 스레드로 분배함으로써 동시성 프로그래밍을 구현할 수 있도록 해줌

#### 글로벌 큐(Global Queue)와 메인 큐(Main Queue)는 어떻게 다르나요?

- 메인 큐는 시스템에서 기본적으로 존재하는 큐로, 직렬 큐기때문에 모든 작업이 순차적으로 실행됩니다.
- 글로벌 큐는 메인 스레드가 아닌 다른 스레드들에 작업을 분배하여 동시성 프로그래밍을 가능하게 하는 큐입니다.

#### GCD를 사용하지 않고 스레드를 직접 생성하고 관리할 때 발생할 수 있는 어려움은 무엇일까요?

- 개발자가 직접 스레드 풀이나 스케줄링을 관리해야하므로 코드가 복잡해짐
- 스레드를 적절하게 관리하지 못하면 데드락, 경쟁 상태 등의 문제가 발생할 위험이 큼

#### GCD의 DispatchQueue 종류와 사용 목적과 차이에 대해 설명해주세요.

- Serial Queued와 Concurrent Queue 2가지 종류로 나뉩니다.
- Serial Queue는 큐 내의 작업들을 순차적으로 작업하는 직렬 큐이며, 순차적으로 작업하는 것이 중요한 경우 사용합니다.
- Concurrent Queue는 큐 내의 작업들을 동시에 실행하기 위한 동시 큐로, 네트워크 요청이나 대규모 데이터 처리 등 성능 최적화가 필요한 경우 사용합니다.

### Swift의 async/await를 사용한 비동기 프로그래밍에 대해 설명해주세요.

- Swift의 async/await는 비동기 코드를 동기처럼 작성할 수 있게 해주는 문법입니다. 기존에는 클로저나 completion handler를 사용했지만, 가독성이 떨어지고 중첩이 많아지는 문제가 있어 해당 가돡성 문제를 해결하여 간결하게 비동기 처리를 도와주는 문법입니다.
- async 키워드는 함수가 비동기적으로 동작함을 나타내는 키워드이며, await는 비동기 함수를 호출하여 붙이는 키워드로 "결과를 기다린다"는 의미입니다.
- 가독성이 증진되어 코드 흐름이 명확해지고, 에러 처리도 do-catch로 간결하게 처리할 수 있어 유지보수가 쉬워집니다.

#### async/await 문법의 동작 원리와 사용 방법은 무엇인가요?

- async/await는 Swift Concurrency의 문법으로, 비동기 함수를 선언하고 호출할 때 사용됩니다.
- async 키워드는 해당 함수가 비동기적으로 실행되며, 호출 시 중간에 멈췄다가 다시 재개할 수도 있다는 의미를 내포하고 있습니다.
- await는 그 비동기 함수를 호출할 때 실행 결과를 기다린다는 의미로 붙이는 키워드입니다.

#### Task와 TaskGroup을 사용하여 비동기 작업을 관리하는 방법을 설명해주세요.

- Task는 비동기 작업의 단위 하나하나를 일컬으며, 작업의 우선순위를 정할 수 있습니다.
- TaskGroup은 여러 개의 하위 task를 그룹으로 묶어 관리할 수 있습니다.
여러 개의 하위 작업을 병렬로 실행하고 결과를 집계하며, 하위 작업의 결과는 완료 순서대로 반환됩니다.

#### async let을 활용한 병렬 처리를 설명해주세요.

- async let은 고정된 개수의 비동기 작업을 병렬로 실행하는 데 적합합니다.
- 작업이 정의된 즉시 실행되며, 결과를 사용할 때 await 키워드를 통해 기다립니다.

#### async let vs Taskgroup

- async let은
병렬로 실행할 작업 개수가 고정되어 있을 때, 
모든 결과를 기다려야 다음 단계를 진행할 수 있을 때 사용하는 것이 적합합니다.
또한 async let을 붙여 간편하게 병렬 처리를 하고자할 때에도 유용합니다.

- TaskGroup은
병렬로 실행할 작업의 개수를 미리 알 수 없고, 동적으로 변경될 수 있는 경우이거나
for 문을 통해 시작한 작업들의 결과를 순서대로 기다리므로, 먼저 처리된 작업을 가지고 먼저 사후 작업을 진행해야할 때 유용합니다.

## 📚 디자인 패턴, 아키텍처

### 싱글톤 패턴(Singleton Pattern)이란 무엇이며, 어떤 경우에 사용하나요?

- 싱글톤 패턴은 특정 클래스의 인스턴스를 하나만 생성하여 전역적으로 접근할 수 있도록 하는 디자인 패턴입니다.
- 예를 들어, 네트워크 매니저, UIScreen이나 UserDefaults 등과 같이 하나의 인스턴스만 있어도 되고 이를 여러 곳에서 공유해야 하는 상황에서 사용됩니다.​

#### 싱글톤 패턴의 장점과 단점을 설명해주세요.

- 장점: 동일한 인스턴스를 여러번 생성하지 않고 재사용 하므로 메모리를 효율적으로 관리할 수 있습니다.
- 단점: 싱글톤 패턴은 전역적으로 오로지 하나의 인스턴스를 생성하고 접근하는 형태이므로, 다른 목 객체를 주입할 수 없어 테스트가 어려워진다는 단점이 있습니다.

#### Swift에서 `let` 키워드를 사용하여 싱글톤 인스턴스를 선언하는 것이 왜 스레드 안전성을 보장하는 데 도움이 되나요?

- let을 사용하면 값을 바꿀 수 없는 상수로 고정되므로, 멀티 스레드 환경에서 여러 스레드가 해당 인스턴스를 변경하지 못하므로 안정성을 보장함

### iOS 앱 아키텍처 패턴 중 MVC, MVVM의 차이점은 무엇인가요?

- MVC는 Model, View, Controller로 이루어진 디자인 패턴으로 iOS에서는 View와 Controller의 결합성이 강하여 Controller가 View 로직을 다수 담당하게 됩니다.
- MVVM은 Model, View, ViewModel로 이루어진 디자인 패턴으로 View는 ViewModel의 데이터 바인딩에만 집중하게되고, ViewModel은 View 의존 없는 로직 구현이 가능해집니다.

#### MVC의 장점은 무엇인가요?

- 초기 구현이 단순하여 효율적입니다.

#### 각 아키텍처 패턴의 구성 요소와 책임을 설명해주세요.

- MVC
  - Model(화면과 관련없는 로직, 데이터) / View(UI 관련 코드) / Controller(모델의 정보를 어떻게 뷰에 표현할지 중재)
- MVVM
  - Model(화면과 관련없는 로직, 데이터) / ViewModel(View에 필요한 데이터 구성 등 로직 처리) / View (ViewModel에 바인딩 되어 UI 관련 로직 수행)
 
#### MVVM 패턴에서 Binding은 어떤 역할을 하나요?

- ViewModel의 값이 변경될 때 View가 자동으로 업데이트될 수 있도록 연결하는 역할을 합니다.
- Binding 덕분에 View는 ViewModel의 상태에만 집중하고, ViewModel은 UI에 대한 의존 없이 로직 구현 가능해집니다.

### MVVM-C(Coordinator) 아키텍처 패턴에 대해 설명해주세요.

- ViewModel에 여전히 종속되어 있던 화면 전환 책임을 Coordinator로 분리함으로써 ViewModel이 좀 더 데이터를 처리하는 로직에 집중할 수 있도록 돕습니다.

#### Coordinator의 역할과 구현 방법을 설명해주세요.

- Coordinator는 화면 이동(전환)을 전담하는 역할
- 각 화면에 대응하는 ViewController, ViewModel을 생성하고 연결

#### MVVM-C 패턴의 장단점과 적용 사례를 소개해주세요.

- 장점:
화면 전환 로직 분리로 ViewModel이 깔끔해짐
테스트 용이성, 유지보수성 향상
복잡한 네비게이션 흐름도 명확하게 표현 가능

- 단점:

초기 진입 장벽과 구현 복잡도가 있음

- 적용 사례:

딥링크, 조건 분기에 따라 화면 전환이 다양한 앱 등

## 📚 네트워크
## 📚 [네트워크 CS](https://github.com/yurrrri/ready-for-tech-interview/blob/main/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC.md)
### OSI 7계층에서, iOS 앱에서 서버와 통신할 때, 개발자가 주로 신경 쓰는 계층은 어디이며, 그 이유는 무엇인가요? (Application Layer 위주)
### iOS 앱에서 네트워크 통신을 하는 방법에는 어떤 것들이 있나요?

- Apple이 기본적으로 제공하는 URLSession, 혹은 서드파티인 Alamofire를 주로 많이 사용합니다.

### iOS에서 URLSession을 사용하여 네트워크 요청을 보내는 기본적인 과정은 무엇인가요?

- 네트워크 요청을 보내고자 하는 Url 객체를 생성하고, http 메서드나 헤더 등 추가 설정이 필요할 시 URLRequest 객체를 생성합니다.
- 그리고 네트워크 통신을 진행하는 주체인 URLSession을 생성하고,
- data, upload, download 등 구체적인 task를 생성한 다음
- resume을 통해 해당 작업을 수행합니다. 

#### URLSession 외에 iOS에서 네트워크 통신을 위해 사용할 수 있는 다른 방법(라이브러리)들은 무엇이 있나요? (예: Alamofire) 어떤 장단점이 있을까요?

- Alamofire는 반복적으로 수행하는 요청이나 JSON 파싱 등을 편리하게 처리할 수 있다는 장점이 있습니다.
- 단점으로는 서드파티 라이브러리이기 때문에 해당 라이브러리에서 문제가 발생했을 때 문제가 해결되려면 해당 라이브러리에서 문제가 해결되기 전까지 기다려야 한다는 단점이 있습니다.

#### API 요청 실패 시, 4xx 에러와 5xx 에러의 의미 차이는 무엇이며, 앱에서는 각각 어떻게 대응하는 것이 좋을까요? (예: 사용자에게 알림, 재시도 로직)

- 400번대 에러는 사용자가 서버에 잘못된 요청을 보냈다는 의미이고, 500번대 에러는 서버에서 사용자의 서버 요청을 처리할 수 없다는 의미라는 점에서 차이가 있습니다.
- 앱에서는 사용자에게 에러에 맞는 적절한 오류 메시지를 토스트나 팝업 등을 통해 보여줄 필요가 있는데,
- 401번은 로그인(인증)에 실패했다는 의미이므로 로그인화면으로 리다이렉트하여 다시 로그인 시도해달라고 사용자에게 안내할 것 같습니다.
- 나머지 코드의 경우 똑같은 서버 요청을 3번정도 재시도한다음에 그럼에도 오류가 발생할 경우에는 오류가 발생하여 고객센터에 문의해달라는 내용으로 팝업을 띄우도록 조치할 것 같습니다.

### 서버로부터 받은 JSON 데이터를 Swift 객체로 변환하는 과정(Decoding)에 대해 설명해주세요.

- 1) 먼저 JSON 데이터와 매칭되는 Swift 객체를 Decodable 프로토콜을 따르도록 준수하여 생성합니다.
- 2) JSONDecoder를 활용하여 해당 json 데이터를 앞서 생성한 Swift 객체로 Decoding을 진행합니다.

#### Swift의 `Codable` 프로토콜은 어떻게 동작하나요? `Encodable`과 `Decodable`은 무엇인가요?

- 개발자가 Encoding하거나 Decoding할 객체가 Codable 프로토콜을 준수하도록 설정한다면, 컴파일러가 내부 로직에서 자동으로 인코딩 혹은 디코딩 로직을 수행합니다.
- Encodable은 Swift 객체를 JSON 등의 외부 객체로 변환할 때 사용하는 프로토콜이며, Decodable은 외부 객체를 Swift 객체로 변환하고자 할 때 사용하는 프로토콜입니다.

#### JSON 데이터를 커스텀 객체로 디코딩하는 방법을 설명해주세요.

- JSON 데이터와 매칭되는, Decodable 프로토콜을 따르는 Swift 커스텀 객체를 생성한 후
- JSONDecoder를 활용하여 해당 객체로 디코딩을 수행합니다.

#### Codable 프로토콜을 채택한 타입에서 인코딩/디코딩 키를 커스터마이징하는 방법은 무엇인가요? (=JSON 키와 Swift 프로퍼티 이름이 다를 경우 어떻게 매핑하나요?)

- CodingKeys 열거형을 활용하여 JSON 키와 Swift 프로퍼티를 커스텀하여 매칭할 수 있습니다.
- CodingKeys 열거형이란, Codable 프로토콜을 따르는 객체 내에 존재할 수 있는 열거형이며 CodingKey 프로토콜을 준수합니다.

- 코드 예시

```swift
{
  "first_name": "John",
  "last_name": "Doe",
  "age": 30
}

struct Person: Codable {
    var firstName: String
    var lastName: String
    var age: Int

    enum CodingKeys: String, CodingKey {
        case firstName = "first_name"
        case lastName = "last_name"
        case age
    }
}
```

### 직렬화(Serialization)와 역직렬화(Deserialization)는 무인가요?

- 직렬화란 프로그램 내에서 사용하는 객체를 서버에 전송가능한 형태(JSON, XML 등)으로 변환하는 과정이며
- 역직렬화는 반대로 서버에 전송가능한 형태를 다시 프로그램 내에서 사용하는 객체로 변환하는 과정을 의미합니다.

#### JSON 형식이란 무엇이며, 왜 API 통신에서 자주 사용되나요?

- JSON 형식이란 데이터를 표현할 수 있는 경량화된 객체 중 하나로, 중괄호와 key-value 쌍 묶음으로 데이터와 그 계층을 표현합니다.
- API 통신에서 자주 사용되는 이유는, XML 형식에 비해 가독성이 좋으며 경량적인 데이터이기 때문에 효율적이고, 대부분의 프로그래멩서 JSON을 처리할 수 있는 라이브러리를 제공하므로 가공하기에도 간편합니다.

#### JSON외에 통신에서 자주 사용 되는 형식은 어떤것이 있나요?

- XML, Yaml 형식 등이 있는 것으로 알고 있습니다.

### iOS에서의 보안 통신 방법에 대해 설명해주세요.
#### HTTPS를 사용하면 통신 내용이 안전하다고 말하는데, 정확히 무엇으로부터 보호되는 건가요? (기밀성, 무결성, 인증 설명)
#### iOS 앱에서 HTTP 통신을 시도하면 기본적으로 어떤 제한이 있나요? 이 제한을 우회하려면 어떻게 해야 하나요? (ATS - App Transport Security)
### 소켓 통신에 대해 설명해주세요.
#### 소켓 프로그래밍을 직접 해야 하는 경우는 언제일까요? URLSession과 같은 고수준 API와 비교했을 때 장단점은 무엇인가요?
### iOS 앱에서 네트워크 요청 시 응답 캐싱(Response Caching)을 하는 방법은 무엇인가요?
#### URLCache는 어떤 역할을 하나요?
#### 응답 캐싱의 장단점은 무엇인가요?
#### 응답 캐싱을 커스터마이징하는 방법을 설명해주세요.

## 📚 딥링크, 유니버셜 링크, URL 스키마 
### iOS 앱에서 Deep Link와 Universal Link의 차이점은 무엇인가요

| 항목                | 딥링크 (URL Scheme)                             | 유니버설 링크 (Universal Link)                  |
|---------------------|--------------------------------------------------|--------------------------------------------------|
| 형식                | `myapp://path`                                   | `https://example.com/path`                       |
| 앱 미설치 시 동작   | 오류 발생 또는 무반응                            | 웹페이지로 자동 리디렉션                         |
| 보안성              | 낮음 (스킴 충돌 및 스푸핑 가능성)                | 높음 (도메인 소유 확인 필요)                     |
| 구현 난이도         | 낮음 (간단한 설정으로 가능)                     | 높음 (서버 설정 및 인증 필요)                   |

#### Deep Link를 구현하는 방법과 주의 사항을 설명해주세요.
#### Universal Link의 동작 원리와 설정 방법은 무엇인가요?
#### Deep Link와 Universal Link를 함께 사용하는 경우의 장점은 무엇인가요?
### URL 스킴(URL Scheme)을 이용한 앱 간 통신은 어떻게 이루어지나요?
#### URL 스킴을 사용할 때 보안적으로 고려해야 할 점은 무엇일까요?

## 📚 에러 처리
### Swift의 에러 처리 방법에 대해 설명해주세요.

- Error 프로토콜을 준수하는 error 열거형으로 발생할 수 있는 오류들을 정의합니다.
- 위에서 정의한 오류가 발생할 수 있는 함수에서 throws 키워드를 붙이고,
- 오류가 발생할 조건에서 throw error 를 통해 오류를 던집니다.
- 또한, do-catch 문에서 오류가 발생할 수 있는 함수를 호출 시 앞에 try를 붙여 호출하고, 에러 발생시의 동작은 catch 문에서 처리합니다.

#### 열거형(Enum)의 원시값(Raw Value)과 연관값(Associated Value)은 무엇인가요?

- 원시값은 정수나 문자열을 각 열거형 타입에 매칭시켜, 타입을 생성하거나 좀 더 쉽게 다루기 위해 사용하기 위한 목적으로 사용하는 값
- 연관값은 열거형에 보다 구체적이고 다양한 정보를 나타내고 싶을 때 사용하는 값

#### `throws`, `try`, `catch` 키워드의 사용 방법은 무엇인가요?

- throws는 해당 함수가 오류를 발생할 수 있음을 나타내는 키워드입니다.
- try는 throws가 선언된 오류가 발생할 수 있는 함수를 호출 시 사용합니다.
- catch 키워드는 do-catch 문에서 오류 발생시 에러를 포획하고 처리하는 데 사용합니다.

#### 옵셔널을 사용한 에러 처리와 `do-catch`를 사용하는 에러 처리의 차이는 무엇인가요?

- 옵셔널을 사용한 에러 처리의 경우, 오류가 발생했을 때 nil을 반환하는 방식입니다. 단, 오류의 세부 정보를 확인할 수 없으므로 단순 작업 성공 / 실패 여부를 따질 때는 간편하지만 오류를 세부적으로 처리할 필요가 있을 때 적합하지 않은 방법입니다.
- do-catch를 사용한 에러 처리의 경우, 사전에 정의한 에러의 세부 정보를 파악 후 오류에 따라 디테일하게 동작 처리가 가능합니다.

#### 에러를 전파하는 방법은 무엇인가요?

- 하위함수에서 상위함수에 에러를 전파하기 위해서는 상위 함수에서도 throws 키워드를 붙여 에러를 발생할 수 있는 함수임을 나타내도록 합니다.
- 상위함수를 호출할 때 마찬가지로 try를 붙이며, 필요시 do-catch 문을 통해 오류를 처리할 수 있습니다.

### Swift의 Result 타입과 에러 처리 방식에 대해 설명해주세요.

- Result 타입은 에러가 발생하는 경우, 오류를 따로 던지는게 아니라 return 타입으로 오류를 처리하는 방식을 의미합니다. result 타입에는 성공 여부를 나타내는 Bool 값과 실패 시의 오류 케이스를 함께 담아 리턴하는 방식입니다.
- 따라서 Result 타입을 활용하여 에러를 처리할 경우, switch 문을 통해 success/failure를 따지고 failure의 경우 연관값인 error를 활용하여 오류 처리를 진행하게 됩니다.

#### Result 타입을 사용하는 이유와 장점은 무엇인가요?

- result 타입을 반환하는 함수를 정의할 때 에러 타입을 명시적으로 선언할 수 있기에 해당 함수가 어떤 오류를 던질 지 가독성 좋게 확인이 가능하고, 타입캐스팅이 불필요하기에 편리합니다.

#### 에러 처리 시 do-catch 문과 Result 타입을 함께 사용하는 방법을 설명해주세요.

[예제코드]

```swift
enum FileError: Error {
    case fileNotFound
    case insufficientPermissions
}

func readFile(at path: String) -> Result<String, FileError> {
    guard path == "/valid/path" else {
        return .failure(.fileNotFound)
    }
    return .success("File content")
}

let result = readFile(at: "/invalid/path")

do {
    let content = try result.get()
    print("File content: \(content)")
} catch FileError.fileNotFound {
    print("The file was not found.")
} catch FileError.insufficientPermissions {
    print("You don't have permission to read the file.")
} catch {
    print("An unexpected error occurred: \(error)")
}
```
- Result 문을 통해 성공/실패 여부를 명확하게 알 수 있고, do-catch 문을 통해 명시적인 에러 처리가 가능하다는 장점을 취할 수 있습니다.

## 📚 클로저
### Swift의 클로저와 함수의 차이점은 무엇인가요?

- 클로저는 이름 없는 함수이고, 함수는 이름이 있는 함수입니다.
- 함수는 매개 변수나 변환 타입을 명시해야하지만, 클로저는 생략이 가능합니다.

#### 클로저가 일급 객체(First-Class Citizen)인 이유는 무엇인가요?

- 일급 객체란, 1) 변수에 할당할 수 있고 2) 함수의 인자로 넘길 수 있으며 3) 함수의 반환값으로 사용되는 타입을 의미하는데,
- 클로저는 해당 특성 모두 가지고 있으므로 일급 객체로 취급합니다.

#### 함수형 프로그래밍 패러다임에서 클로저가 어떻게 활용되나요?

- 고차함수를 통해 간결한 코드 작성이 가능해집니다.
- 비동기 작업이나 콜백 처리 시 유용하게 활용됩니다.

#### 클로저의 캡처(Capture) 기능은 무엇인가요?

- 외부의 변수 주소를 캡쳐하여 들고있음으로써 클로저 내부에서 해당 변수를 참조하거나 값을 수정하고, 상태값을 지속적으로 들고 있도록 하는 기능입니다.

#### 클로저의 캡처 리스트(Capture List) 기능은 무엇인가요?

- 값 타입의 경우 캡처 현상에서 외부의 변수 주소를 캡처하는 것과 달리, 값을 복사함으로써 외부 요인에 의한 값 변경을 방지하고
- 참조 타입의 경우 캡처 현상에서 외부의 변수 주소를 캡처하는 것과 달리, 참조 타입의 주소값을 직접 복사해서 사용함으로써 강한 참조를 통해 메모리에서 해제될 가능성을 방지하도록 합니다.
  (예를들어 캡처 현상에서는 변수 a = 5를 가리키고 있다면 변수 a의 주소를 가리키다가, 캡처리스트에서는 a의 참조를 직접 가리키게 됨)
  참조 타입은 캡처 리스트로서만 weak, unowned 키워드를 사용가능하기 때문에 강한 참조 사이클 문제를 해결하기 위해 사용하기도 합니다.

#### @escaping 클로저와 non-escaping 클로저의 차이점은 무엇인가요?

- escaping 클로저는 클로저의 기능 수행이 모두 끝나고 나서도 해당 클로저가 살아있도록 만들어주는 키워드입니다. 클로저가 함수 실행이 끝났음에도 오래 살아있도록 해야하는 경우 (변수 저장, GCD 등) 사용합니다.
- non-escaping 클로저는 이와 반대로 클로저의 기능 수행이 모두 끝난 다음에 클로저도 함께 사라집니다.

#### 트레일링 클로저(Trailing Closure) 문법은 어떤 경우에 유용한가요?

- 파라미터나 return문 등을 삭제함으로써 간결하게 코드를 작성하고자 할 때 유용합니다.
- 주로 고차함수나 비동기 처리함수 등에서 많이 사용합니다.

## 📚 메모리, ARC
### iOS에서의 메모리 구조와 관리 방식에 대해 자세히 설명해주세요

- iOS에서의 메모리 구조는 코드, 데이터, 힙, 스택 영역으로 이루어져있습니다.
- 코드 영역은 프로그램의 소스코드가 저장되어 있는 영역, 데이터 영역은 전역 변수/static 변수가 저장되어 있는 영역, 힙 영역은 동적 메모리 할당이 이루어지는 곳으로 참조 타입이 저장됩니다. 스택 영역은 값 타입이나 함수 호출 시의 복귀 주소나 return 값 등이 저장되는 영역입니다.

#### 함수 호출 시 스택 메모리는 어떻게 사용되나요? 재귀 함수 호출 시 스택 메모리 사용은 어떻게 될까요?

- 함수 호출 시, 함수의 지역변수나 매개 변수, 복귀할 리턴 주소가 스택 메모리에 적재되었다가 함수 종료 시 스택 영역에서 해당 메모리가 없어집니다.
- 재귀 함수 호출 시에도 함수 호출과 유사하나, 재귀 호출이 종료될 때 마지막에 호출된 순서부터 스택 영역에서 제거됩니다.

#### Swift의 값 타입(Value Type)과 참조 타입(Reference Type)은 각각 힙과 스택 중 어디에 주로 할당되나요? 그 이유는 무엇일까요?

- 값 타입은 스택에, 참조 타입은 힙 영역에 할당됩니다.
- 값 타입은 복사 시 독립적인 인스턴스로 복사되는 형태이므로, 함수가 종료될 때 오래 남아있는 힙 영역에 있을 필요 없이 바로 메모리에서 해제되기 때문에 스택 영역이 적합합니다.
- 참조 타입은 데이터를 공유하고, 생명 주기를 더 오래 관리해야할 수 있으므로 데이터를 오래 보관해야 하는 힙 영역이 적합합니다.

#### 값 타입과 참조 타입의 복사 방식(Copy-on-Write 포함) 차이에 대해 설명해주세요.

- 값 타입은 변수의 값을 복사하기 떄문에 복사본을 변경하여도 원본에 영향을 주지 않고, 참조 타입은 변수의 메모리 주소 값을 복사하여 같은 인스턴스를 공유하기 떄문에, 복사본 변경 시 원본에 영향을 주게 됩니다.
- 단 값 타입 중 배열과 같이 메모리를 많이 차지하는 값 타입의 경우, 메모리를 효율적으로 사용하기 위해 Copy-On-Write 방식을 사용하게 되는데, 해당 방식은 변수를 복사하여도 메모리 주소만 공유하다가 값의 내용 변경이 발생하는 경우에 값을 복사하는 형태를 의미합니다.

#### 스택 오버플로우(Stack Overflow)는 어떤 경우에 발생할 수 있나요?

- 스택 오버플로우는 프로그램이 스택의 영역을 넘어선 메모리를 사용하고자 할 때 발생합니다. 주로 지나치게 깊은 재귀나 무한 재귀 등의 상황에서, 스택에서 메모리가 해제 되지 않아 발생합니다.

### 메모리 관리 기법 중 iOS에서 사용되는 방식과 그 특징에 대해 설명해주세요.

- ARC를 통해 관리하며, 객체의 참조 횟수(RC)를 추적하여 필요하지 않은 객체를 자동으로 해제해주는 메모리 관리 시스템입니다.

### 자동 참조 카운팅(ARC)은 어떻게 동작하나요?

- 객체의 참조 카운트(Reference Count)를 추적하여 객체가 더 이상 사용되지 않을 때 메모리를 해제합니다. 이는 컴파일러가 런타임에서 참조 증가와 감소를 자동으로 처리합니다.

#### ARC가 자동으로 메모리를 관리해주는데, 개발자가 여전히 메모리 관리에 신경 써야 하는 이유는 무엇일까요?

- 강한 참조 사이클이 발생하게 되면, 개발자가 메모리 관리에 신경쓰지 않으면 참조 횟수가 0이 되지 않으므로 메모리에서 해제가 되지 않아, 메모리 누수가 발생할 수 있으므로 개발자가 이에 대해 신경쓸 필요가 있습니다.

#### 순환 참조(Retain Cycle)는 무엇이며, 어떻게 발생하고 해결할 수 있나요?

- 순환 참조란 객체가 서로 참조하는 과정에서, 소유하는 객체가 메모리에서 해제 되더라도 참조하는 객체는 계속 참조하고 있기 때문에, 메모리 누수의 상황이 발생하는 문제를 의미합니다.
- 해당 문제를 해결하기 위해 약한 참조나 비소유 참조를 적절하게 활용하여 참조 카운팅의 수를 늘리지 않게 함으로써 해결할 수 있습니다.

#### 메모리 관리에서 강한 참조(Strong Reference)와 약한 참조(Weak Reference)의 차이점은 무엇인가요?

- 강한 참조란 객체를 참조하는 기본적인 방식으로, 참조 카운트를 증가시켜 메모리에서 해제되지 않도록 보장합니다.
- 약한 참조란 객체를 소유하여도 참조 카운트를 증가시키지 않기 때문에, 객체가 해제되면 자동으로 nil이 설정됨으로써 순환 참조를 방지할 수 있또록 합니다.

#### 클로저에서 `[weak self]`와 `[unowned self]`의 차이는 무엇인가요?

- weak self는 소유하여 가리키는 객체의 RC를 증가하지 않도록 하는 방법 중 하나로, 참조하는 객체가 메모리에서 해제될 경우 ARC가 자동으로 nil을 할당합니다.
- unowned self는 소유하여 가리키는 객체의 RC를 증가하지 않도록 하는 방법 중 하나로, 참조하는 객체가 메모리에서 해제될 경우임에도 자동으로 nil을 할당하지 않는 대신 런타임 에러가 발생하므로 참조하는 객체가 소유자보다 오래 살아있음을 보장할 경우 사용합니다.

#### 강한 참조(Strong Reference), 약한 참조(Weak Reference), 미소유 참조(Unowned Reference)는 각각 언제 사용해야 하나요? 예를 들어 설명해주세요.

- 강한 참조는 RC를 증가시키는 기본 방식이므로 객체에 대한 소유권을 유지해야할 경우 사용하며, (메모리에서 해제 되지 않도록 방지)
- 약한 참조와 미소유 참조는 모두 RC를 증가시키지 않도록 하는 방식이나, 약한 참조는 가리키는 대상이 nil일 가능성이 있을때 유용하나 미소유 참조는 가리키는 대상이 항상 소유자보다 오래 살아있음을 보장할 때 사용하는 것이 적합합니다.

#### `deinit` 메서드는 언제 호출되며, 어떤 역할을 하나요?

- deinit은 인스턴스가 메모리에서 해제될 때, 자동으로 호출됩니다.
- 이 때 개발자가 메모리에서 해제될 때 추가적으로 정리해야하는 내용이 있을 때 개발자가 의도적으로 정의함으로써 정리 작업을 진행할 수 있습니다.

## 📚 값 타입, 참조 타입
### 값 타입(Value Type)과 참조 타입(Reference Type)의 차이점은 무엇인가요?

- 값 타입은 값이 복사되어 전달되고 (복사본의 변경이 원본에 영향을 주지 않음), 참조 타입은 메모리의 주소가 복사되어 전달되는 형태로 동작합니다.
- 참조 타입은 클래스, 클로저에 해당되며 Heap에 동적 할당되는 형태이기 때문에 ARC를 통해 메모리를 관리합니다.
- 값 타입은 클래스, 클로저가 아닌 대부분의 데이터 타입에 해당되며 Stack에서 실행되고 없어지기 때문에 메모리 관리를 신경쓰지 않아도 됩니다.

### 구조체(Struct)와 클래스(Class)의 사용 시기는 어떻게 구분하나요?

- 구조체는 실행 후 메모리에서 바로 사라지기 떄문에, 메모리 관리를 따로 하지 않고 가볍게 사용하고 싶을 경우나 값 자체를 복사하여 인스턴스를 새로 생성해야하는 경우, 상속이 필요없는 경우에 사용합니다.
- 클래스는 상속이 필요한 경우나 인스턴스의 공유가 필요한 경우에 사용합니다.

## 📚 OOP, POP
## 📚 [개발상식 CS](https://github.com/yurrrri/ready-for-tech-interview/blob/main/%EA%B8%B0%ED%83%80.md)
### 객체지향 프로그래밍(OOP)의 주요 개념에 대해 설명해주세요.

- 현실 세계를 '객체'로 모델링하여 프로그램을 설계 및 개발하는 프로그래밍 패러다임입니다.
- 캡슐화, 상속, 추상화, 다형성이라는 4대 특징이 있습니다.

#### 캡슐화(Encapsulation)와 정보 은닉(Information Hiding)의 차이점은 무엇인가요?

- 캡슐화는 데이터와 메서드를 하나로 묶어 객체를 형성한다는 의미이고,
- 정보 은닉은 객체 내부의 구현 사항을 외부로부터 숨기는 방식을 의미합니다.

#### 상속(Inheritance)의 장단점은 무엇인가요?

- 장점은 부모 클래스의 속성과 메소드를 자식 클래스에서 재사용하므로, 중복 코드를 줄이고 개발 시간을 단축할 수 있습니다.
- 단점은 자식 클래스는 부모 클래스의 모든 속성과 메소드를 물려 받으므로, 불필요한 내용까지 물려받는 비효율이 발생할 수 있으며 부모 클래스에서 내용 변경 시, 자식 클래스도 같이 변경되는 문제가 있습니다.
또한, 클래스에서만 상속 가능하다는 단점도 존재합니다.

#### 다형성(Polymorphism)을 활용하는 예시를 들어주세요.

- 메서드 오버라이딩: 자식 클래스가 부모 클래스의 메서드를 재정의하여 다른 동작을 구현하는 것
- 오버로딩: 한 가지 메소드가 다른 타입의 매개변수를 가지면서 각기 다른 동작을 실행하는 것

### 프로토콜 지향 프로그래밍(POP)이란 무엇이며, 어떤 장점이 있나요?

- 프로토콜 지향 프로그래밍이란, 프로토콜과 프로토콜 확장을 중심으로 코드를 설계하고 구현하는 패러다임을 의미합니다.
- 프로토콜 확장을 통해 기본 구현을 제공하여, 프로토콜을 따르는 모든 타입에서 공통 동작을 구현할 수 있으므로 코드 재사용성이 증가합니다.
- 기존 상속의 단점이었던 다중 상속이 가능하여, 더 유연한 설계를 지원합니다.
- 클래스에서만 가능했던 상속이 프로토콜 프로그래밍에서는 값 타입에서도 구현이 가능합니다.

#### 프로토콜 확장(Protocol Extension)을 사용하는 이유는 무엇인가요?

- 코드 중복을 제거하기 위한 목적이 큰데, 프로토콜을 준수하는 모든 클래스나 구조체에서 같은 동작을 할 경우에 모두 같은 내용을 구현하지 않아도, extension을 통해 기본값을 제공함으로써 코드 중복을 제거해준다는 이점이 있습니다.

### Swift에서 프로토콜(Protocol)이란 무엇이며, 어떻게 활용하나요?

- 클래스나 구조체가 특정 요구사항을 따르게 구현되도록 요구하는 청사진
- 프로토콜에서 속성이나 메서드를 정의할 경우, 이 프로토콜을 따르는 클래스나 구조체에서 해당 속성과 메서드를 반드시 구현해야합니다.

#### 프로토콜의 요구사항은 무엇인가요?

- 프로토콜에서 해당 프로토콜을 준수하는 클래스나 구조체는 반드시 구현하거나 준수해야하는 사항을 의미합니다.
- 프로퍼티 요구사항, 메서드 요구사항, 생성자 요구사항이 있습니다.

#### 다중 상속(Multiple Inheritance)이 불가능한 이유는 무엇인가요?

- 다중 상속은 여러 부모 클래스에서 동일한 이름의 메서드나 속성을 상속받을 경우, 어떤 부모의 구현을 사용할지 결정하기 어려운 문제가 발생할 수 있기 떄문입니다.

#### 프로토콜 준수(Conformance)를 통해 다형성을 구현하는 방법은 무엇인가요?

- 다형성이란 동일한 이름의 메소드나 속성이 상황에 따라 다른 동작을 수행할 수 있다는 점이므로, 프로토콜 채택 및 구현을 통해 프로토콜을 준수하는 타입마다 다른 동작을 수행할 수 있도록 할 수 있습니다.

## 📚 Delegate
### iOS에서 Delegate 패턴은 무엇이며, 어떤 상황에서 사용되나요?

- Delegate 패턴은 한 객체가 특정 작업을 다른 객체에 위임하도록 설계된 디자인 패턴입니다.
- 앞서 말씀드린것과 같이 특정 작업을 다른 객체가 하도록 위임해야할 경우거나, UIKit에서 대표적으로 UITableView나 UICollectionView에서 셀 선택 이벤트를 처리할 때 사용합니다.

#### Delegate 패턴과 Notification, KVO의 차이점은 무엇인가요?

- Delegate 패턴은 객체간 1:1 통신만 가능하지만, Notification은 1:N 통신을 하는 방식입니다. KVO는 1:N 관계에서 특정 프로퍼티의 변경점을 감지하기 위한 방식입니다.

#### 프로토콜을 활용한 Delegate 패턴 구현 방법을 설명해주세요.

- 1) 위임할 작업을 프로토콜 내 메소드를 통해 정의합니다.
```swift
protocol TaskDelegate: AnyObject {
    func taskDidComplete(data: String)
}
```

- 2) Delegate 프로퍼티를 선언하고, 작업 완료 시 delegate 메서드를 호출합니다.
```swift
class TaskManager {
    weak var delegate: TaskDelegate?

    func completeTask() {
        print("Task Completed")
        delegate?.taskDidComplete(data: "Task Data")
    }
}
```

- 3) 위임 받아 처리할 객체가 해당 프로토콜을 채택하고, delegate 메서드를 통해 작업을 구현합니다.
```swift
class ViewController: UIViewController, TaskDelegate {
    private let taskManager = TaskManager()

    override func viewDidLoad() {
        super.viewDidLoad()
        taskManager.delegate = self
        taskManager.completeTask()
    }

    func taskDidComplete(data: String) {
        print("Delegate received data: \(data)")
    }
}
```

#### 델리게이션 패턴에서 메모리 누수가 발생할 수 있는 경우와 해결 방법을 설명해주세요.

## 📚 자료구조
## 📚 [자료구조 CS](https://github.com/yurrrri/ready-for-tech-interview/blob/main/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%26%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%26%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md)
### 스택과 큐는 어떤 iOS 기능 구현에 사용될 수 있을까요? (예: 화면 네비게이션 스택, 작업 큐)

- 스택은 화면 네비게이션 스택에 사용됩니다. 네비게이션 바에서 화면 전환 시 화면 스택에 화면이 쌓이게되고(push), 뒤로가기를 누르면 가장 최근에 추가된 화면이 제거되는 방식(pop) 입니다.
- 큐는 DispatchQueue에서 사용됩니다. 해당 큐에 개발자가 작업을 보내면, 운영체제가 알아서 스레드에 작업을 분배하여 동시성 작업을 처리하게 됩니다.

### Swift의 `Dictionary`와 `Set`은 해시 테이블과 어떤 관련이 있을까요?

- 해시 테이블 기반: Dictionary의 키와 Set의 요소는 해시 테이블로 구현되어 검색 시 O(1) 시간 복잡도를 가집니다.

### iOS UI 구조(View Hierarchy)와 트리는 어떤 관련이 있을까요?
### Swift 표준 라이브러리의 `sort()` 메서드는 어떤 정렬 알고리즘을 사용할까요?

- IntroSort 알고리즘을 사용합니다. 기본적으로 퀵 정렬을 사용하다가, 재귀 깊이가 일정 수준 이상을 넘으면 힙 정렬로 전환하고, 작은 구간에서는 삽입 정렬을 적용합니다.
- Swift5 이후에는 modified timsort도 함께 적용되어 동작하는데, 이는 병합 정렬과 삽입 정렬을 결합한 알고리즘입니다.

### Swift의 `Array`는 값 타입인데, 이것이 성능과 메모리 사용에 어떤 영향을 미치나요? (Copy-on-Write 설명 포함)

- Swift의 Array는 값 타입이기 때문에 변수에 할당하거나 함수에 전달할 때 원칙적으로는 전체 데이터가 복사되어야 합니다. 하지만 배열의 원소의 갯수가 굉장히 많게되면 매번 복사가 일어나면 성능과 메모리 사용 측면에서 매우 비효율적일 수 있습니다.
- 이 문제를 해결하기 위해 Swift는 Copy-on-Write(COW) 방식을 사용합니다.
- COW란, 배열을 복사할 때 실제로는 내부 데이터를 바로 복사하지 않고, 여러 배열이 동일한 메모리(버퍼)를 참조하도록 합니다.
- 그러다가 배열 중 하나에서 변경(쓰기) 작업이 발생하면, 그 시점에 해당 배열만을 위한 복사본을 만들어 변경을 적용합니다.
- 즉, 읽기만 할 때는 메모리를 공유하고, 쓸 때만 진짜 복사가 일어나는 방식이기에 메모리 사용에 있어서 효율적입니다.

## 📚 기타 Swift 문법
### Swift에서 옵셔널(Optional)이란 무엇이며, 언제 사용해야 하나요?

- 옵셔널은 기본 타입에 값이 없을 수 있음(nil)을 포함하는 타입입니다.
- 값이 없을 수 있음을 나타냄으로써 사전에 해당 경우를 대처하여 오류를 방지하기 위해 사용합니다.

#### 옵셔널 바인딩과 강제 언래핑의 차이점은 무엇인가요?

- 강제 언래핑: 값이 무조건 있다는 것으로 확신하고 값을 강제로 꺼내는 방법으로, 변수 뒤에 ! 을 붙여서 값을 가져옵니다.
- 옵셔널 바인딩: if let, guard let 구문을 활용하여 변수에 옵셔널 타입을 할당함으로써 nil이 아닌지 확인한 후 값을 꺼내오는 방법입니다.

#### 옵셔널 체이닝의 동작 원리는 무엇이며, 어떻게 사용하나요?

- 옵셔널 타입 변수의 속성이나 메서드에 접근할 때, 변수에 ?.를 붙여 접근하는 방식입니다.
- 옵셔널 체이닝의 결과는 항상 옵셔널 타입이며, 체이닝 과정에서 하나라도 nil이라면 이어지는 식을 평가하지 않고 nil을 return합니다.

#### Swift에서 옵셔널(Optional)을 사용할 때 주의할 점은 무엇인가요?

- 옵셔널은 변수가 값이 없을 수 있음을 나타내는 타입이므로, nil인지 아닌지를 먼저 확인하고 안전하게 값을 꺼내야합니다.

#### 강제 언래핑(Force Unwrapping)을 사용하면 안 되는 이유는 무엇인가요?

- 옵셔널 타입을 강제로 값을 꺼내게 되면, nil일 경우 런타임 에러가 발생하므로 가급적 사용을 지양해야합니다.

## 접근 제어자
### Swift의 접근 제어자(Access Control Levels)에 대해 설명해주세요.

- 코드의 접근 범위를 정의할 수 있는 제어자를 의미합니다. 외부에서 확인하면 안되는 코드를 은닉함으로써 코드 보안성을 유지할 수 있고, 컴파일러가 해당 변수가 어느 범위까지 쓰는지를 인지하여 컴파일 시간이 줄어든다는 장점이 있습니다.

#### 접근 제어자를 사용하는 이유는 무엇인가요?

-  외부에서 확인하면 안되는 코드를 은닉함으로써 코드 보안성을 유지할 수 있고, 컴파일러가 해당 변수가 어느 범위까지 쓰는지를 인지하여 컴파일 시간이 줄어든다는 장점이 있습니다.

#### `open`과 `public`의 차이점은 무엇인가요?

- 모두 외부 모듈에서 접근 가능하다는 특징이 있지만, open은 상속이 가능하며 public은 상속이 불가능하다는 차이점이 있습니다.

#### `internal`, `fileprivate`, `private`의 사용 시기는 어떻게 결정하나요?

- internal은 기본 접근 제어자로, 같은 모듈 내에서만 접근해야할 때 사용하며
- fileprivate는 파일 내에서만 접근 가능하게 하기 위해 사용합니다.
- private는 해당 코드 스코프 내에서만 접근가능하게 하고싶을 때 사용합니다.

### Swift의 고차 함수(Higher-Order Functions)에 대해 설명해주세요.
#### `map`과 `flatMap`의 차이점은 무엇인가요?
#### `filter`, `reduce` 함수는 어떤 경우에 사용하나요?
#### `compactMap`은 어떤 역할을 하나요?

### Swift의 제네릭(Generic)에 대해 설명해주세요.

- Swift의 제네릭은 특정 타입에 종속되지 않고, 다양한 타입에서 동작할 수 있는 범용적인 코드를 작성할 수 있도록 하는 기능입니다.

#### 제네릭을 사용하는 이유는 무엇인가요?

- 로직은 동일하나 다양한 타입을 사용하는 코드에 대해 하나의 코드로 정의할 수 있어 코드 재사용성이 올라간다는 이점이 있기에 사용합니다.

#### 제네릭 타입 파라미터와 제약 조건을 설정하는 방법은 무엇인가요?

- <T>: 플레이스홀더로 타입 파라미터 설정

```swift
func swapValues<T>(_ a: inout T, _ b: inout T) {
    let temp = a
    a = b
    b = temp
}
```

- 제약 조건(Type Constraints): 특정 프로토콜을 따르거나 클래스를 상속하도록 제한할 수 있습니다.

```swift
func findIndex<T: Equatable>(of value: T, in array: [T]) -> Int? {
    return array.firstIndex(of: value)
}
```

### Swift의 문자열(String) 다루기와 관련된 주요 기능은 무엇이 있나요?
#### 서브스트링(Substring)과 문자열의 차이점은 무엇인가요?
#### 문자열 보간법(String Interpolation)을 사용하는 방법과 주의 사항을 설명해주세요.
#### 정규식(Regular Expression)을 사용하여 문자열을 다루는 방법을 설명해주세요.

## 📚 UIKit
### iOS 앱의 생명주기(App Life Cycle)에 대해 설명해주세요.
#### 앱의 각 상태(`Not Running`, `Inactive`, `Active`, `Background`, `Suspended`)에서 가능한 작업은 무엇인가요?

| 상태         | 설명                                                                 | 가능한 작업                                                                                   |
|--------------|----------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| Not Running  | 앱이 실행되지 않았거나, 시스템 또는 사용자가 종료한 상태.                  | 아무 작업도 수행되지 않음.                                                                   |
| Inactive     | 앱이 Foreground에 있지만 사용자 입력을 받지 않는 상태. (예: 전화 수신 시)   | UI 업데이트 가능. 제한된 작업 수행 가능.                                                      |
| Active       | 앱이 Foreground에 있으며 사용자 입력을 받고 있는 정상적인 상태.            | 사용자와 상호작용 가능. 모든 기능 실행 가능.                                                  |
| Background   | 앱이 Background로 전환되었지만 여전히 코드 실행이 가능한 상태.              | 제한된 시간 동안 작업 가능 (예: 데이터 저장, 네트워크 요청). 백그라운드 작업 모드 활성화 시 장기 작업 가능 (예: 오디오 재생, 위치 추적). |
| Suspended    | 앱이 Background에 있지만 코드 실행이 중단되고 메모리에만 유지된 상태. 시스템 리소스 부족 시 종료될 수 있음. | 작업 불가. 필요 시 시스템에 의해 다시 Active 또는 Background로 전환됨.                     |


#### 상태 변화에 따라 호출되는 `AppDelegate` 또는 `SceneDelegate` 메서드는 무엇인가요?


| 상태 변화             | AppDelegate 메서드                                  | SceneDelegate 메서드                         |
|----------------------|-----------------------------------------------------|----------------------------------------------|
| 앱 시작              | `application(_:didFinishLaunchingWithOptions:)`     | `scene(_:willConnectTo:options:)`            |
| Foreground 진입      | `applicationWillEnterForeground(_:)`                | `sceneWillEnterForeground(_:)`               |
| Active 상태 진입     | `applicationDidBecomeActive(_:)`                    | `sceneDidBecomeActive(_:)`                   |
| Inactive 상태로 전환 | `applicationWillResignActive(_:)`                   | `sceneWillResignActive(_:)`                  |
| Background 진입      | `applicationDidEnterBackground(_:)`                | `sceneDidEnterBackground(_:)`                |
| 앱 종료              | `applicationWillTerminate(_:)`                     | -                                            |


#### 백그라운드에서 작업을 완료하기 위한 방법은 어떤 것이 있나요?
### UIKit의 ViewController 생명주기에 대해 설명해주세요.

| 메서드                    | 설명                                                                 |
|---------------------------|----------------------------------------------------------------------|
| `loadView()`              | 뷰를 메모리에 로드하는 단계로, 커스텀 뷰를 생성하거나 초기화할 때 사용됩니다.         |
| `viewDidLoad()`           | 뷰가 메모리에 로드된 후 호출되며, 초기화 및 1회성 설정 작업을 수행합니다.             |
| `viewWillAppear(_:)`      | 뷰가 화면에 나타나기 직전에 호출되며, 화면 갱신이나 데이터 업데이트를 처리합니다.      |
| `viewDidAppear(_:)`       | 뷰가 화면에 완전히 나타난 후 호출되며, 애니메이션 시작이나 타이머 설정 등에 사용됩니다. |
| `viewWillDisappear(_:)`   | 뷰가 화면에서 사라지기 직전에 호출되며, 데이터 저장이나 네트워크 요청 취소 등을 처리합니다. |
| `viewDidDisappear(_:)`    | 뷰가 화면에서 완전히 사라진 후 호출되며, 리소스 해제나 정리 작업을 수행합니다.         |


### UIKit에서 TableView와 CollectionView의 차이점은 무엇인가요?

| 항목                 | UITableView                                               | UICollectionView                                                  |
|----------------------|------------------------------------------------------------|-------------------------------------------------------------------|
| 구조                 | 단일 열(Column), 여러 행(Row)                             | 다중 열과 행을 구성할 수 있는 2차원 구조                         |
| 스크롤 방향          | 수직 스크롤만 지원                                        | 수직 및 수평 스크롤 모두 지원                                    |
| 셀 레이아웃          | 기본 스타일 제공 (예: 기본, 상세 등)                      | 기본 스타일 없음, 완전한 커스터마이징 필요                      |
| 레이아웃 커스터마이징 | 제한적 (기본 제공 스타일 활용)                           | 자유로운 커스터마이징 가능 (FlowLayout, CompositionalLayout 등) |
| 사용 사례            | 단순한 리스트 (예: 연락처 목록)                           | 복잡한 그리드나 다양한 레이아웃이 필요한 경우 (예: 사진 갤러리) |


#### 셀을 재사용하는 이유와 방법을 설명해주세요.

- 1) 이유
- 메모리 효율성: 스크롤 시마다 새로운 셀을 생성하면 메모리 사용량이 증가합니다.​
성능 향상: 재사용을 통해 셀 생성 및 초기화 비용을 줄여 스크롤 성능을 개선합니다.

- 2) 방법
셀 등록: tableView.register(CustomCell.self, forCellReuseIdentifier: "CellID")​
셀 dequeuing: let cell = tableView.dequeueReusableCell(withIdentifier: "CellID", for: indexPath)​
재사용 준비: 셀 클래스에서 prepareForReuse() 메서드를 오버라이드하여 셀의 상태 초기화

#### 동적인 셀 높이(Dynamic Cell Height)를 설정하는 방법은 무엇인가요?

- Auto Layout을 활용하여 셀의 콘텐츠에 따라 높이가 자동으로 조정되도록 설정합니다.​
- tableView.rowHeight = UITableView.automaticDimension 설정으로 셀 높이를 자동으로 계산하게 합니다.​
- tableView.estimatedRowHeight = 100 등으로 예상 높이를 설정하여 초기 로딩 성능을 향상시킵니다.​

이러한 설정을 통해 콘텐츠의 양이나 종류에 따라 셀의 높이가 동적으로 조정됩니다.​

#### CollectionView의 레이아웃 종류와, 커스터마이징하는 방법은 무엇인가요?

- 1) 레이아웃 종류:
- UICollectionViewFlowLayout: 기본 제공 레이아웃으로, 셀을 행과 열로 배치합니다.​
- UICollectionViewCompositionalLayout: 복잡한 레이아웃을 구성할 수 있는 현대적인 레이아웃 시스템입니다. ​

- 2) 커스터마이징 방법:
- UICollectionViewDelegateFlowLayout 프로토콜을 구현하여 셀의 크기, 간격 등을 조정합니다.​
- UICollectionViewLayout을 상속하여 완전히 새로운 레이아웃을 구현할 수 있습니다.​

이러한 방법들을 통해 다양한 형태의 레이아웃을 구성할 수 있습니다.​

#### 테이블 뷰와 컬렉션 뷰의 데이터 소스(Data Source)와 델리게이트(Delegate)의 역할은 무엇인가요?

- 1) Data Source:
데이터 제공: 뷰에 표시할 데이터의 수와 내용을 제공합니다.​
필수 메서드: numberOfSections, numberOfRowsInSection/numberOfItemsInSection, cellForRowAt/cellForItemAt​

- 2) Delegate:
사용자 상호작용 처리: 셀 선택, 편집, 높이 설정 등 사용자와의 상호작용을 처리합니다.​
예시 메서드: didSelectRowAt/didSelectItemAt, heightForRowAt​

- Data Source는 데이터를 관리하고 제공하는 역할을, Delegate는 사용자와의 상호작용을 처리하는 역할을 담당합니다. ​

## 📚 iOS 개발
### iOS 앱에서 데이터를 저장하는 방법에는 어떤 것들이 있나요?**
#### `UserDefaults`의 사용 시 주의할 점은 무엇인가요?
#### Keychain은 어떤 데이터를 저장하기에 적합한가요?
#### Core Data와 SQLite의 차이점은 무엇이며, 각각 언제 사용하면 좋나요?

### 의존성 관리 도구(CocoaPods, Carthage, Swift Package Manager)의 종류와 차이점은 무엇인가요?
#### 각 도구의 사용 방법과 장단점을 설명해주세요.
#### 의존성 관리를 통해 얻을 수 있는 이점은 무엇인가요?

### 사용자 인터페이스(UI) 테스트와 단위(Unit) 테스트의 차이점은 무엇인가요?
#### XCTest 프레임워크를 사용하여 테스트를 작성하는 방법은 무엇인가요?
#### 테스트 주도 개발(TDD)의 장점은 무엇인가요?
#### 의존성 주입(Dependency Injection)을 활용하여 테스트 가능한 코드를 작성하는 방법은 무엇인가요?

### Xcode에서 Instruments를 사용하여 앱의 성능을 분석하는 방법은 무엇인가요?**
#### Time Profiler를 사용하여 성능 이슈를 찾는 방법을 설명해주세요.
#### Allocations Instrument를 사용하여 메모리 누수를 탐지하는 방법은 무엇인가요?
#### Leaks Instrument를 사용하여 메모리 누수를 찾는 방법은 무엇인가요?

### iOS 앱에서 의존성 주입(Dependency Injection)은 어떤 목적으로 사용되나요?
#### 의존성 주입의 세 가지 유형(Initializer Injection, Property Injection, Method Injection)을 설명해주세요.
#### 의존성 주입 컨테이너(Dependency Injection Container)란 무엇인가요?
#### 의존성 주입을 사용함으로써 얻을 수 있는 이점은 무엇인가요?

------ 분류중 -----

4. **CPU 아키텍처의 종류(예: ARM, x86)와 각 특징에 대해 설명해주세요.**

*   iOS 기기는 주로 어떤 아키텍처를 사용하며, 그 이유는 무엇일까요?
*   iOS 시뮬레이터는 보통 어떤 아키텍처에서 실행되며, 실제 기기와 어떤 차이가 있을까요? 이것이 개발에 어떤 영향을 미칠 수 있나요?
*   iOS 기기에서 사용되는 AP(Application Processor)의 특징과 역할에 대해 설명해주세요.
    *   iOS AP에는 CPU 외에 어떤 중요한 구성 요소들이 포함되어 있으며, 이들이 앱 성능에 어떻게 기여하나요? (예: GPU, Neural Engine)
*   SoC(System on a Chip)의 개념은 무엇인가요?
    *   SoC 설계가 모바일 기기에서 중요한 이유는 무엇일까요? (예: 전력 효율, 크기)

5. **운영체제의 역할과 iOS의 운영체제 구조에 대해 설명해주세요.**

*   운영체제가 없다면 앱 개발은 어떻게 달라질까요?
*   iOS의 샌드박스 구조는 어떻게 동작하나요?
    *   샌드박스 구조가 앱 보안 외에 어떤 장점이나 단점을 가질 수 있을까요?
*   커널(Kernel)의 역할은 무엇인가요?
    *   앱 코드에서 직접 커널 기능을 호출할 수 있나요? 없다면 어떻게 상호작용하나요?
*   다중 태스킹(Multitasking)은 어떻게 지원되나요?
    *   iOS 앱이 백그라운드에서 계속 실행될 수 있는 경우는 어떤 것들이 있나요? (예: 음악 재생, 위치 추적)

8. **iOS의 샌드박스(Sandbox) 개념과 역할, 그리고 앱 간 데이터 공유 방법에 대해 설명해주세요.**

*   샌드박스 때문에 앱 개발 시 겪을 수 있는 제약사항에는 어떤 것들이 있을까요?
*   앱 그룹(App Group)을 활용하여 데이터 공유를 하는 방법은 무엇인가요?
    *   앱 그룹을 통한 데이터 공유는 어떤 종류의 데이터에 적합할까요? 대용량 파일 공유에도 적합할까요?
    *   앱 확장(App Extension)과 앱 그룹은 어떤 관계가 있나요


16. **iOS에서 메모리 사이즈와 관련된 개념과 고려 사항에 대해 설명해주세요.**

*   메모리 정렬(Alignment)이 성능에 미치는 영향은 무엇인가요?
    *   메모리 정렬이 잘못되었을 때 발생할 수 있는 문제는 무엇인가요? (성능 저하 외에 Crash 가능성)
*   iOS 디바이스의 메모리 제약과 앱 메모리 제한에 대해 설명해주세요.
    *   앱의 메모리 사용량을 줄이기 위해 개발자가 할 수 있는 노력에는 어떤 것들이 있을까요? (이미지 최적화, 데이터 캐싱 전략, 불필요한 객체 해제 등)
*   메모리 경고(Memory Warning)가 발생하면 어떤 조치를 취해야 하나요?
    *   메모리 경고를 받았을 때, 가장 먼저 확인하거나 시도해 볼 수 있는 조치는 무엇일까요? (캐시 비우기, 백그라운드 작업 정리 등)
    *   Instruments의 Allocations, Leaks 도구를 사용해 본 경험이 있나요? 어떤 정보를 얻을 수 있나요?


22. **암호화와 보안의 기본 개념, 그리고 iOS 앱 보안을 위한 방안에 대해 설명해주세요.**

*   대칭키 암호화와 비대칭키(공개키) 암호화의 차이점과 각각의 장단점, 사용 예를 들어주세요. HTTPS에서는 이 둘을 어떻게 조합하여 사용하나요?
*   해싱(Hashing)은 무엇이며 암호화와 어떻게 다른가요? 비밀번호 저장에 왜 해싱(솔트 포함)이 사용될까요?
*   앱 내부에 사용자 비밀번호나 API 키 같은 민감한 정보를 저장해야 할 때, 어떻게 안전하게 처리해야 할까요? (Keychain 사용) UserDefaults에 저장하는 것과 비교했을 때 Keychain의 장점은 무엇인가요?
*   네트워크 통신 시 중간자 공격(Man-in-the-Middle Attack)은 무엇이며, HTTPS와 인증서 고정(Certificate Pinning)이 이를 어떻게 방지하는 데 도움이 되나요?

23. **가상 메모리(Virtual Memory)의 개념과 동작 원리에 대해 설명해주세요.**

*   가상 메모리를 사용하는 주된 이유는 무엇인가요? (메모리 관리 단순화, 프로세스 격리, 실제 메모리보다 큰 주소 공간 제공 등)
*   가상 메모리가 실제 물리 메모리(RAM)보다 클 수 있는 이유는 무엇인가요? 페이징(Paging)과 스와핑(Swapping)은 무엇인가요?
*   가상 메모리 시스템에서 페이지 폴트(Page Fault)는 무엇이며, 언제 발생하나요? 페이지 폴트가 자주 발생하면 어떤 성능 문제가 생길 수 있나요?

24. **데이터베이스의 종류와 iOS에서 주로 사용되는 데이터베이스에 대해 설명해주세요.**

*   관계형 데이터베이스(RDBMS)와 NoSQL 데이터베이스의 주요 차이점(데이터 모델, 스키마, 확장성 등)은 무엇인가요?
*   iOS 앱에서 데이터를 영구적으로 저장하기 위해 사용할 수 있는 방법들(UserDefaults, Plist, Keychain, Core Data, Realm, SQLite 등)의 특징과 각각의 장단점, 적합한 사용 사례를 설명해주세요.
    *   앱 내부에 간단한 사용자 설정 값(예: 다크 모드 여부, 폰트 크기)을 저장하고 싶을 때 어떤 기술을 사용하는 것이 가장 적합할까요?
    *   복잡한 객체 관계를 가지고 많은 양의 데이터를 관리해야 할 때는 어떤 기술을 고려해볼 수 있을까요? (Core Data, Realm)

3. **Auto Layout을 사용하는 이유와 장점은 무엇인가요?**
   - 제약 조건(Constraints)의 우선순위(Priority)는 어떻게 동작하나요?
   - Intrinsic Content Size란 무엇이며, 어떻게 활용되나요?
   - Ambiguous Layout과 Unsatisfiable Constraints는 무엇이며, 어떻게 해결하나요?

7. **Xcode에서 디버깅 시 자주 사용하는 기능은 무엇인가요?**
   - 중단점(Breakpoint)의 종류와 활용 방법을 설명해주세요.
   - LLDB 콘솔에서 유용한 명령어는 어떤 것이 있나요?


13. iOS 앱에서 코어 애니메이션(Core Animation)을 사용하는 방법은 무엇인가요?

- CALayer의 주요 속성과 메서드를 설명해주세요.
- 애니메이션 그룹(Animation Group)은 어떤 경우에 사용하나요?
- 키 프레임 애니메이션(Keyframe Animation)과 스프링 애니메이션(Spring Animation)의 차이점은 무엇인가요?


18. iOS 앱에서 로컬 푸시 알림(Local Push Notification)을 구현하는 방법은 무엇인가요?

- 로컬 푸시 알림과 원격 푸시 알림(Remote Push Notification)의 차이점은 무엇인가요?
- 푸시 알림의 콘텐츠(Content)와 트리거(Trigger)는 어떤 역할을 하나요?
- 사용자가 푸시 알림을 탭했을 때 앱의 동작을 처리하는 방법을 설명해주세요.

19. Swift에서 키 경로(Key Path)란 무엇이며, 어떻게 사용하나요?

- 키 경로 표현식(Key Path Expression)의 문법과 사용 예시를 설명해주세요.
- 런타임에 키 경로를 사용하여 속성에 접근하는 방법은 무엇인가요?
- 키 경로와 KVO(Key-Value Observing)의 관계를 설명해주세요

24. UIKit의 AdaptiveLayout과 Size Classes에 대해 설명해주세요.

- AdaptiveLayout의 개념과 사용 목적을 설명해주세요.
- Size Classes를 활용하여 다양한 기기에 적응적인 UI를 구현하는 방법을 예시와 함께 설명해주세요.

25. Swift의 커스텀 연산자(Custom Operator)에 대해 설명해주세요.

- 커스텀 연산자를 정의하는 방법과 주의 사항은 무엇인가요?
- 커스텀 연산자를 활용한 코드 가독성 향상 방안을 제시해주세요.

26. Swift의 생성자(Initializer)와 관련된 고급 개념에 대해 설명해주세요.

- 지정 생성자(Designated Initializer)와 편의 생성자(Convenience Initializer)의 차이점은 무엇인가요?
- 필수 생성자(Required Initializer)와 실패 가능한 생성자(Failable Initializer)는 어떤 경우에 사용하나요?

2. iOS 앱의 낮은 메모리 상황 대응 방안과 관련 API에 대해 설명해주세요.

- 낮은 메모리 경고(Low Memory Warning)의 개념과 iOS에서의 동작 방식에 대해 설명해주세요.
- didReceiveMemoryWarning() 메서드의 역할과 구현 방법에 대해 설명해주세요.
- 낮은 메모리 상황에서 앱의 안정성을 유지하기 위한 리소스 관리 전략에 대해 설명해주세요.

3. Swift의 메타타입(Metatype)과 미러(Mirror)에 대해 설명해주세요.

- 메타타입을 사용하여 타입 정보에 접근하는 방법은 무엇인가요?
- 미러를 사용하여 객체의 속성을 동적으로 탐색하는 방법을 설명해주세요.
- 메타타입과 미러를 활용한 실제 사용 사례를 들어주세요.

4. iOS 앱에서 바이너리 프레임워크(Binary Framework)를 생성하고 사용하는 방법은 무엇인가요?

- 바이너리 프레임워크와 소스 코드 프레임워크의 차이점은 무엇인가요?
- 바이너리 프레임워크를 생성할 때 고려해야 할 사항은 무엇인가요?
- 바이너리 프레임워크를 배포하고 버전 관리하는 방법을 설명해주세요.

6. Swift의 동적 멤버 조회(Dynamic Member Lookup)에 대해 설명해주세요.
@dynamicMemberLookup 속성의 역할과 사용 방법은 무엇인가요?
서브스크립트(Subscript)를 사용하여 동적 멤버 조회를 구현하는 방법을 설명해주세요.
동적 멤버 조회를 활용한 실제 사용 사례를 들어주세요.


8. Swift의 Property Wrapper에 대해 설명해주세요.

- Property Wrapper를 사용하는 이유와 장점은 무엇인가요?
- @State, @Binding, @ObservedObject 등의 Property Wrapper의 차이점과 사용 방법을 설명해주세요.
- Custom Property Wrapper를 만드는 방법과 사용 예시를 들어주세요.


11. iOS 앱에서 Keychain을 사용하여 민감한 데이터를 안전하게 저장하는 방법은 무엇인가요?

- Keychain Services API를 사용하여 데이터를 저장하고 읽어오는 과정을 설명해주세요.
- Keychain Access Groups를 사용하여 앱 간에 데이터를 공유하는 방법은 무엇인가요?
- Keychain의 접근 제어(Access Control) 옵션과 사용 방법을 설명해주세요.

