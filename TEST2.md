

\\<!--

2. 글보기 페이지 작성_1 - 페이지 이동 기능 
(링크 URI 활용)

(process)
-> 글 리스트 페이지(list.jsp) 
-> 각 리스트별 글(상세보기) uri 선택(board_detail.do)
-> 글 상세보기 페이지 표시(detail.jsp)

(task)
<1> 기존 리스트 페이지에서 uri 추가(list.jsp)
<2> 리스트 페이지에서 uri로 이동한 상세 글보기 페이지(detail_view.jsp)
<3> bean 클래스 추가생성(bean 객체/springboard-servlet.xml)

-->

---


\\<!--
<1> 기존 리스트 페이지에서 uri 추가

ex 1) list.jsp
<%@ taglib prifix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<table border = "1">
  <tr>
    <th>번호</th><th>제목</th><th>등록자</th><th>등록일</th>
  </tr>
  
<c:forEach var="vo" items="${boardList}">
  <tr>
  <td>${vo.seq}</td>
  <td><a href="board_detail.do?"seq=${vo.seq}">${vo.title}</a></td> //링크처리
  <td>${vo.writer}</td>
  <td>${vo.regdate}</tc>
  </tr>
</c:forEach>
  </table>
-->
