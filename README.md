# member_search
# 회원정보 조회하기
# 결과화면
![1](https://user-images.githubusercontent.com/104752580/195018349-7a44f061-41e7-409e-a5b1-16141a9e3e41.JPG)
![3](https://user-images.githubusercontent.com/104752580/195018361-95dc444f-2ab5-43f7-9173-adc3d4d7dd0a.JPG)
![2](https://user-images.githubusercontent.com/104752580/195018368-6a5a0eaf-5f21-4165-bde3-1d57c7d3e74b.JPG)
![4](https://user-images.githubusercontent.com/104752580/195018379-6fc71f18-42e1-41cb-a463-42cc74fae6f4.JPG)
# 코드설명(member_search.jsp, member_search_list.jsp)
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
