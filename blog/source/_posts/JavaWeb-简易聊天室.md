---
title: JavaWeb简易聊天室
date: 2020-11-03 10:43:43
tags:
categories: JavaWeb
comments: false
--- 
# JavaWeb简易聊天室
利用session,application
<!-- more -->
## chat.jsp
```HTML
<center>
    <h3>简易聊天室</h3>
    <textarea rows="10" cols="40" name="tt">
        <%
            Object chats = application.getAttribute("chat");
            List<String> chatList = null;
            if(null == chats){
                chatList = new ArrayList<String>();
            }else{
                chatList = (List<String>)chats;
            }
            if(chatList.size() == 0){
                out.print("还没有人聊天");
            }else {
                for(int i = 0;i < chatList.size();i++){
                    out.print(chatList.get(i) + "\n");
                }
            }
        %>
    </textarea>
    <br><br>
    <form action="chatDo.jsp">
        <input type="text" name="words">
        <input type="submit" name="sub" value="提交">
        <input type="reset" name="rec" value="取消">
    </form>
</center>
```
## chatdo.jsp
```jsp
<%
    //1.获取应用对象中聊天列表:chatList
    Object chats = application.getAttribute("chat");
    List<String> chatList = null;
    if(null == chats){
        chatList = new ArrayList<String>();
    }else{
        chatList = (List<String>)chats;
    }
    //2.获取表单聊天信息
    String words = request.getParameter("words");
    //3.获取会话中用户的姓名
    String userName = (String)session.getAttribute("userName");
    //4.构建聊天信息:  姓名+words+时间
    DateFormat f = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
    Date d = new Date();
    String time = f.format(d);
    words = userName + ":" + words + " " + time;
    //5.将words加入聊天列表中
    chatList.add(words);
    //6.将聊天列表放入application中
    application.setAttribute("chat",chatList);
    //7.返回聊天页面
    response.sendRedirect("chat.jsp");
%>
```
## login.jsp
```HTML
<center>
		<h3>用户登录</h3>
		<form action="loginDo.jsp">
			<p>
				账号:<input type="text" name="userName" />
			<p>
			<p>
				密码:<input type="password" name="password" />
			<p>	
				<input type="submit" value="提交" /> <input type="reset" value="取消" />
		</form>
	</center>
```
## loginDo.jsp
```HTML
<%
		//获取登录信息
		String userName = request.getParameter("userName");
		String password = request.getParameter("password");

		//中文处理

		if (userName.equals("") || password.equals("")) {
			//返回登录页面
			response.sendRedirect("login.jsp");
		} else {
			session.setAttribute("userName", userName);
			//返回到聊天室中
			response.sendRedirect("chat.jsp");
		}
	%>
```