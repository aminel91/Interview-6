# Android

###Android Process와 Thread

###Android Service vs Intent Service

* IntentService는 Service를 상속받은 클래스로 작업을 수행하는 스레드(Thread)를 별도로 생성하는 서비스
* 여러번 실행될 경우 별도의 Queue를 통해 처리됨.

####IntentService의 장점

* 서비스의 콜백메소드들에 대해서 디폴트 구현을 제공하기 때문에 별도로 콜백 메소드를 구현할 필요가 없음. 
* onHandleIntent() 메소드만 구현하면 되고 이 메소드 안에서 클라이언트에 의해 제공되는 작업.
* 작업이 완료되면 자동적으로 서비스를 중단하기 때문에 stopSelf() 또는 stopService()를 호출할 필요가 없음.

참고 <http://android-kr.tistory.com/9#Lifecycle> 

###ListView의 ViewHolder패턴에 대해 설명하고 왜 사용하는지에 대해 설명

###View와 Fragment의 차이

###Asynctask에서 UIThread를 제어하기 위해 사용할 수 있는 기법에 대해 모두 말하시오

### MVP, MVVM에 대한 설명

### Android TroubleShooting 경험

### Image Process에 대한 설명 및 경험과 Caching처리에 대한 설명

### ServiceComponent가 동작하는 Thread에 대해 설명

###Activity의 Window의 역할과 Instance가 Activity별 생성인지 여부

### Width와 MeasureWidth의 차이
Layout의 드로잉 과정 
* Animate 과정(animate)
* Measure 과정(requestLayout)
* Layout 과정(requestLayout)
* Draw 과정(Invalidate)

뷰의 기하는 사각형이다.
[(left, top), (right, bottom)] or [(left, top), (width, height)] 로 사각형을 정의한다.

Measured Width, Measured Height 는 뷰가 부모뷰 크기의 범위 내에서 가지고 싶어하는 너비와 높이이다.
Drawing Width, Drawing Height 는 뷰의 실제 너비와 높이로 뷰를 그리기 위해서 사용한다.
안드로이드에서는 이 Drawing Width와 Drawing Height를 width와 height로 표기한다.
따라서 Measured Width, Measured Height 는 Drawing Width, Drawing Height 와 다를 수 있다.
왜냐하면 뷰의 패딩, 마진 등을 고려하면 원하는 크기에서 패딩 및 마진 값을 빼야 하기 때문이다.

뷰의 정확한 위치와 크기는 언제 알 수 있는가?
안드로이드에서 뷰의 위치와 크기는 Layout 과정이 끝나야 정확히 계산된다.
이 Layout 과정은 여러번 호출 될 수 있다.
그렇기 때문에 Draw 과정이 시작되기 직전에 View의 정확한 위치와 크기를 알 수 있다.
위치 얻기 : getLeft(), getTop()
크기 얻기 : getWidth(), getHeight()
그렇다면 View의 Draw 과정이 시작되기 직전을 어떻게 알 수 있을까?
ViewTreeObserver 사용
뷰의 크기를 알고자 하는 뷰에서 getViewTreeObserver() 를 통해서 ViewTreeObserver를 가져온다
OnPreDrawListener 를 등록해서 드로잉 직전에 리스너가 호출 되도록 한다.
픽셀 단위의 뷰의 크기를 알 수 있다.