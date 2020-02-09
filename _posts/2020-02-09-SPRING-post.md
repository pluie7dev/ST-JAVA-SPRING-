
-------------------------------------------------
3. 리스트 페이지 작성 - DriverManagerDataSource 


-----------------------
<1> JNDI를 활용한 리스트 페이지 작성

jstl 라이브러리 : tomcat /example/WEB-INF/lib/ 2개 라이브러리 -> 프로젝트에 복사


-----------
ex 1) list.jsp
<%@ taglib prifix="c" uri="http://java.sun.com/jsp/jstl/core" %>


<table border = "1">
  <tr>
    <th>번호</th><th>제목</th><th>등록자</th><th>등록일</th>
  </tr>
  
<c:forEach var="vo" items="${boardList}" delims="">
  <tr>
  <td>${vo.seq}</td><td>${vo.title}</td><td>${vo.writer}</td><td>${vo.regdate}</tc>
  </tr>
</c:forEach>
  </table>

-----------  
boardList 라는 리스트 객체를 가져와서 뷰(jsp)에서 
forEach로 반복하여 출력한다 
ex 1) 예제는 JNDI 방식을 사용 

-----------------------


-----------------------
<2> JDBC를 활용한 리스트 페이지 작성 

springboard-servlet.xml(예제) 
에서 객체를 생성한다. xml에 등록하는 과정이 곧
객체를 생성하는 과정

1) bean 클래스 생성(bean 객체)

-----------
ex 1) springboard-servlet.xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" .../>

<bean id="dataSource" class>
  </bean>
  
  <!-- Controller --> 
  <bean name="/board.list.do" class="board.controller.BoardListController">
  <property name="boardDao" ref="boardDao"/>
  </bean>
  
  <!-- DAO -->
  <bean id="boardDao" class="board.dao.BoardDaoImpl">
  <property name="jdbcTemplate">
    <ref bean="springJdbcTemplate"/>
  </property>
  </bean>

-----------

  