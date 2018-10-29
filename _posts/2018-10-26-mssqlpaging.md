---
layout: post
title: "MSSQL 페이징 쿼리"
tags: [ etc, mssql, pagingquery ]
date: 2018-10-26
categories: [ etc ]
---

<p align="center">
    데이터의 양이 많을 때 페이지 하단에 페이지번호를 처리하는것을 <font color="deeppink">Pagination</font>이라고 한다.<br/>
    mssql에서는 이 페이징을 처리할 수 있는 sql구문을 지원해준다.
</p><br/>

# mssql 페이징 쿼리
ex) 데이터가 20개씩 묶여있는 2페이지의 데이터 출력

{% highlight ruby %}
DECLARE @RowsPerPage INT = 20, @PageNumber INT = 2
SELECT *
FROM 테이블
WHERE 조건
ORDER BY 순서
OFFSET (@PageNumber-1)*@RowsPerPage ROWS
FETCH NEXT @RowsPerPage ROWS ONLY
{% endhighlight %}

### 한페이지가 가지고 있을 데이터의 개수와 페이지 지정
맨위 구문인 DECLARE @RowsPerPage INT = 20, @PageNumber INT = 2에서 <font color="orange">@RowperPage INT=N</font>가 의미하는 것은 한페이지에서 보여줄 <font color="orange">데이터의 개수</font>를 지정하는 것이며, <font color="orange">@PageNumber INT = N</font>가 의미하는 것은 지정한 데이터만큼의 페이지를 나눌때의 <font color="orange">해당 보여줄 페이지</font>를 의미한다.
<br/>
<hr/>