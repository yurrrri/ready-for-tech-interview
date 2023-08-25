# iOS (UIKit 위주)

## iOS (UIKit)

### Scene Delegate에 대해 설명하시오.

- iOS 13 이후에 멀티 윈도우가 지원되면서, 기존에 App Delegate가 앱의 UI 상태와 프로세스를 모두 관리하던 것에서 Scene 별로 UI 상태를 관리할 필요성이 생기면서 Scene의 UI 상태를 관리하는 것이 분리된 개념이 Scene Delegate입니다.
- Scene Delegate의 메소드를 통해 씬의 액티브 상태/포그라운드 상태/백그라운드 상태/인 액티브 상태일 때의 작업을 수행할 수 있습니다.

### App의 상태에는 어떤 것들이 있나요?

- Not running, Foreground, Foreground에서도 2가지로 나뉘는데 In Active, Active가 있으며 Background, Suspended가 있습니다.

### App의 Not running, Inactive, Active, Background, Suspended에 대해 설명하시오.

- Not running은 앱이 아직 실행되지 않은 상태, Inactive는 실행되고 있지만 이벤트를 받을 수 없는 상태, Active는 포그라운드에 있으면서 사용자가 실제로 앱을 사용할 수 있는, 즉 앱이 이벤트를 받을 수 있는 상태, Background는 백그라운드에서 코드를 실행중인 상태, Suspended는 백그라운드에서 메모리는 남아있으나 코드를 실행중인 상태는 아닌 상황입니다.

### 앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있나요?

- 포그라운드에 있을 때 앱의 리소스가 높은 우선순위로 사용되기 때문에 백그라운드 앱을 종료할 필요가 있고, 백그라운드에 있을 떄 가능한한 리소스를 최소화해야한다는 제약사항이 있습니다.

### 앱이 InActive 상태가 되는 시나리오를 설명하시오.

- 앱이 처음으로 실행될 때 foreground로 진입하면서 인 액티브 상태였다가 바로 사용자에게 온전히 화면이 보여져서 사용자가 사용할 수 있을 때 액티브 상태로 진입합니다. 즉, 액티브 상태 이전에 인 액티브 상태를 거칩니다.
- 또한, 앱 스위처 상태에 돌입했을 때 In-Active 상태가 되며 백그라운드로 진입했을 때 백그라운드 직전에 인 액티브 상태가 됩니다.

### ViewController의 생명주기를 설명하시오.

- ViewController의 생명주기에는 loadView, viewDidLoad, viewWillAppear, viewDidAppear, viewWillDisappear, viewDidDisappear가 있습니다.
- loadView는 뷰컨트롤러와 연관된 뷰를 메모리에 올리는 과정으로, 코드로 짠 뷰의 경우 해당 시점에 교체할 수 있습니다.
- viewDidLoad는 뷰컨트롤러가 초기화되면서 최초 한번 호출되는 메서드로, 주로 뷰에 필요한 속성을 초기화할 때 사용합니다.
- viewWillAppear는 뷰가 완전히 보이기 직전, viewDidAppear는 뷰에 완전히 보일 때 호출되며 주로 애니메이션이나 타이머같은, 화면에 보일 때 처리해도 무관한 작업들을 진행합니다.
- viewWillDisappear, viewDidDisappear는 각각 뷰가 사라지기 직전 / 뷰가 완전히 보이지 않을 때 호출되며 뷰가 사라지기 직전 저장해야하는 정보들을 저장합니다. 

### 스토리보드 혹은 xib 파일은 언제 불리나요?

- loadView에서 뷰를 메모리에 올립니다.

### API 통신은 생명주기 어느 메서드에서 하는것이 적당할까요?

- 사용자에게 앱을 보여줄 때마다 새로운 내용을 업데이트할 필요가 있을 때, viewWillAppear에서 호춣하는 것이 적당할것 같습니다.

### UIWindow 객체의 역할은 무엇인가?

- UIView의 컨테이너 역할로서, 앱 컨텐츠를 보여주고 이벤트를 뷰에 전달하는 역할을 합니다.
- 이외에도 Window의 rootViewController를 포함해서 이로부터 시작된 하나 이상의 뷰를 보여주는 역할을 합니다.

### 상태 변화에 따라 다른 동작을 처리하기 위한 App Delegate 메서드들을 설명하시오.

- iOS 13 이후로 멀티 윈도우 개념에서 기존의 Window가 Scene으로 대체되었기에, 상태 변화를 각각의 Scene 별로 관리하는 것으로 변경되면서 Scene Delegate에 상태 변화 메소드가 이전되어서 이 델리게이트의 메소드를 설명드리겠습다.
- sceneDidDisconnect는 앱 스위처에서 Scene Session이 완전히 종료되었을 때 호출되며,
- sceneWillEnterForeground는 백그라운드에서 포그라운드로 진입될 때
- sceneDidBecomActive는 인 액티브상태에서 액티브 상태로 진입하여 사용자가 앱을 사용할 수 있을 때 호출됩니다.
- sceneWillResignActive는 액티브 상태에서 인 액티브 상태로 진입될 때 호출되고
- sceneDidBecomeBackground는 Scene session이 완전히 백그라운드로 진입할 때 호출됩니다.

### Delegate 패턴이란 무엇인가요? Delegate 패턴을 활용하는 경우를 예를 들어 설명하시오.

- 특정 인스턴스가 다른 인스턴스의 프로토콜을 준수하여 해야할 일을 대신 수행하는 패턴을 델리게이트 패턴이라고 합니다.
- 활용 예시로는, UITableViewDelegate 프로토콜을 준수하여 테이블뷰를 뷰컨트롤러에 띄워주거나, UITextField에서 입력이 시작했을 때의 동작을 UITextFieldDelegate 프로토콜을 준수함으로써 대신 수행할 수 있습니다.

### ❗️ Delegate란 무엇인지 설명하고, retain 되는지 안되는지 그 이유를 함께 설명하시오.


### NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오.
- NotificationCenter는 싱글톤 객체가 있는데, Notification을 보낼 객체들을 observer에 저장을 한 이후에 post를 하게 되면, Notification의 옵저버에 등록된 객체 모두에게 Notification을 보내게 됩니다.
- 활용방안으로는 앱 내에서 공식적으로 연결될 수 없는 컴포넌트 간 상호작용이 필요한 경우에 활용되는데, 예를들어 앱이 백그라운드에 진입했을 때 뷰컨트롤러에서 특정 액션을 취해야 한다거나 키보드가 등장할 때 키보드 크기를 가져와서 뷰컨트롤러에서 크기 만큼 입력창의 y값을 조정한다거나 등에서 활용됩니다.

### Delegates와 Notification 방식의 차이점에 대해 설명하시오.

- delegate 방식은 주로 이벤트를 1:1로 전달할 때 많이 사용됩니다. 주로 protocol을 정의하고 이를 이벤트를 대신 처리할 객체가 채택하여 사용하게 됩니다.
이에 따라 제 3 객체를 필요로 하지 않지만, 많은 객체에게 이벤트를 알리고 싶을 경우 많은 코드가 필요하여 비효율적이라는 단점이 있습니다.

- notification 방식은 이벤트를 1:N으로 전달할 때 용이합니다. NotificationCenter라는 싱글톤객체를 기반으로 이벤트 발생여부를 옵저버를 등록한 객체에게 전달하는 방식으로 구성됩니다. 
따라서 다수의 객체에게 손쉽게 이벤트 전달이 가능합니다. 하지만 제 3 객체를 필수적으로 필요로 하며, key값으로 발신-수신을 해야하는 구조이기 때문에 컴파일 중 수신여부를 확인하기 어렵다는 단점이 있습니다.

### TableView와 CollectionView의 차이점을 설명하시오.
- TableView는 세로 스크롤만 가능하지만 CollectionView는 세로 혹은 가로 스크롤 모두 가능하고, flowLayout을 통해 다양한 레이아웃의 리스트를 구현할 수 있다는 점에서 차이가 있습니다.

### TableView의 동작 방식과 화면에 Cell을 출력하기 위해 최소한 구현해야 하는 DataSource 메서드를 설명하시오.

- UITableView 동작방식은 다음과 같습니다.
  - datasource, delegate, 재사용 관점에서 설명하기
- 어떠한 형태로 보여줄것인가?에 대해 관련이 깊습니다. 필수적으로 구현해야하는 메소드 첫번째로 numberOfRowsInSection가 있는데, 해당 메소드는 테이블뷰에 몇개의 row 데이터를 보여줄 것인가를 지정하는 메소드입니다. 두번째로 cellForRowAt 메소드가 있습니다. 해당 메소드는 테이블뷰 row마다 보여줄 UITableViewCell과 그 형태를 지정 후 반환합니다.

### 하나의 View Controller 코드에서 여러 TableView Controller 역할을 해야 할 경우 어떻게 구분해서 구현해야 하는지 설명하시오.

- tableViewDataSource Delegate 메소드에서 테이블뷰 매개변수를 구분하고자 하는 테이블뷰에 따라 구분하여 구현하면 됩니다.

### Bounds 와 Frame 의 차이점을 설명하시오.

https://zeddios.tistory.com/231
https://babbab2.tistory.com/45

- frame은 자신의 슈퍼뷰를 기준으로 하여 위치와 사이즈를 정의하며, bounds는 자신을 기준으로 하여 위치와 사이즈를 정의합니다.
- 따라서 frame의 origin 초기값은 슈퍼뷰에서 얼마만큼 떨어져있는가 이고, bounds의 origin 초기값은 항상 (0,0) 이 됩니다.
- 만약에 frame의 origin을 변경하게 되면 슈퍼로부터의 위치가 변화게 되고, bounds의 origin을 변경하면 해당 뷰를 바라보는 viewport의 위치가 이동하게 됩니다.

### 그럼 bounds와 frame은 각각 어쩔때 사용하는 것이 좋을까요?

- frame은 UIView의 위치와 크기를 설정할 때 사용하며, bounds는 View를 회전한 후의 실제 크기를 알고 싶거나 ScrollView에서 특정 위치로 스크롤하여 해당 부분을 보여주고 싶을 때 사용합니다.

### iOS 앱을 만들고, User Interface를 구성하는 데 필수적인 프레임워크 이름은 무엇인지 설명하시오

- UIKit, SwiftUI

### ❗️ UIKit 클래스들을 다룰 때 꼭 처리해야하는 애플리케이션 쓰레드 이름은 무엇인가?

### 모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가?

https://developer.apple.com/documentation/uikit/uiviewcontroller
https://cali-log.oopy.io/082474c8-2668-436b-af2f-f41fe891e1fb

- View Controller의 상위 클래스는 UIViewController입니다.
- 뷰로부터 사용자 액션을 전달받아 이를 모델에 전달하며, 모델 데이터의 변경이 발생했을 경우 해당 내용을 통해 뷰를 업데이트하는 역할을 합니다.
- 자신에게 속한 뷰의 크기를 조정하는 역할을 합니다. 


### UINavigationController 의 역할이 무엇인지 설명하시오.

https://developer.apple.com/documentation/uikit/uinavigationcontroller

- UINavigationController는 뷰 컨트롤러를 네비게이션 계층으로 관리하고자 할 때, 자식 뷰 컨트롤러들을 관리하는 Container 뷰컨트롤러 역할을 합니다.
- 네비게이션 컨트롤러는 뷰를 스택 형태로 관리하기 떄문에 네비게이션 바에 이전 화면으로 돌아가기 위한 back button을 제공합니다.

### 실제 디바이스가 없을 경우 개발 환경에서 할 수 있는 것과 없는 것을 설명하시오.

https://developer.apple.com/library/archive/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator/TestingontheiOSSimulator.html
(아카이브 된 애플 문서라서 현재는 푸시알림, auto input 등 가능한 기능들이 몇개 있는 것으로 보임)

시뮬레이터에서 테스트할 수 없는 환경을 설명드리겠습니다.
- 하드웨어
```모션 지원(가속도계 및 자이로스코프)
카메라
근접 센서 
기압계
주변 광 센서
```

- Apple API
```
핸드오프 기능
Message UI (메시지 보내기) 
```

### 앱의 콘텐츠나 데이터 자체를 저장/보관하는 특별한 객체를 무엇이라고 하는가?

**User Defaults** 
- key-value 쌍의 데이터를 앱 내 데이터베이스에 영구적으로 저장하기 위한 객체이며, 보통 단일 데이터를 저장할 때 사용합니다.

**Core Data**
- UserDefaults 보다는 복잡하고 큰 데이터를 영구적으로 저장하기에 적합하며, Entity 기반으로 앱의 모델을 관리하는 프레임워크입니다.

### User Defaults에 struct나 class를 저장할 수 있나요?

- struct나 class와 같은 사용자 정의 타입은 NsData 형식으로 변경한다음, NSKeyedArchiver를 이용하여 저장할 수 있습니다.
- 가져올때는 NsKeyedUnArchiever로 객체를 복구해서 가져올 수 있습니다.

### 앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가?

- UIViewController입니다.
- UIView를 통해 전달되는 사용자의 액션에 대해 응답하며, 이 과정에서 데이터의 변경이 발생할 경우에 Model로부터 전달받은 변화 내용을 기반으로 뷰를 업데이트합니다.

### 자신만의 Custom View를 만들려면 어떻게 해야하는지 설명하시오.

- 첫번째 방식은 xib를 이용하는 방식입니다. xib파일과 해당 xib 파일과 동일한 이름을 가진 class 파일을 만들어서, xib에서 인터페이스를 구성한 후 해당 xib와 커스텀 클래스를 연결해줍니다.
- 두번째는 코드로 작성하는 방식입니다. UIView를 상속한 클래스에서 addSubView를 통해 자식 뷰들을 추가해서 코드로 뷰를 만드는 방식입니다. <br/>

이 때 2가지 방식 모두 init과 required init을 구현해야한다는 특징이 있습니다.

### init과 required init을 반드시 구현해야한다고 했는데 무슨 의미인가요?

- UIView는 지정 생성자를 생략하면 자동으로 상속하는데, 지정 생상자를 통해 커스텀하게 view를 초기화하게 되면 required init도 반드시 구현해야하므로, 2가지 메소드를 필수적으로 구현해야합니다.

### View 객체에 대해 설명하시오.

- 직사각형 영역 안에 포함된 컨텐츠를 관리하는 객체이며, 앱의 UI를 구성함에 있어 가장 기본적인 구성 단위입니다.
- 뷰는 다음과 같은 역할을 하게 됩니다.
    - 직사각형 영역 안에 컨텐츠를 그려냄
    - 뷰는 0개 이상의 SubView를 가지게 되는데,  이 SubView들의 사이즈 혹은 위치를 관리하게 됩니다.
    - UIResponder의 하위 클래스로서, 터치와 그 외의 이벤트에 대해 응답할 수 있습니다. 이 제스쳐를 핸들링하기 위해 gesture recognizer를 추가할 수 있습니다.

### ❗️사용자의 액션이 들어왔을 때 UIView와 UIViewController 각각의 역할에 대해 설명하시오.


### UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오.

https://babbab2.tistory.com/53

- Core Animation 프레임워크에 포함된 객체로서, UIView는 하나의 layer를 감싸고 있는 형태입니다.
- layer는 UIKit에서 처리할 수 없는 이미지 기반의 컨텐츠를 관리하는 역할을 하며, border, shadow, cornerRadius 등의 속성을 UIView 대신 변경해주는 역할을 하기도 합니다.

### iOS에서 뷰(View)와 레이어(Layer)의 개과 차이점에 대해 설명해보세요.

https://ios-development.tistory.com/977

- UIView가 layer를 감싸고 있는 형태이고, UIView는 1개 이상의 Layer를 가질 수 없지만 하나의 Layer는 여러개의 sub layer를 가질 수 있습니다.
- UIView는 UIKit에 속한 클래스인 반면에 Layer는 Core Animation 프레임워크에 속한 클래스입니다.
- UIView는 UIResponder의 서브클래스이기 때문에 사용자의 제스처를 제스처 인식기를 통해 인식할 수 있지만, layer는 UIResponder가 없기 때문에 제스처를 인식할 수 없습니다.

### setNeedsLayout와 setNeedsDisplay의 차이에 대해 설명하시오.

https://zeddios.tistory.com/359

- View의 drawing cycle과 관련한 메서드이며, setNeedsLayout은 다음 drawing cycle에 바로 크기나 위치의 변경사항을 업데이트 해달라 라는 메소드이며, setNeedsDisplay는 View의 컨텐트 (배경색이나 이미지같은)를 바로 다음 drawing cycle에 다시 그려줘 라고 명시하는 메소드입니다.

### layoutIfNeeded()는 뭔가요?

- drawing cycle을 기다리지 않고 호출 즉시 크기나 위치를 다시 적용해달라고 명시하는 메소드

### stackView의 장점과 단점에 대해서 설명하시오.

장점으로는 다음과 같습니다.

- stackView는 해당 뷰의 SubView들을 조건에 따라 자동으로 간격조절 및 정렬을 해주기 때문에, 개발자가 직접 constraint를 일일이 다 줄 번거로움이 훨씬 줄어들게 됩니다.
- 이에 따라 뷰를 추가하거나 삭제하더라도 제약을 거는것이 매우 편리해집니다.

단점으로는 다음과 같습니다.

- stackView의 SubView는 StackView가 지정한 뷰의 배치나 정렬을 따르기에, 개별 SubView의 디테일한 위치나 크기 조정은 어려울 수 있습니다.

### ❗️App thinning에 대해서 설명하시오.

### 앱이 시작할 때 main.c 에 있는 UIApplicationMain 함수에 의해서 생성되는 객체는 무엇인가?

https://developer.apple.com/documentation/uikit/uiapplication

- UIApplictaion 객체를 생성합니다. 앱당 싱글톤으로 1개의 인스턴스가 존재하는 개념이며 앱의 상태를 AppDelegate의 UIApplicationDelegate에게 전달하게 됩니다.

### @Main에 대해서 설명하시오. 

- 앱을 시작할 때의 진입점을 지정하는 어노테이션으로, iOS앱에서는 App Delegate에 지정되어있어 App Delegate를 진입점으로 하여, 앱 상태를 관리하는 UIApplication 인스턴스 생성 및 메인 UI를 로드하게 됩니다.

### 앱 생명주기에서 didFinishLaunching() 이전에는 어떤 과정이 있나요? 

- App Delegate를 진입점으로 하여, 앱 상태를 관리하는 UIApplication 인스턴스 생성 및 메인 UI를 로드, 앱 초기화를 진행하게 됩니다.

### UIApplication 객체의 컨트롤러 역할은 어디에 구현해야 하는가?

- UIApplicationMain()

### Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오.

- Cocoa Touch Framework에 포함되어있는 프레임워크로, URL을 다룰 때 쓰는 클래스인 URLSession, Json을 엔코딩/디코딩할 때 사용하는 JSONEncoder/Decoder 등이 있습니다.

### App Bundle의 구조와 역할에 대해 설명하시오.

https://neph3779.github.io/ios/WhatIsAppBundle/

- App Bundle 안에는 앱을 실제로 실행하는 파일, info.plist, 사용하는 프레임워크, 이미지나 문자열 등의 Resource 파일, 화면을 스토리보드나 Xib로 구현할 경우에 해당 파일 또한 App Bundle 안에 포함됩니다.

### NSCache와 딕셔너리로 캐시를 구성했을때의 차이를 설명하시오.

- NSCache는 딕셔너리와는 달리 자동 삭제 정책이 있어서 필요에 따라 일부 항목을 제거합니다.
- key의 이름을 변경하게 되면, 딕셔너리는 키 객체를 복사하는 대신에, NSCache는 키 객체를 복사하지 않고 기존의 키를 그대로 가져가게 된다는 차이가 있습니다. 

### prepareForReuse에 대해서 설명하시오.

- 테이블뷰에서 셀을 재사용하여 객체를 반환하기 전에 호출되는 메소드로, content와 무관한 내용들은 재사용하게 됩니다.
- 따라서 재사용으로 인해 셀 간 내용이 섞이는 이슈 등을 방지하기 위해 해당 메소드에서 데이터를 초기 상태로 초기화해주는 작업을 진행해야 합니다.

### 다크모드를 지원하는 방법에 대해 설명하시오.

https://labs.brandi.co.kr//2019/12/19/kimjh.html
- UITraitCollection.userInterfaceStyle에서 dark 일 경우와 아닐 경우의 color를 각각 지정해주고
- 이미지의 경우 Appreance에서 Any, Dark 속성을 주변 다크모드 일때와 아닐 떄의 이미지를 각각 추가할 수 있습니다.
- 혹은 이미지에 tint color를 적용하여 변경할 수도 있습니다.

### Dynamic Library와 Static Library의 차이점에 대해 설명해보세요.

https://ios-development.tistory.com/800
- 두 가지 라이브러리는 라이브러리를 프로젝트에 어떤 시점에 포함시키는지에 따라 차이가 있습니다.
- static library는 컴파일 단계에서 object 언어에서 실행파일로 변경될 때 포함되는 라이브러리고, dynamic library는 런타임 중에 해당 라이브러리를 연결합니다.
- 이에 따라 static library는 메모리 효율이 좋지 않다라는 단점이 있고, dynamic library는 그에 비해 필요할 때마다 라이브러리를 불러오므로 메모리 효율이 좋다는 장점이 있습니다.
- 또한, static library는 추가 작업없이 라이브러리를 사용할 수 있다는 장점이 있는 반면에 dynamic library는 라이브러리를 찾아서 올리는 시간이 추가적으로 소요되므로 시간이 상대적으로 더 걸린다는 단점이 있습니다.

### MVVM, MVI, Ribs, Viper 등 자신이 알고있는 아키텍쳐를 설명하시오.
### 의존성 주입에 대하여 설명하시오.

- 클래스 외부에서 객체를 생성해서 그 객체를 클래스 내부에 주입하는것을 의존성 주입이라고 합니다.
클래스 내부에서 객체를 직접생성하지 않기때문에 객체간 결합도를 낮출 수 있으며, Swift에서는 프로토콜을 이용하여 의존성 문제를 해결합니다.
결합도가 낮아진다는것은 한 클래스가 변경될 경우 다른클래스가 변경될 필요성이 적어진다는 뜻으로도 이해할 수 있습니다.

### Responder Chain은 무엇이고, 구조가 어떻게 되어있는가?

- responder chain은 이벤트를 first responder에서부터 이벤트가 처리될 때까지 상위 뷰인 UIView에서 UIViewController, UIWindow까지 거슬러 올라가서 이벤트를 전달하는 구조입니다.

### First Responder 역할에 대해 설명하시오.

- 이벤트 발생시 가장 먼저 이벤트를 받는 responder로, responder chain중에 가장 첫번째로 이벤트를 처리함

### selector는 무엇인가. 어떻게 불러내는가.

- selector 뒤에 명시한 속성이나 메소드를 가리키기 위한 문법이며 주로 코드로 UI를 짤 때 유저의 이벤트가 발생할 때 어떤 메소드를 실행할 것인지 지정할 때 많이 사용함

### ❗️Cocoapod을 gitignore에 넣어야하는 이유는 뭘까요?


## Autolayout

### 오토레이아웃을 코드로 작성하는 방법은 무엇인가? (3가지)

https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/ProgrammaticallyCreatingConstraints.html#//apple_ref/doc/uid/TP40010853-CH16-SW1 <br/>
https://nsios.tistory.com/99 <br/>

1) NSLayoutConstraint
- 제약을 가지는 뷰의 몇 배, 그리고 상수 몇만큼 떨어져있는지에 대한 수식으로 오토레이아웃을 작성하는 방법입니다.

2) NSLayoutAnchor
- NSLayoutConstraint가 사용이 불편해서 간소화되어 나온 클래스로, 어떤 뷰와 제약이 걸려있는지 그리고 top/leading.trailing.bottom의 어떤 부분과 제약이 걸려있는지, 몇만큼 떨어져있는지에 대한 몇 가지 정보만 주어 간결하게 오토레이아웃을 세팅가능합니다.

3) Visual Format Language

레이아웃의 시각적 표현으로, NSLayoutConstraint의 withVisualFormat 속성을 활용하여 좀 더 시각적으로 간결하게 활용하는 방법입니다.
뷰는 [] (대괄호) 사용
뷰간연결은 - (하이픈)을 사용

### 코드로 작성했을 때의 장단점은 뭔가요?

https://www.toptal.com/ios/ios-user-interfaces-storyboards-vs-nibs-vs-custom-code

장점
- 빠르고 가볍다.
- 협업 시 Conflict가 날 때 해결에 용이하다.
- 뷰에 대한 재사용이 용이하다.

단점
- 화면의 전반적인 흐름을 파악하기 어렵다.

### Intrinsic Size에 대해서 설명하시오.
https://velog.io/@eddy_song/intrinsic-content-size

- intrinsic content size는 고유 콘텐츠의 크기로, intrinsic content size를 가지고 있는 뷰는 해당 사이즈에 맞춰서 자동으로 조건을 설정하기 떄문에 개발자가 별도로 크기를 지정해주지 않아도 됩니다.
- intrinsic content size를 가지고 있는 뷰들은 다음과 같습니다.
- UISlider: width만 가짐
- UITextView의 경우 스크롤이 있다면 intrinsic size가 없지만, 스크롤이 없다면 텍스트의 크기에 따라 결정되기 때문에 Intrinsic size가 있습니다.
- UIImageView의 경우 이미지가 들어왔을 때 이미지의 크기에 기반하여 intrinsic size가 결정됩니다.
- 그 외의 UIView/UIStackView 외의 다른 UI Component는 intrinsic content size를 가지고 있습니다.

### hugging, resistance에 대해서 설명하시오.

- intrinsic size가 있는 뷰에 개발자가 특정 width나 height에 대한 조건을 주었을 때, 어떤 사항을 더 우선순위로 하여 사이즈를 조정해줄 것인가와 관련한 속성입니다.
- hugging은 intrinsic size 이상으로 늘어나지 않으려고 하도록 하는 속성이며, Resistance는 intrinsic size 이하로 줄어들지 않으려고 하도록 하는 속성입니다.
- 디폴트로 hugging은 250, resistance는 750로 세팅되어있으며 만약 특정 뷰가 이 이상 더 늘어나지 않도록/줄어들지 않도록 하고자하면 해당 뷰의 hugging의 우선순위 값을 기존값보다 키워주면 됩니다.

### 스토리보드를 이용했을때의 장단점을 설명하시오.

https://www.toptal.com/ios/ios-user-interfaces-storyboards-vs-nibs-vs-custom-code

장점
- 인터페이스의 전반 흐름을 바로 확인 가능하며, 레이아웃 결과를 예측하기 쉽다.

단점
- 앱의 규모가 커질수록 화면 로딩이 무거워진다.
- IBOutlet이나 IBAction의 연결이 끊어졌을 때 파악이 어렵다.
- 협업 시, 스토리보드를 분리하지 않는 경우 conflict가 날 때 해결이 어려워진다.

### Storyboard에서 충돌이 이미 발생했을 때 어떻게 해결하는가?

### Safearea에 대해서 설명하시오.

- iOS 11이후 등장한 개념으로, 노치나 하단 홈에 의해 가려질 수 있는 부분에 대한 마진을 자체적으로 가지는 영역입니다.

### Left Constraint 와 Leading Constraint 의 차이점을 설명하시오.

https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/AnatomyofaConstraint.html

- left constraint는 절대적인 개념으로, 항상 화면의 왼쪽을 가리킵니다.
- leading constraint는 장치의 국가 설정에 영향을 받게 되는데, 국가별 읽는 방향에 따라 방향이 달라진다. 예를들어 아랍권 국가의 경우 leading이 오른쪽, trailing이 왼쪽을 가리키게 된다
- 따라서 애플은 leading과 trailing 사용을 권장하고있음.

### Auto Layout과 Frame-based Layout의 차이점은 무엇인가요?

- Autolayout은 뷰와의 관계에 제약을 두어 레이아웃을 짜는 방식이며, Frame-based layout은 view의 frame을 직접 지정하여 레이아웃을 짜는 방식입니다.
- Autolayout은 뷰 간의 관계로 정의하기 때문에 기기별로 대응이 가능하다는 장점이 있는 반면에 Frame-based layout은 그렇지 않아서 기기 별로 대응하는 레이아웃을 별도로 구성해야한다는 번거로움이 있습니다.

### ❗️ 오토레이아웃이 깨졌을 때 어떻게 대처하는가

### ❗️ 뷰 디버깅은 어떻게 하는지?


<br/>

## GCD, 동시성 프로그래밍
### GCD API 동작 방식과 필요성에 대해 설명하시오.

- Queue라는 작업열에 보내기만 하면, iOS가 적절하게 다른 스레드로 분산하여 동시성 처리할 수 있도록 하여 동작함. 여기서 Qos라는 우선순위를 개발자가 따로 지정해서 우선순위에 따른 스레드 순서를 지정하는 것 또한 가능하다.
- 비동기 처리가 필요한 이유는 2가지가 있다.
1) 효율적인 프로그래밍을 위해 -> 여러 스레드로 분산처리 하므로 순서가 중요한 작업이 아니라면 더 효율적으로 동작한다.
2) 사용성, 반응성이 좋은 앱을 위해 -> 이미지나 네트워킹같이 시간이 오래걸리는 작업을 동기적으로 처리하면 사용자는 처리될 때까지 기다려야 하므로 사용성이 좋지 않고, 화면이 끊겨 보이게 될 것임


### GCD의 Queue 종류는 어떤게 있나요?

- 메인스레드인 main 뷰, 메인 스레드 이외의 부가적인 작업열인 글로벌 큐, 사용자가 label을 통해 커스텀하여 사용 가능한 커스텀 큐가 있습니다.

### ❗️ 그럼, 한 화면에 썸네일이 100개 정도 있다고 치고, 100개의 각각의 통신을 하게 된다면, GCD는 이걸 버텨낼까요? GCD는 몇가지의 쓰레드까지 가능할까요? 해결 방법은?



<br/>

#### 질문 출처

https://github.com/JeaSungLEE/iOSInterviewquestions

면접 스터디에서 나온 꼬리질문, 면접 경험에서 나온 질문
