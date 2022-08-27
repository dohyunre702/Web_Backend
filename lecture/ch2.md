## 2 웹 백엔드 프로그래밍 기초

### 1. Web 개발의 이해
브라우저에 'Hello World'가 출력되는 원리
1. 사용자가 웹 브라우저를 통해 웹 어플리케이션에 접근하여, 인터넷을 통해 WAS에게 요청을 전달한다.
2. WAS는 요청받은 url의 mapping값에 해당하는 doget()메소드를 실행한다.
3. WAS는 요청된 정보를 브라우저에 전달한다.

http://localhost:8080/{프로젝트명}/{url mapping값}

1. java의 웹 어플리케이션 : 네이버 블로그 등

### 3. 서블릿(Servlet)
- WAS에 동작하는 JAVA 클래스
- HttpServlet 클래스를 상속받아야 함
- 웹페이지를 개발할 때 JSP와 서블릿을 조화롭게 사용해야 함
- EX. 웹페이지를 구성하는 화면(HTML)은 JSP로 표현하고, 복잡한 프로그래밍은 서블릿으로 구현
** 동적 페이지는 요청이 들어왔을 때, 서블릿이 실행되면서 응답할 코드를 만들어내고 그 때 그 코드로 응답을 하게 하는 것이다 (데이터 가져오는 것이 기준)
- 어노테이션 = 마크업 시스템
- / web.xml

<br><b>요청과 응답</b><br>
- 웹 브라우저가 요청정보에 담아서 보내는 header값을 읽어들여 브라우저 화면에 출력

<br>WAS는 웹 브라우저로부터 Servlet요청을 받으면,
- 요청할 때 가지고 있는 정보를 HttpServletRequest객체를 생성하여 저장
- 웹 브라우저에게 응답을 보낼 때 사용하기 위하여 HttpServletResponse객체를 생성
- 생성된 HttpServletRequest, HttpServletResponse 객체를 서블릿에게 전달

HttpServletRequest
- http프로토콜의 request정보를 서블릿에게 전달하기 위한 목적으로 사용
- 헤더정보, 파라미터, 쿠키, URI, URL 등의 정보를 읽어 들이는 메소드를 가지고 있음
- Body의 Stream을 읽어 들이는 메소드를 가지고 있음

HttpServletResponse
- WAS는 어떤 클라이언트가 요청을 보냈는지 알고 있고, 해당 클라이언트에게 응답을 보내기 위한 HttpServletResponse객체를 생성하여 서블릿에 전달
- 서블릿은 해당 객체를 이용해 content type, 응답코드, 응답 메시지 등 전송

* contentPath : web application이 mapping된 path
<br><br>

### 4. JSP
- JSP(JavaServer Page) : 마이크로소프트의 ASP에 대항하기 위해 만든 스크립트 언어
- 마이크로소프트에서 ASP(Active Server Page)라는 쉽게 웹을 개발할 수 있는 스크립트(script) 엔진을 발표함 (1998년)
- 1997년에 발표된 서블릿은 ASP에 비하여 상대적으로 개발 방식이 불편함
- ASP에 대항하기 위하여 1999년 썬마이크로시스템즈에서 JSP를 발표
- <b>모든 JSP는 서블릿으로 변환된 후 동작. 서블릿과 똑같은 라이프사이클로 실행된다.</b>
<br>

<b>JSP 실행순서</b>
1. 브라우저가 웹서버에 JSP에 대한 요청 정보를 전달한다.
2. 브라우저가 요청한 JSP가 최초로 요청했을 경우만 JSP로 작성된 코드가 서블릿으로 코드로 변환한다. (java 파일 생성)
3. 서블릿 코드를 컴파일해서 실행가능한 bytecode로 변환한다. (class 파일 생성)
4. 서블릿 클래스를 로딩하고 인스턴스를 생성한다.
5. 서블릿이 실행되어 요청을 처리하고 응답 정보를 생성한다.
<BR><BR>

<b>3가지 스크립트 요소</b>
  - 선언문(Declaration) - <%! %> : JSP페이지 내에서 필요한 전역변수 선언 및 메소드 선언에 사용
  - 스크립트릿(Scriptlet) - <% %> : 프로그래밍 코드 기술에 사용
  - 표현식(Expression) - <%= 문장 %> : 화면에 출력할 내용 기술에 사용. 출력할 부분은 내장객체인 out 객체의 print() 또는 println() 메소드를 사용해서 출력 (out.print(); -> <%= %>)
<br>
<b>주석(Comment)</b>
- JSP페이지에서 사용할 수 있는 주석 : HTML주석, 자바주석, JSP주석
- HTML주석 - <!-- --> : HTML주석을 사용한 페이지를 웹에서 서비스할 때는 표시되지 않으나, [소스보기]를 수행하면 HTML 주석의 내용이 화면에 표시
- JSP주석 - <%-- --%> : 해당 페이지를 웹 브라우저를 통해 출력 결과로서 표시하거나, 웹브라우저 상에서 소스보기를 해도 표시되지 않음. 또한 JSP주석 내에 실행코드를 넣어도 그 코드는 실행되지 않음
- JAVA주석 - <//, /* */> : 스트립트릿이나 선언문에서 사용되는 주석으로, 자바와 주석처리 방법이 같음
<BR><br>
<b>내장 객체</b><br>
- 개발자가 선언하지 않아도 사용할 수 있는 미리 선언된 변수
- JSP를 실행하면 서블릿 소스가 생성되고 실행된다.
- JSP에 입력한 대부분의 코드는 생성되는 서블릿 소스의 _jspService() 메소드 안에 삽입되는 코드로 생성된다.
- _jspService()에 삽입된 코드의 윗부분에 미리 선언된 객체들이 있는데, 해당 객체들은 jsp에서도 사용 가능하다.
- response, request, application, session, out과 같은 변수를 내장객체라고 한다.

<br><br>
### 5. Scope
  - <i>참고 링크 : http://www.javajee.com/application-request-session-and-page-scopes-in-servlets-and-jsps </i>
- Scope : 변수의 유효 범위. 해당 변수가 접근할 수 있는 변수, 객체 그리고 함수의 집합
- 4가지 Scope : Application, Session, Request, Page
  - Application : 웹 어플리케이션이 시작되고 종료될 때까지 변수가 유지되는 경우 사용
  - Session : 웹 브라우저 별로 변수가 관리되는 경우 사용
  - Request : http요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수가 유지되는 경우 사용
  - Page : 페이지 내에서 지역변수처럼 사용

1) page scope : 특정 서블릿이나 JSP가 실행되는 동안에만 정보를 유지 하고 싶을 때
- PageContext 추상 클래스를 사용한다.
- JSP 페이지에서 pageContext라는 내장 객체로 사용 가능 하다.
- forward가 될 경우 해당 Page scope에 지정된 변수는 사용할 수 없다.
- 사용방법은 Application scope나 Session scope, request scope와 같다.
- 마치 지역변수처럼 사용된다는 것이 다른 Scope들과 다릅니다.
- jsp에서 pageScope에 값을 저장한 후 해당 값을 EL표기법 등에서 사용할 때 사용됩니다.
- 지역 변수처럼 해당 jsp나 서블릿이 실행되는 동안에만 정보를 유지하고자 할 때 사용됩니다.

2) request scope : 웹 브라우저로부터 WAS가 요청을 받은 후, 포워드되는 동안 유지하고 싶은 정보가 있을 때
- http 요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수값을 유지하고자 할 경우 사용한다.
- HttpServletRequest 객체를 사용한다.
- JSP에서는 request 내장 변수를 사용한다.
- 서블릿에서는 HttpServletRequest 객체를 사용한다.
- 값을 저장할 때는 request 객체의 setAttribute()메소드를 사용한다.
- 값을 읽어 들일 때는 request 객체의 getAttribute()메소드를 사용한다.
- forward 시 값을 유지하고자 사용한다.
- 앞에서 forward에 대하여 배울 때 forward 하기 전에 request 객체의 setAttribute() 메소드로 값을 설정한 후, 서블릿이나 jsp에게 결과를 전달하여 값을 출력하도록 하였는데 이렇게 포워드 되는 동안 값이 유지되는 것이 Request scope를 이용했다고 한다.
 
3) session scope : 접속한 웹 브라우저별로 정보를 관리 하고 싶을 때
- 웹 브라우저별로 변수를 관리하고자 할 경우 사용한다.
- 웹 브라우저간의 탭 간에는 세션정보가 공유되기 때문에, 각각의 탭에서는 같은 세션정보를 사용할 수 있다.
- HttpSession 인터페이스를 구현한 객체를 사용한다.
- JSP에서는 session 내장 변수를 사용한다.
- 서블릿에서는 HttpServletRequest의 getSession()메소드를 이용하여 session 객체를 얻는다.
- 값을 저장할 때는 session 객체의 setAttribute()메소드를 사용한다.
- 값을 읽어 들일 때는 session 객체의 getAttribute()메소드를 사용한다.
- 장바구니처럼 사용자별로 유지가 되어야 할 정보가 있을 때 사용한다.

4) application scope : 하나의 웹 어플리케이션에서 공유하고 싶은 변수가 있을 때
- 웹 어플리케이션이 시작되고 종료될 때까지 변수를 사용할 수 있다.
- ServletContext 인터페이스를 구현한 객체를 사용한다.
- jsp에서는 application 내장 객체를 이용한다.
- 서블릿의 경우는 getServletContext()메소드를 이용하여 application객체를 이용한다.
- 웹 어플리케이션 하나당 하나의 application객체가 사용된다.
- 값을 저장할 때는 application객체의 setAttribute()메소드를 사용한다.
- 값을 읽어 들일 때는 application객체의 getAttribute()메소드를 사용한다.
- 모든 클라이언트가 공통으로 사용해야 할 값들이 있을 때 사용한다.
  
<br><br>
## 실습 과정에서 마주한 오류
- The selection cannot be run on any server <br>
ㄴ 해결방법 : project 우클릭 > properties > server > <None>을 Tomcat v9.0 Server at localhost로 변경<br><br>
- [404 error] Origin 서버가 대상 리소스를 위한 현재의 representation을 찾지 못했거나, 그것이 존재하는지를 밝히려 하지 않습니다.
ㄴ 해결방법 : 톰캣 서버탭 > 하단부 Modules > edit > path를 /root만 남기고 모두 지워 줌.

<BR><BR>
### 느낀 점
자바 서블렛으로 하는 웹브라우저 개발이 약간 약간 옛날 웹페이지.. 그니까 html5로 html이랑 블로그 페이지 꾸미는 확장판이라는 생각이 들고 있는데..
기본 틀은 비슷한데 이제 컴퓨터에서 제대로 돌아갈 수 있게끔 여러 개의 프로그램이 필요하다! 정도로 이해하였음
+ 일단 객체지향까지만 제대로 이해되면 그 다음부터는 레고 조립이고 그걸 효과적으로 지원해 주는 여러 기술들에 숙달되면 됨
