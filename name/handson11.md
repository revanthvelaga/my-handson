### what i learnt

- adding boot strap for formating data
- deleting added todo

### todo controller
```java
package com.createmaveen.project.controller;

import java.util.Date;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.ModelMap;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.SessionAttributes;

import com.createmaveen.project.service.TodoService;


@Controller
@SessionAttributes("name")
public class Todocontroller {
	
	@Autowired
	TodoService service;
	
	@RequestMapping(value="/list-todos", method = RequestMethod.GET)
	public String showTodos(ModelMap model){
		String name = (String) model.get("name");
		//model.put("todos", service.retrieveTodos("in28Minutes"));
		model.put("todos", service.retrieveTodos(name));
		return "list-todos";
	}
	@RequestMapping(value="/todo", method = RequestMethod.GET)
	public String showAddTodoPage(ModelMap model){
		return "todo";
	}
	@RequestMapping(value="/todo", method = RequestMethod.POST)
	public String addTodo(ModelMap model, @RequestParam String desc){
		service.addTodo((String) model.get("name"), desc, new Date(), false);
		return "redirect:/list-todos";
	}
	@RequestMapping(value="/delete-todo", method = RequestMethod.GET)
	public String deleteTodo(@RequestParam int id){
		service.deleteTodo(id);
		return "redirect:/list-todos";
	}
}
```

### list-todoss
```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<html>

<head>
<title>your Todos</title>
<link href="webjars/bootstrap/3.3.6/css/bootstrap.min.css"
	    		rel="stylesheet">

</head>

<body>
<div class="container">
<H1>Todos</H1>
<table class="table table-striped">

<thead> 
<tr>
<th>desc</th>
<th>targetDate</th>
<th>isDone</th>
<th>Delete</th>
</tr>
</thead>
<%-- --%> <tbody>
<c:forEach items="${todos}" var="x">
<tr>
<td>${x.desc}</td>
<td>${x.targetDate}</td>
<%-- --%><td>${x.done}</td>
<td><a type="button" class= "btn btn-warning" href="/delete-todo?id=${x.id}">Delete </a></td>
</tr>
</c:forEach>
</tbody>
 
</table>

<div><a class="button" href="todo">click here</a></div>
</form>

<script src="webjars/jquery/1.9.1/jquery.min.js"></script>
 <script src="webjars/bootstrap/3.3.6/js/bootstrap.min.js"></script>
 </div>
</body>
</html>
```
