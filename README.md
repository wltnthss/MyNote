# MyNote

> 개발하면서 헷갈렸던 개념, 자주 나오는 개념, 트러블슈팅 정리하고자 함.

# 트러블슈팅

**JSP web.xml 파일 &설정**

* JSP2.3 웹프로그래밍 책을 참고하면서 web.xml 파일을 설정하다가 밑에 해당하는 에러가 발생했다.

* org.xml.sax.SAXParseException; systemId: file:/D:/Workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/Chap20/WEB-INF/web.xml; lineNumber: 13; columnNumber: 82; "characterEncoding" 엔티티에 대한 참조는 ';' 구분자로 끝나야 합니다.

```java
// Before
jdbcUrl=jdbc:mysql://localhost:3306/guestbook?useUnicode=true&characterEncoding=utf8&useSSL=false&serverTimezone=UTC

// After
jdbcUrl=jdbc:mysql://localhost:3306/guestbook?useUnicode=true&amp;characterEncoding=utf8&amp;useSSL=false&amp;serverTimezone=UTC

& : &amp;
< : &lt;
> : &gt;
‘ : &apos;
” : &quot;
```

* 알고보니 web.xml에는 & 문자를 사용할 수 없다는 간단한 문제였다.
* web.xml에는 특수문자를 사용하지 못하니 & 은 &amp; 으로 적어주어야한다.
* 위의 특수기호들(&, >, <, ', ") 은 메모해두고 필요할 때 사용하자.

# CSS

**padding이 max-width 계산에 포함되지 않는 경우**

* padding은 내부 영역에만 적용되어 박스 모델의 너비 계산에는 포함되지 않습니다.
* 따라서, padding은 이와 별도로 고려해야합니다.

* input text가 max-width 를 해도 계속 범위에서 벗어나서 아래 명령어를 적어줬더니 정상 작동했다.
* box-sizing: border-box; 


# 디자인 패턴

* 디자인 패턴은 개발하면서 발생하는 반복적인 문제들을 OOP 4대 특성(캡슐화, 상속, 추상화, 다형성)과 SOLID 설계 원칙을 기반으로 구현되어있는 패턴들입니다.

**커맨드 패턴**

* 하나의 객체를 통해 여러 객체들에 명령을 할 때 사용하는 패턴입니다.
* 요청을 캡슐화함으로써 여러 기능을 실행할 수 있는 재사용성이 높은 클래스를 설계하는 패턴입니다.

**커맨드 패턴 예제**

* 새로운 텍스트 편집기 앱을 개발한다고 가정해보자.

* 다양한 대화 상자들의 일반 버튼들에 사용할 수 있는 Button 클래스를 생성했다.
* 가장 간단한 방법은 버튼이 사용되는 각 위치에 자식 클래스를 만드는 것이다.
* 하지만 이 방법은 Button 클래스를 수정할 때마다 자식 클래스들의 코드가 망가질 위험이 존재한다.
* 또한 여러 클래스가 같은 기능을 구현하므로 코드 리팩토링을 해야될 필요성이 생긴다.

**해결 방법**

* 이를 해결하기 위해서는 사용자 인터페이스와 비즈니스 로직사이에 Button 클래스에 커맨드 객체에 대한 참조를 저장하는 단일 필드를 넣은 후 클릭 될 때 이 커맨드를 시행하도록 하면 해결이 가능합니다.

> 단일 실행 메서드로 **커맨드 인터페이스를 선언**하여 작업을 호출하는 클래스들로부터 분리할 수 있습니다. (단일 책임 원칙)

> 기존 클라이언트 코드를 손상하지 않고 새 커맨드들을 도입할 수 있습니다. (개방/폐쇄 원칙)

**한 줄 설명**

> 즉, 커맨드 패턴은 Servlet내 Model 로직에서 공통으로 구현할 Handler interface를 선언함으로써 알맞은 로직 코드를 구현하고 사용할 정보를 저장한 다음에 결과를 보여줄 JSP URI를 리턴한다.  

