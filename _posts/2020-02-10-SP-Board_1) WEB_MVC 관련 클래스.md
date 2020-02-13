
```
--- 
1. WEB_MVC 관련 클래스

Spring -> MVC 컨테이너

서블릿
웹프로그래밍에서 클라이언트의 요청을 처리하고 그 결과를 
다시 클라이언트에게 전송하는 Servlet 클래스의 구현 
규칙을 지킨 자바 프로그래밍 기술

---

WEB_MVC 관련 클래스 종류

1) Dispatcher-Servlet
(org.springframework.web.servlet.DispatcherServlet)
Servlet Container에서 HTTP프로토콜을 통해 들어오는 
모든 요청을 프레젠테이션 계층의 제일앞에 둬서 중앙
집중식으로 처리해주는 프론트 컨트롤러

2) HandlerMapping
(org.springframework.web.servlet.handler)
Dispatcher-Servlet은 클라이언트의 요청이 들어오면
해당 요청을 처리할 컨트롤러를 구현하기 위해 
HandlerMapping 이용
 (1) BeanNameUrlHandlerMapping (default)
 (2) SimpleUrlHandlerMapping
 
3) Controller(org.springframework.web.servlet.mvc)
 (1) Controller(interface)
 (2) AbstractController
 (3) AbstractCommandController
 (4) SimpleFormController
 
4) ViewResolver(org.springframework.web.servlet.view)
컨트롤러를 통해 db작업등의 결과를 ModelAndView로 가져오면
Dispatcher-Servlet은 ViewResolver에게 해당 객체를 
보여줄 view를 찾도록 요청 
 (1) InternalResourceViewResolver (default)
 (2) ResourceBundleViewResolver
 (3) velocity.VelocityViewResolver
 
5) View(jsp/org.springframework.web.servlet.view)
 (1) InternalResourceView (default)
 (2) JstlView
 (3) VelocityView
 
 
 * Dispatcher-Servlet을 통해 HandlerMapping, 
   ViewResolver는 자동으로(default) 생성되는 객체
   사용자는 Controller만 비즈니스 로직으로 구현한다
   
---

JDBC 
1) 절차 
  (1) db와 연결   : DataSource
  (2) 명령문 실행 : JdbcTemplate
  (3) 결과를 수신 : RowMapper
  
2) DataSource
  (1) org.springframework.jdbc.datasource.DriverManagerDataSource
  (2) org.springframework.jndi.JndiObjectFactoryBean
  
3) JdbcTemplate
  (1) org.springframework.jdbc.core.JdbcTemplate
      - query(), update()
  (2) org.springframework.jdbc.core.support.JdbcDaoSupport
      - getConnection(), getJdbcTemplate()
      
4) RowMapper(org.springframework.jdbc.core)
  (1) Callback Interface
  
5) ResultSetExtractor

---
게시판 기본 프로젝트 테스트 파일 구성
1) view : index.html/list.jsp

2) obj  
web.xml
  -servlet class(DispatcherServlet)
  -servlet mapping(*.do)
springboard-servlet.xml
  -bean(.do class)
  -DAO
  
3) controller 
BoardListContorller.java
  -implements Controller
  -ModelAnView
  -HttpServletRequest/Response
  
4) DAO(interface), DAOImpl(class), DTO

5) server.xml(db 접속설정)

---

---
1) view : list.jsp
<%@ taglib prifix="c" uri="http://java.sun.com/
jsp/jstl/core" %>

<table border = "1">
  <tr>
    <th>번호</th><th>제목</th><th>등록자</th>
    <th>등록일</th>
  </tr>
  
<c:forEach var="vo" items="${boardList}" delims="">
  <tr>
  <td>${vo.seq}</td><td>${vo.title}</td><td>
  ${vo.writer}</td><td
  ${vo.regdate}</tc>
  </tr>
</c:forEach>
  </table>
  
2) obj 
web.xml


springboard-servlet.xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/
schema/beans" .../>

<bean id="dataSource" 
class="org.springframework.jdbc.datasource.
DriverManagerDataSource">
<property name="driverClassName" 
value="oracle.jdbc.driver.OracleDriver"/>
<property name="url" 
value="jdbc:oracle:thin:@localhost:1521:orcl"/>
<property name="username" value="scott"/>
<property name="password" value="a1234"/>
  
</bean>
  
<!-- Controller --> 
<bean name="/board.list.do" 
class="board.controller.BoardListController">
<property name="boardDao" ref="boardDao"/>
</bean>
  
<!-- DAO -->
<bean id="boardDao" class="board.dao.BoardDaoImpl">
<property name="jdbcTemplate">
 <ref bean="springJdbcTemplate"/>
</property>
</bean>

3) controller : BoardListContorller.java
public class BoardListController implements Controller {

 @Override
 public ModelAndView handleRequest(HttpServletRequest arg0,
 HttpservletResponse arg1) throws Exception{
 
  ModelAndview mav = new ModelAndView();
  mav.setViewName("WEB-INF/jsp/list.jsp");
  
  return mav;
  }
}

4) -DAO(interface)
public class BoardDaoImpl implements BoardDao{
 public List list();
  }
 
   -DAOImpl(class)
 public class BoardDaoImpl implements BoardDao{
 private JdbcTemplate jdbctemplate;
 
 public void setJdebcTemplate(JdbcTemplate jdbcTemplate){
  this.jdbcTempalte = jdbcTempalte;
 }
  
 @Override
 public List list(){
   String sql = "select * from tblSpringboard order by seq desc";
   
   jdbcTemplate.query(sql, result); 
   return null;
 }   
 
   -DTO(class)
 public class BoardDto{   
   private int seq;
   private String title;
   private String content;
   private String writer;
   private String regdate;  
   
   ... 
   
   public String getWriter() {
      return writer;
   }
   
   public String setWriter(String writer) {
      this.writer = writer;
   }
   
   ... 
 
 }
   
   
    
 
5) server.xml(db 접속설정)
<Resource name="jdbc/SpringDB"
 auth="Container"
 type="javax.sql.DataSource"
 username="scott"
 password="a1111"
 driverClassname="oracle.jdbc.driver.OracleDriver"
 url="jdbc:oracle:thin:@localhost:1521:orcl"
 maxActive="8"
 maxIdle="4"/>
 
 
}

```
