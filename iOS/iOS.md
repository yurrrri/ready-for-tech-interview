# iOS (UIKit 위주)

## iOS (UIKit)

### 1. Scene Delegate에 대해 설명하시오.

- iOS 13 이후에 멀티 윈도우가 지원되면서, 기존에 App Delegate가 앱의 UI 상태와 프로세스를 모두 관리하던 것에서 Scene 별로 UI 상태를 관리할 필요성이 생기면서 Scene의 UI 상태를 관리하는 것이 분리된 개념이 Scene Delegate입니다.
- Scene Delegate의 메소드를 통해 씬의 액티브 상태/포그라운드 상태/백그라운드 상태/인 액티브 상태일 때의 작업을 수행할 수 있습니다.

#### 1-1. App의 상태에는 어떤 것들이 있나요?

- Not running, Foreground, Foreground에서도 2가지로 나뉘는데 In Active, Active가 있으며 Background, Suspended가 있습니다.

### 2. App의 Not running, Inactive, Active, Background, Suspended에 대해 설명하시오.

- Not running은 앱이 아직 실행되지 않은 상태, Inactive는 실행되고 있지만 이벤트를 받을 수 없는 상태, Active는 포그라운드에 있으면서 사용자가 실제로 앱을 사용할 수 있는, 즉 앱이 이벤트를 받을 수 있는 상태, Background는 백그라운드에서 코드를 실행중인 상태, Suspended는 백그라운드에서 코드를 실행중이지 않는, 앱이 종료된 상태입니다.

### 3. 앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있나요?

- 포그라운드에 있을 때 앱의 리소스가 높은 우선순위로 사용되기 때문에 백그라운드 앱을 종료할 필요가 있고, 백그라운드에 있을 떄 가능한한 리소스를 최소화해야한다는 제약사항이 있습니다.

### 4. 앱이 InActive 상태가 되는 시나리오를 설명하시오.

- 앱이 처음으로 실행될 때 foreground로 진입하면서 인 액티브 상태였다가 바로 사용자에게 온전히 화면이 보여져서 사용자가 사용할 수 있을 때 액티브 상태로 진입합니다. 즉, 액티브 상태 이전에 인 액티브 상태를 거칩니다.
- 또한, 앱 스위처 상태에 돌입했을 때 In-Active 상태가 되며 백그라운드로 진입했을 때 백그라운드 직전에 인 액티브 상태가 됩니다.

### 5. ViewController의 생명주기를 설명하시오.

- ViewController의 생명주기로 init, loadView, viewDidLoad, viewWillAppear, viewDidAppear, viewWillDisappear, viewDidDisappear, viewDidUnload가 있습니다.
- init은 뷰컨트롤러를 생성할 때 호출되며, 저장 프로퍼티를 초기화할 때 사용되고
- loadView는 뷰컨트롤러에 뷰를 할당하고
- viewDidLoad는 뷰가 완전히 메모리에 올라와있을 때 호출되어서 주로 초기값을 세팅할 때 해당 메소드에서 초기화를 하게 됩니다.
- viewWillAppear는 뷰가 사용자에게 보이기 직전에 호출되는데, 다른 뷰컨트롤러에 갔다가 다시 올 때 이 메소드부터 호출됩니다.
- viewDidAppear는 뷰가 사용자에게 완전히 보이기 시작할 때 호출되며, 애니메이션을 이 시점에 그리게 됩니다.
- viewWillDisappear는 뷰가 뷰 계층에서 제거되기 직전에 호출되며, viewDidDisappear는 뷰가 뷰계층에서 완전히 사라지고 나서 호출되는 메소드입니다.

### 6. UIWindow 객체의 역할은 무엇인가?

- UIView의 컨테이너 역할로서, 앱 컨텐츠를 보여주고 이벤트를 뷰에 전달하는 역할을 합니다.
- 이외에도 Window의 rootViewController를 포함해서 이로부터 시작된 하나 이상의 뷰를 보여주는 역할을 합니다.

### 7. 상태 변화에 따라 다른 동작을 처리하기 위한 App Delegate 메서드들을 설명하시오.

- iOS 13 이후로 멀티 윈도우 개념에서 기존의 Window가 Scene으로 대체되었기에, 상태 변화를 각각의 Scene 별로 관리하는 것으로 변경되면서 Scene Delegate에 상태 변화 메소드가 이전되어서 이 델리게이트의 메소드를 설명드리겠습다.
- sceneDidDisconnect는 앱 스위처에서 Scene Session이 완전히 종료되었을 때 호출되며,
- sceneWillEnterForeground는 백그라운드에서 포그라운드로 진입될 때
- sceneDidBecomActive는 인 액티브상태에서 액티브 상태로 진입하여 사용자가 앱을 사용할 수 있을 때 호출됩니다.
- sceneWillResignActive는 액티브 상태에서 인 액티브 상태로 진입될 때 호출되고
- sceneDidBecomeBackground는 Scene session이 완전히 백그라운드로 진입할 때 호출됩니다.

### 8. NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오.
- NotificationCenter는 싱글톤 객체가 있는데, Notification을 보낼 객체들을 observer에 저장을 한 이후에 post를 하게 되면, Notification의 옵저버에 등록된 객체 모두에게 Notification을 보내게 됩니다.
- 활용방안으로는 앱 내에서 공식적으로 연결될 수 없는 컴포넌트 간 상호작용이 필요한 경우에 활용되는데, 예를들어 앱이 백그라운드에 진입했을 때 뷰컨트롤러에서 특정 액션을 취해야 한다거나 키보드가 등장할 때 키보드 크기를 가져와서 뷰컨트롤러에서 크기 만큼 입력창의 y값을 조정한다거나 등에서 활용됩니다.

### 9. TableView와 CollectionView의 차이점을 설명하시오.
- TableView는 세로 스크롤만 가능하지만 CollectionView는 세로 혹은 가로 스크롤 모두 가능하고, flowLayout을 통해 다양한 레이아웃의 리스트를 구현할 수 있다는 점에서 차이가 있습니다.

### 10. TableView의 동작 방식과 화면에 Cell을 출력하기 위해 최소한 구현해야 하는 DataSource 메서드를 설명하시오.

- UITableView 동작방식은 다음과 같습니다.
  - datasource, delegate, 재사용 관점에서 설명하기
- 어떠한 형태로 보여줄것인가?에 대해 관련이 깊습니다. 필수적으로 구현해야하는 메소드 첫번째로 numberOfRowsInSection가 있는데, 해당 메소드는 테이블뷰에 몇개의 row 데이터를 보여줄 것인가를 지정하는 메소드입니다. 두번째로 cellForRowAt 메소드가 있습니다. 해당 메소드는 테이블뷰 row마다 보여줄 UITableViewCell과 그 형태를 지정 후 반환합니다.

### 11. 하나의 View Controller 코드에서 여러 TableView Controller 역할을 해야 할 경우 어떻게 구분해서 구현해야 하는지 설명하시오.

- tableViewDataSource Delegate 메소드에서 테이블뷰 매개변수를 구분하고자 하는 테이블뷰에 따라 구분하여 구현하면 됩니다.

### 12. Bounds 와 Frame 의 차이점을 설명하시오.

https://zeddios.tistory.com/231
https://babbab2.tistory.com/45

- frame은 자신의 슈퍼뷰를 기준으로 하여 위치와 사이즈를 정의하며, bounds는 자신을 기준으로 하여 위치와 사이즈를 정의합니다.
- 따라서 frame의 origin 초기값은 슈퍼뷰에서 얼마만큼 떨어져있는가 이고, bounds의 origin 초기값은 항상 (0,0) 이 됩니다.
- 만약에 frame의 origin을 변경하게 되면 슈퍼로부터의 위치가 변화게 되고, bounds의 origin을 변경하면 해당 뷰를 바라보는 viewport의 위치가 이동하게 됩니다.

#### 12-1. 그럼 bounds와 frame은 각각 어쩔때 사용하는 것이 좋을까요?

- frame은 UIView의 위치와 크기를 설정할 때 사용하며, bounds는 View를 회전한 후의 실제 크기를 알고 싶거나 ScrollView에서 특정 위치로 스크롤하여 해당 부분을 보여주고 싶을 때 사용합니다.

### 13. iOS 앱을 만들고, User Interface를 구성하는 데 필수적인 프레임워크 이름은 무엇인지 설명하시오

- UIKit, SwiftUI

### 14. 모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가?

https://developer.apple.com/documentation/uikit/uiviewcontroller
https://cali-log.oopy.io/082474c8-2668-436b-af2f-f41fe891e1fb

- View Controller의 상위 클래스는 UIViewController입니다.
- 뷰로부터 사용자 액션을 전달받아 이를 모델에 전달하며, 모델 데이터의 변경이 발생했을 경우 해당 내용을 통해 뷰를 업데이트하는 역할을 합니다.
- 자신에게 속한 뷰의 크기를 조정하는 역할을 합니다. 

#### 14-1. UIViewController의 상위 클래스는 무엇인가요? 해당 클래스의 역할은 무엇인가요?

- UIViewController는 UIResponder 추상클래스를 구현하고 있습니다.
- (UIResponder 공부)

### 16. UINavigationController 의 역할이 무엇인지 설명하시오.

https://developer.apple.com/documentation/uikit/uinavigationcontroller

- UINavigationController는 뷰 컨트롤러를 네비게이션 계층으로 관리하고자 할 때, 자식 뷰 컨트롤러들을 관리하는 Container 뷰컨트롤러 역할을 합니다.
- 네비게이션 컨트롤러는 뷰를 스택 형태로 관리하기 떄문에 네비게이션 바에 이전 화면으로 돌아가기 위한 back button을 제공합니다.

### 17. 실제 디바이스가 없을 경우 개발 환경에서 할 수 있는 것과 없는 것을 설명하시오.

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

### 18. 앱의 콘텐츠나 데이터 자체를 저장/보관하는 특별한 객체를 무엇이라고 하는가?

**User Defaults** 
- 

**Core Data**

**SQLite**

**Realm**


### 19. Core Data와 Sqlite 같은 데이터 베이스의 차이점을 설명하시오.


### 19. 앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가?

- UIViewController입니다.
- UIView를 통해 전달되는 사용자의 액션에 대해 응답하며, 이 과정에서 데이터의 변경이 발생할 경우에 Model로부터 전달받은 변화 내용을 기반으로 뷰를 업데이트합니다.

### 20. 자신만의 Custom View를 만들려면 어떻게 해야하는지 설명하시오.
### 21. View 객체에 대해 설명하시오.

- 직사각형 영역 안에 포함된 컨텐츠를 관리하는 객체이며, 앱의 UI를 구성함에 있어 가장 기본적인 구성 단위입니다.
- 뷰는 다음과 같은 역할을 하게 됩니다.
    - 직사각형 영역 안에 컨텐츠를 그려냄
    - 뷰는 0개 이상의 SubView를 가지게 되는데,  이 SubView들의 사이즈 혹은 위치를 관리하게 됩니다.
    - UIResponder의 하위 클래스로서, 터치와 그 외의 이벤트에 대해 응답할 수 있습니다. 이 제스쳐를 핸들링하기 위해 gesture recognizer를 추가할 수 있습니다.

### 22. UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오.
### 23. iOS에서 뷰(View)와 레이어(Layer)의 개념과 차이점에 대해 설명해보세요.

### 24. setNeedsLayout와 setNeedsDisplay의 차이에 대해 설명하시오.

### 25. stackView의 장점과 단점에 대해서 설명하시오.

### 26. App thinning에 대해서 설명하시오.
### 27. 앱이 시작할 때 main.c 에 있는 UIApplicationMain 함수에 의해서 생성되는 객체는 무엇인가?
### 28. @Main에 대해서 설명하시오.
### 29. UIApplication 객체의 컨트롤러 역할은 어디에 구현해야 하는가?
### 30. Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오.
### 31. App Bundle의 구조와 역할에 대해 설명하시오.


#### 질문 출처

https://github.com/JeaSungLEE/iOSInterviewquestions
