
```
--- 
1. WEB_MVC 관련 클래스 정리 

Spring -> MVC 컨테이너

서블릿
웹프로그래밍에서 클라이언트의 요청을 처리하고 그 결과를 다시 클라이언트에게 
전송하는 Servlet 클래스의 구현 규칙을 지킨 자바 프로그래밍 기술

---

WEB_MVC 관련 클래스 종류

1) Dispatcher-Servlet
  (org.springframework.web.servlet.DispatcherServlet)
Servlet Container에서 HTTP프로토콜을 통해 들어오는 모든 요청을 프레젠테이션 
계층의 제일앞에 둬서 중앙집중식으로 처리해주는 프론트 컨트롤러(Front Controller)

2) HandlerMapping(org.springframework.web.servlet.handler)
Dispatcher-Servlet은 클라이언트의 요청이 들어오면 해당 요청을 처리할 컨트롤러를
구현하기 위해 HandlerMapping을 이용
 (1) BeanNameUrlHandlerMapping (default)
 (2) SimpleUrlHandlerMapping
 
3) Controller(org.springframework.web.servlet.mvc)
 (1) Controller(interface)
 (2) AbstractController
 (3) AbstractCommandController
 (4) SimpleFormController
 
4) ViewResolver(org.springframework.web.servlet.view)
 (1) InternalResourceViewResolver (default)
 (2) ResourceBundleViewResolver
 (3) velocity.VelocityViewResolver
 
5) View(jsp/org.springframework.web.servlet.view)
 (1) InternalResourceView (default)
 (2) JstlView
 (3) VelocityView
 
 
 * Dispatcher-Servlet을 통해 HandlerMapping, ViewResolver는 자동으로(default) 
   생성되는 객체. 사용자는 Controller만 비즈니스 로직으로 구현한다
   

---
<1> JNDI를 활용한 리스트 페이지 작성

jstl 라이브러리 : tomcat /example/WEB-INF/lib/ 2개 라이브러리 -> 프로젝트에 복사


---
ex 1) list.jsp

```
