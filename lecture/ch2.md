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
- 주요 지시자 <% %>
  - out.print(); -> <%= %>
<br>

<b>JSP 실행순서</b>
1. 브라우저가 웹서버에 JSP에 대한 요청 정보를 전달한다.
2. 브라우저가 요청한 JSP가 최초로 요청했을 경우만 JSP로 작성된 코드가 서블릿으로 코드로 변환한다. (java 파일 생성)
3. 서블릿 코드를 컴파일해서 실행가능한 bytecode로 변환한다. (class 파일 생성)
4. 서블릿 클래스를 로딩하고 인스턴스를 생성한다.
5. 서블릿이 실행되어 요청을 처리하고 응답 정보를 생성한다.

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