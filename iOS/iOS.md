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
- key-value 쌍의 데이터를 앱 내 데이터베이스에 영구적으로 저장하기 위한 객체이며, 보통 단일 데이터를 저장할 때 사용합니다.

**Core Data**
- UserDefaults 보다는 복잡하고 큰 데이터를 영구적으로 저장하기에 적합하며, Entity 기반으로 앱의 모델을 관리하는 프레임워크입니다.

#### 18-1. User Defaults에 struct나 class를 저장할 수 있나요?

- struct나 class와 같은 사용자 정의 타입은 NsData 형식으로 변경한다음, NSKeyedArchiver를 이용하여 저장할 수 있습니다.
- 가져올때는 NsKeyedUnArchiever로 객체를 복구해서 가져올 수 있습니다.

### 19. 앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가?

- UIViewController입니다.
- UIView를 통해 전달되는 사용자의 액션에 대해 응답하며, 이 과정에서 데이터의 변경이 발생할 경우에 Model로부터 전달받은 변화 내용을 기반으로 뷰를 업데이트합니다.

### 20. 자신만의 Custom View를 만들려면 어떻게 해야하는지 설명하시오.

- 첫번째 방식은 xib를 이용하는 방식입니다. xib파일과 해당 xib 파일과 동일한 이름을 가진 class 파일을 만들어서, xib에서 인터페이스를 구성한 후 해당 xib와 커스텀 클래스를 연결해줍니다.
- 두번째는 코드로 작성하는 방식입니다. UIView를 상속한 클래스에서 addSubView를 통해 자식 뷰들을 추가해서 코드로 뷰를 만드는 방식입니다. <br/>

이 때 2가지 방식 모두 init과 required init을 구현해야한다는 특징이 있습니다.

#### 20-1. init과 required init을 반드시 구현해야한다고 했는데 무슨 의미인가요?

- UIView는 지정 생성자를 생략하면 자동으로 상속하는데, 지정 생상자를 통해 커스텀하게 view를 초기화하게 되면 required init도 반드시 구현해야하므로, 2가지 메소드를 필수적으로 구현해야합니다.

### 21. View 객체에 대해 설명하시오.

- 직사각형 영역 안에 포함된 컨텐츠를 관리하는 객체이며, 앱의 UI를 구성함에 있어 가장 기본적인 구성 단위입니다.
- 뷰는 다음과 같은 역할을 하게 됩니다.
    - 직사각형 영역 안에 컨텐츠를 그려냄
    - 뷰는 0개 이상의 SubView를 가지게 되는데,  이 SubView들의 사이즈 혹은 위치를 관리하게 됩니다.
    - UIResponder의 하위 클래스로서, 터치와 그 외의 이벤트에 대해 응답할 수 있습니다. 이 제스쳐를 핸들링하기 위해 gesture recognizer를 추가할 수 있습니다.

#### 21-1. 사용자의 액션이 들어왔을 때 UIView와 UIViewController 각각의 역할에 대해 설명하시오.


### 22. UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오.

https://babbab2.tistory.com/53

- Core Animation 프레임워크에 포함된 객체로서, UIView는 하나의 layer를 감싸고 있는 형태입니다.
- layer는 UIKit에서 처리할 수 없는 이미지 기반의 컨텐츠를 관리하는 역할을 하며, border, shadow, cornerRadius 등의 속성을 UIView 대신 변경해주는 역할을 하기도 합니다.

### 23. iOS에서 뷰(View)와 레이어(Layer)의 개념과 차이점에 대해 설명해보세요.

https://ios-development.tistory.com/977

- UIView가 layer를 감싸고 있는 형태이고, UIView는 1개 이상의 Layer를 가질 수 없지만 하나의 Layer는 여러개의 sub layer를 가질 수 있습니다.
- UIView는 UIKit에 속한 클래스인 반면에 Layer는 Core Animation 프레임워크에 속한 클래스입니다.
- UIView는 UIResponder의 서브클래스이기 때문에 사용자의 제스처를 제스처 인식기를 통해 인식할 수 있지만, layer는 UIResponder가 없기 때문에 제스처를 인식할 수 없습니다.

### 24. setNeedsLayout와 setNeedsDisplay의 차이에 대해 설명하시오.

### 25. stackView의 장점과 단점에 대해서 설명하시오.

장점으로는 다음과 같습니다.

- stackView는 해당 뷰의 SubView들을 조건에 따라 자동으로 간격조절 및 정렬을 해주기 때문에, 개발자가 직접 constraint를 일일이 다 줄 번거로움이 훨씬 줄어들게 됩니다.
- 이에 따라 뷰를 추가하거나 삭제하더라도 제약을 거는것이 매우 편리해집니다.

단점으로는 다음과 같습니다.

- stackView의 SubView는 StackView가 지정한 뷰의 배치나 정렬을 따르기에, 개별 SubView의 디테일한 위치나 크기 조정은 어려울 수 있습니다.

### 26. App thinning에 대해서 설명하시오.

### 27. 앱이 시작할 때 main.c 에 있는 UIApplicationMain 함수에 의해서 생성되는 객체는 무엇인가?

- UIApplication 객체가 생성되며, 이 객체는 

### 28. @Main에 대해서 설명하시오.

### 29. UIApplication 객체의 컨트롤러 역할은 어디에 구현해야 하는가?

### 30. Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오.

- Cocoa Touch Framework에 포함되어있는 프레임워크로, URL을 다룰 때 쓰는 클래스인 URLSession, Json을 엔코딩/디코딩할 때 사용하는 JSONEncoder/Decoder 등이 있습니다.

### 31. App Bundle의 구조와 역할에 대해 설명하시오.

https://neph3779.github.io/ios/WhatIsAppBundle/

- App Bundle 안에는 앱을 실제로 실행하는 파일, info.plist, 사용하는 프레임워크, 이미지나 문자열 등의 Resource 파일, 화면을 스토리보드나 Xib로 구현할 경우에 해당 파일 또한 App Bundle 안에 포함됩니다.

### 32. NSCache와 딕셔너리로 캐시를 구성했을때의 차이를 설명하시오.

- NSCache는 딕셔너리와는 달리 자동 삭제 정책이 있어서 필요에 따라 일부 항목을 제거합니다.
- key의 이름을 변경하게 되면, 딕셔너리는 키 객체를 복사하는 대신에, NSCache는 키 객체를 복사하지 않고 기존의 키를 그대로 가져가게 된다는 차이가 있습니다. 

### 33. prepareForReuse에 대해서 설명하시오.

- 테이블뷰에서 셀을 재사용하여 객체를 반환하기 전에 호출되는 메소드로, content와 무관한 내용들은 재사용하게 됩니다.
- 따라서 재사용으로 인해 셀 간 내용이 섞이는 이슈 등을 방지하기 위해 해당 메소드에서 데이터를 초기 상태로 초기화해주는 작업을 진행해야 합니다.

### 34. 다크모드를 지원하는 방법에 대해 설명하시오.

https://labs.brandi.co.kr//2019/12/19/kimjh.html
- UITraitCollection.userInterfaceStyle에서 dark 일 경우와 아닐 경우의 color를 각각 지정해주고
- 이미지의 경우 Appreance에서 Any, Dark 속성을 주변 다크모드 일때와 아닐 떄의 이미지를 각각 추가할 수 있습니다.
- 혹은 이미지에 tint color를 적용하여 변경할 수도 있습니다.

### 35. Dynamic Library와 Static Library의 차이점에 대해 설명해보세요.

https://ios-development.tistory.com/800
- 두 가지 라이브러리는 라이브러리를 프로젝트에 어떤 시점에 포함시키는지에 따라 차이가 있습니다.
- static library는 object 언어에서 실행파일로 변경될 때 포함되는 라이브러리고, dynamic library는 런타임 중에 해당 라이브러리를 연결합니다.
- 이에 따라 static library는 메모리 효율이 좋지 않다라는 단점이 있고, dynamic library는 그에 비해 필요할 때마다 라이브러리를 불러오므로 메모리 효율이 좋다는 장점이 있습니다.
- 또한, static library는 추가 작업없이 라이브러리를 사용할 수 있다는 장점이 있는 반면에 dynamic library는 라이브러리를 찾아서 올리는 시간이 추가적으로 소요되므로 시간이 상대적으로 더 걸린다는 단점이 있습니다.

### 36. MVVM, MVI, Ribs, VIP 등 자신이 알고있는 아키텍쳐를 설명하시오.
### 37. 의존성 주입에 대하여 설명하시오.

## Autolayout

### 1. 오토레이아웃을 코드로 작성하는 방법은 무엇인가? (3가지

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

#### 1-1. 코드로 작성했을 때의 장단점은 뭔가요?

https://www.toptal.com/ios/ios-user-interfaces-storyboards-vs-nibs-vs-custom-code

장점
- 빠르고 가볍다.
- 협업 시 Conflict가 날 때 해결에 용이하다.
- 뷰에 대한 재사용이 용이하다.

단점
- 화면의 전반적인 흐름을 파악하기 어렵다.

### 2. Intrinsic Size에 대해서 설명하시오.
https://velog.io/@eddy_song/intrinsic-content-size

- intrinsic content size는 고유 콘텐츠의 크기로, intrinsic content size를 가지고 있는 뷰는 해당 사이즈에 맞춰서 자동으로 조건을 설정하기 떄문에 개발자가 별도로 크기를 지정해주지 않아도 됩니다.
- intrinsic content size를 가지고 있는 뷰들은 다음과 같습니다.
- UISlider: width만 가짐
- UITextView의 경우 스크롤이 있다면 intrinsic size가 없지만, 스크롤이 없다면 텍스트의 크기에 따라 결정되기 때문에 Intrinsic size가 있습니다.
- UIImageView의 경우 이미지가 들어왔을 때 이미지의 크기에 기반하여 intrinsic size가 결정됩니다.
- 그 외의 UIView/UIStackView 외의 다른 UI Component는 intrinsic content size를 가지고 있습니다.

### 3. hugging, resistance에 대해서 설명하시오.

- intrinsic size가 있는 뷰에 개발자가 특정 width나 height에 대한 조건을 주었을 때, 어떤 사항을 더 우선순위로 하여 사이즈를 조정해줄 것인가와 관련한 속성입니다.
- hugging은 intrinsic size 이상으로 늘어나지 않으려고 하도록 조건을 주는것이며, Resistance는 intrinsic size 이하로 줄어들지 않으려고 하도록 조건을 주는 것입니다.
- 디폴트로 hugging은 250, resistance는 750로 세팅되어있으며 만약 특정 뷰가 이 이상 더 늘어나지 않도록 하고자하면 해당 뷰의 hugging의 우선순위 값을 250 이상으로 늘려주면 된다.

### 4. 스토리보드를 이용했을때의 장단점을 설명하시오.

https://www.toptal.com/ios/ios-user-interfaces-storyboards-vs-nibs-vs-custom-code

장점
- 인터페이스의 전반 흐름을 바로 확인 가능하며, 레이아웃 결과를 예측하기 쉽다.

단점
- 앱의 규모가 커질수록 화면 로딩이 무거워진다.
- IBOutlet이나 IBAction의 연결이 끊어졌을 때 파악이 어렵다.
- 협업 시, 스토리보드를 분리하지 않는 경우 conflict가 날 때 해결이 어려워진다.
- 데이터의 흐름을 스토리보드만으로 알기 어렵다는 단점이 있다.

### 5. Safearea에 대해서 설명하시오.

- iOS 11이후 등장한 개념으로, 노치나 하단 홈에 의해 가려질 수 있는 부분에 대한 마진을 자체적으로 가지는 영역입니다.

### 6. Left Constraint 와 Leading Constraint 의 차이점을 설명하시오.

https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/AnatomyofaConstraint.html

- left constraint는 절대적인 개념으로, 항상 화면의 왼쪽을 가리킵니다.
- leading constraint는 장치의 국가 설정에 영향을 받게 되는데, 국가별 읽는 방향에 따라 방향이 달라진다. 예를들어 오른쪽에서 왼쪽으로 읽는 문화권의 경우 leading이 오른쪽, trailing이 왼쪽을 가리키게 된다
- 따라서 애플은 leading constraint 사용을 권장하고있음.

### 7. Auto Layout과 Frame-based Layout의 차이점은 무엇인가요?

- Autolayout은 뷰와의 관계에 제약을 두어 레이아웃을 짜는 방식이며, Frame-based layout은 view의 frame을 직접 지정하여 레이아웃을 짜는 방식입니다.
- Autolayout은 뷰 간의 관계로 정의하기 때문에 기기별로 대응이 가능하다는 장점이 있는 반면에 Frame-based layout은 그렇지 않아서 기기 별로 대응하는 레이아웃을 별도로 구성해야한다는 번거로움이 있습니다.


#### 질문 출처

https://github.com/JeaSungLEE/iOSInterviewquestions

면접 스터디에서 나온 꼬리질문 추가
