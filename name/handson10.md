### what i learnt
- adding New todo
- make it vissible in table
- using jstl tags arranging it as table

### Needed dependency

```
 <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
        </dependency>
```

# needed import

```
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
```

### listfile

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<html>

<head>
<title>your Todos</title>
</head>

<body>
<H1>Todos</H1>
<table>
<caption>your todos</caption>
<thead> 
<tr>
<th>desc</th>
<th>targetDate</th>
<th>isDone</th>
</tr>
</thead>
<%-- --%> <tbody>
<c:forEach items="${todos}" var="x">
<tr>
<td>${x.desc}</td>
<td>${x.targetDate}</td>
<%-- --%><td>${x.done}</td>
</tr>
</c:forEach>
</tbody>
 
</table>
<BR/>
<a href="todo">click here</a>
</form>
</body>
</html>
```
