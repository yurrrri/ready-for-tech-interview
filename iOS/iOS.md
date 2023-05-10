## iOS (UIKit 위주)

### 1. bounds와 frame의 차이점을 설명하시오.

### 2. 앱이 InActive 상태가 되는 시나리오를 설명하시오.

### 3. scene delegate에 대해 설명하시오.

### 4. App의 Not running, Inactive, Active, Background, Suspended에 대해 설명하시오.

- Not running은 앱이 아직 실행되지 않은 상태, Inactive는 실행되고 있지만 이벤트를 받을 수 없는 상태, Background는 백그라운드에서 코드를 실행중인 상태, Suspended는 백그라운드에서 코드를 실행중이지 않은 상태를 의미합니다.

### 5. ViewController의 생명주기를 설명하시오.

- ViewController의 생명주기로 loadView, viewDidLoad, viewWillAppear, viewDidAppear, viewWillDisappear, viewDidDisappear, viewDidUnload가 있습니다.
- loadView는 뷰컨트롤러에 뷰를 할당하고
- viewDidLoad는 뷰가 완전히 메모리에 올라와있을 때 호출되어서 주로 초기값을 세팅할 때 해당 메소드에서 초기화를 하게 됩니다.
- viewWillAppear는 뷰가 사용자에게 보이기 직전에 호출되는데, 다른 뷰컨트롤러에 갔다가 다시 올 때 이 메소드부터 호출됩니다.
- viewDidAppear는 뷰가 사용자에게 보이기 시작할 때 호출됩니다.
- viewWillDisappear는 뷰가 뷰 계층에서 제거되기 직전에 호출되며, viewDidDisappear는 뷰가 뷰계층에서 완전히 사라지고 나서 호출되는 메소드입니다.

### 6. TableView와 CollectionView의 차이점을 설명하시오.
- TableView는 세로 스크롤만 가능하지만 CollectionView는 세로 혹은 가로 스크롤 모두 가능하고, flowLayout을 통해 다양한 레이아웃의 리스트를 구현할 수 있다는 점에서 차이가 있습니다.

### 7. NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오.
- NotificationCenter는 싱글톤 객체가 있는데, Notification을 보낼 객체들을 observer에 저장을 한 이후에 post를 하게 되면, Notification의 옵저버에 등록된 객체 모두에게 Notification을 보내게 됩니다.
- 활용방안으로는 앱 내에서 공식적으로 연결될 수 없는 컴포넌트 간 상호작용이 필요한 경우에 활용되는데, 예를들어 앱이 백그라운드에 진입했을 때 뷰컨트롤러에서 특정 액션을 취해야 한다거나 키보드가 등장할 때 키보드 크기를 가져와서 뷰컨트롤러에서 크기 만큼 입력창의 y값을 조정한다거나 등에서 활용됩니다.
