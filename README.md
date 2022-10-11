# member_search
# 회원정보 조회하기
# 결과화면
![1](https://user-images.githubusercontent.com/104752580/195018349-7a44f061-41e7-409e-a5b1-16141a9e3e41.JPG)
![3](https://user-images.githubusercontent.com/104752580/195018361-95dc444f-2ab5-43f7-9173-adc3d4d7dd0a.JPG)
![2](https://user-images.githubusercontent.com/104752580/195018368-6a5a0eaf-5f21-4165-bde3-1d57c7d3e74b.JPG)
![4](https://user-images.githubusercontent.com/104752580/195018379-6fc71f18-42e1-41cb-a463-42cc74fae6f4.JPG)
# 코드설명
# member_search.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<script type="text/javascript">
function checkValue2() {
	if(!document.data1.in_custno.value){
		alert("회원번호를 입력하세요");
		data1.in_custno.focus();
		return false;
	}
	return true;
}
</script>
<meta charset="UTF-8">
<link rel="stylesheet" type="text/css" href="css/style.css?abc">
<title>Insert title here</title>
</head>
<body>
<header>
<jsp:include page="layout/header.jsp"></jsp:include>
</header>
<nav>
<jsp:include page="layout/nav.jsp"></jsp:include>
</nav>
<section class ="section">
<h2>회원조회</h2><br> 
<form name="data1" action="member_search_list.jsp" method = "post" onsubmit="return checkValue2()">
<table class="table_line">
<tr>
<th>회원번호</th>
<td><input type="text" name="in_custno" ></td>
</tr>
<tr class="center">
   <td  colspan="2" >
<input type="button" value="취소" onclick="location.href='index.jsp'">
<input type="submit" value="조회" >
</td>
</tr>
</table>
</form>
</section>
<footer>
<jsp:include page="layout/footer.jsp"></jsp:include>
</footer>
</body>
</html>
```
### form 태그 안에 테이블을 만들고 회원번호 name을 in_custno로 지정합니다. form 태그의 name은 data1로 지정하고 member_seach_list.jsp와 연결하고 onsubmit을 checkValue2로 지정합니다. script에는 회번호를 안적었을때 회원번호를 입력하세요 라는 문장이 뜨게 checkValue2 함수를 이용해서 유효성 검사를 합니다.
# member_search_list.jsp
```jsp
<%@ page import="java.sql.*" %>
<%@ page import="DB.DBConnect" %>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
 int in_custno = Integer.parseInt(request.getParameter("in_custno"));
 String sql="select custno, custname, phone, address, to_char(joindate,'yyyy-mm-dd')joindate,"
       +"case when grade ='A' then 'VIP' when grade ='B' then '일반' else '직원'end grade,"
       +"city from member_tbl_02 where custno =" + in_custno;
       
       Connection conn = DBConnect.getConnection();
       PreparedStatement pstmt = conn.prepareStatement(sql);
       ResultSet rs  = pstmt.executeQuery();
%>   
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<link rel="stylesheet" type="text/css" href="css/style.css?abc">
<title>Insert title here</title>
</head>
<body>
<header>
     <jsp:include page="layout/header.jsp"></jsp:include>
 </header>

 <nav>
       <jsp:include page="layout/nav.jsp"></jsp:include>
 </nav>
 
 <section class ="section">
 <h2>회원 조회 결과</h2><br>
 <%if(rs.next()) {%>
 <table class="table_line">
 <tr>
 <th>회원번호</th>
 <th>회원성명</th>
 <th>회원전화</th>
 <th>회원주소</th>
 <th>가입일자</th>
 <th>고객등급[A:VIP,B:일반,C:직원]</th>
 <th>도시코드</th>
 </tr>
 <tr class="center">
   <td><%= rs.getString("custno")%></td>
   <td><%= rs.getString("custname") %></td>
   <td><%= rs.getString("phone") %></td>
   <td><%= rs.getString("address") %></td>
   <td><%= rs.getString("joindate") %></td>
   <td><%= rs.getString("grade") %></td>
    <td><%= rs.getString("city") %></td>      
    </tr>
    <tr>
    <td colspan='7' align="center"> 
    <input type="button" value="홈으로" onclick="location.href='index.jsp'">
    </td>
    </tr>
 </table>
    <%}else{%>
   <p align="center">회원번호<%=in_custno %>의 회원정보가 없습니다.</p>
   <p align="center"><input type="button" value="다시 조회" onclick="location.href='member_search.jsp'"></p>
   <%} %>
 </section>
 <footer>
 <jsp:include page="layout/footer.jsp"></jsp:include>
 </footer>
</body>
</html>
```
### head 태그는 sql에서 select가져와 select문과 BD를 연결할 수 있게 해주었습니다. body 태그에서는 table을 if문으로 감싸고 테이블에 회원번호, 회원성명, 회원전화, 회원주소, 가입일자, 고객등급, 도시코드를 String 형태로 넣어줍니다. 그리고 회원번호가 틀리다면 그 번호의 회원번호가 없다는 것을 알려주고 다시 조회 버튼으로 다시 조회할 수 있게 해줍니다.
