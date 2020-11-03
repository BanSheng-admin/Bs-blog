---
title: JavaWeb简易网上购物系统
date: 2020-10-29 20:33:43
tags:
categories: JavaWeb
comments: false
--- 
# JavaWeb简易网上购物系统
利用session传递来构造，于此记录一下源代码！
<!-- more -->
## src-com.my.bean Book.java
```java
public class Book {
    private int id; // 图书标识
    private String bookName;//图书名
    private String writer; //图书作者
    private int number;//数量
    private double price; //价格

    public Book() {
    }

    public String getBookName() {
        return bookName;
    }

    public void setBookName(String bookName) {
        this.bookName = bookName;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public int getNumber() {
        return number;
    }

    public void setNumber(int number) {
        this.number = number;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public String getWriter() {
        return writer;
    }

    public void setWriter(String writer) {
        this.writer = writer;
    }
}

```
## src-com.my.cart Cart.java
```java
import java.util.*;
public class Cart {
    private HashMap<Integer, Book> map;
    public Cart(){
        map = new HashMap<Integer, Book>();
    }
    //添加图书到购物车
    public void addCart(Book book){
        boolean res = map.containsKey(book.getId());//用来判断值是否存在
        if(res){
            int num = book.getNumber();//获取图书数量
            Book bk = map.get(book.getId());//获取book.getId的值
            bk.setNumber(bk.getNumber()+num);//设置bk图书数量
            map.put(book.getId(),bk);//存放
        }else{
            map.put(book.getId(),book);
        }
    }
    public void removeCart(Book book){
        boolean res = map.containsKey(book.getId());
        if(res){
            map.remove(book.getId());
        }
    }
    public void updateCart(Book book){
        boolean res = map.containsKey(book.getId());
        if(res){
            int num = book.getNumber();
            Book bk = map.get(book.getId());
            bk.setNumber(num);
            map.put(book.getId(),bk);
        }
    }
    public HashMap<Integer, Book> getCart() {
        return this.map;
    }
    public String showCart(){
        StringBuffer stf = new StringBuffer();
        if(map == null || map.size() == 0){
            stf.append("请购买图书!");
        }else{
            Collection<Book> c = map.values();
            Iterator<Book> iter = c.iterator();
            while(iter.hasNext()){
                Book book = iter.next();
                stf.append("序列号: " + book.getId() + "书名: " + book.getBookName() + "作者: " + book.getWriter() + "数量: " + book.getNumber() + "单价: " + book.getPrice()  + "<br>");
            }

        }
        return stf.toString();
    }
}
```
## web-book.jsp
```HTML
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>图书信息</title>
  </head> 
  
  <body>
   <h2 align="center">图书基本信息</h2>
   
   <table border="1"  align="center">
   <tr>
     <th>序号</th>
     <th>图书名</th>
     <th>图书作者</th>
     <th>图书价格</th>
     <th>图书数量</th> 
   </tr>
   <form action="cart.jsp?act=add"  method="post"> 
     <tr>
   
    <td><input type="hidden" name="id" value="1">1</td>
    <td><input type="hidden" name="bookName" value="JSP程序设计">JSP程序设计</td>
    <td><input type="hidden" name="writer" value="耿祥义">耿祥义</td>
    <td><input type="hidden" name="price" value="35.0">35.0</td>
    <td><input type="text" name="number" value="1"></td>
    <td><input type="submit" value="加入购物车" name="submit"></td> 
     </tr>
   </form>
   
   
    <form action="cart.jsp?act=add"  method="post">
      <tr>
   
       <td><input type="hidden" name="id" value="2">2</td>
       <td><input type="hidden" name="bookName" value="C语言程序设计">C语言程序设计</td>
       <td><input type="hidden" name="writer" value="谭浩强">谭浩强</td>
       <td><input type="hidden" name="price" value="38">38</td>
       <td><input type="text" name="number" value="1"></td>
       <td><input type="submit" value="加入购物车" name="submit"></td> 
     </tr>
  </form>
  
  <form action="cart.jsp?act=add"  method="post">
       <tr>
   
        <td><input type="hidden" name="id" value="3">3</td>
        <td><input type="hidden" name="bookName" value="Java 程序设计">Java程序设计</td>
        <td><input type="hidden" name="writer" value="王宣">王宣</td>
        <td><input type="hidden" name="price" value="30">30</td>
        <td><input type="text" name="number" value="1"></td>
        <td><input type="submit" value="加入购物车" name="submit"></td> 
      </tr>
   </form>
  
   <form action="cart.jsp?act=add"  method="post">
     <tr>
   
      <td><input type="hidden" name="id" value="4">4</td>
      <td><input type="hidden" name="bookName" value="UML基础">UML基础</td>
      <td><input type="hidden" name="writer" value="董婷">董婷</td>
      <td><input type="hidden" name="price" value="32">32</td>
      <td><input type="text" name="number" value="1"></td>
      <td><input type="submit" value="加入购物车" name="submit"></td> 
    </tr>
  </form>
  
  <form action="cart.jsp?act=add"  method="post">
    <tr>
   
     <td><input type="hidden" name="id" value="5">5</td>
     <td><input type="hidden" name="bookName" value="软件工程">软件工程</td>
     <td><input type="hidden" name="writer" value="李宣东">李宣东</td>
     <td><input type="hidden" name="price" value="48.5">48.5</td>
     <td><input type="text" name="number" value="1"></td>
     <td><input type="submit" value="加入购物车" name="submit"></td> 
    </tr>
  </form>  
 </table>
  
  </body>
</html>
```
## web-cart.jsp
```HTML
<html>
<head>
    <title>cart</title>
</head>
<body>
<%
    request.setCharacterEncoding("UTF-8");
    String act = request.getParameter("act");
    if (act == null) {
        act = "";
    }
    if ("add".equals(act)) {
        System.out.println("您现在进行添加商品到购物车中！");
        String idStr = request.getParameter("id");
        String bookName = request.getParameter("bookName");
        String writer = request.getParameter("writer");
        String priceStr = request.getParameter("price");
        String numberStr = request.getParameter("number");
        int id = Integer.parseInt(idStr);
        double price = Double.parseDouble(priceStr);
        int number = Integer.parseInt(numberStr);

        Book book = new Book();
        book.setId(id);
        book.setBookName(bookName);
        book.setNumber(number);
        book.setWriter(writer);
        book.setPrice(price);

        Cart cart = (Cart) session.getAttribute("cart");
        if (null == cart) {
            Cart cart1 = new Cart();
            cart1.addCart(book);
            session.setAttribute("cart", cart1);
        } else {
            cart.addCart(book);
            session.setAttribute("cart", cart);
        }
%>
        <jsp:forward page="cartMain.jsp"></jsp:forward>
<%
        } else if ("delete".equals(act)) {

        String idStr = request.getParameter("id");
        int id = Integer.parseInt(idStr);

        Book book = new Book();
        book.setId(id);

        Cart cart = (Cart) session.getAttribute("cart");
        cart.removeCart(book);
        session.setAttribute("cart", cart);
%>
<jsp:forward page="cartMain.jsp"></jsp:forward>

<%      } else if ("update".equals(act)) {

        String idStr = request.getParameter("id");
        int id = Integer.parseInt(idStr);

        String numStr = request.getParameter("number");
        int num = Integer.parseInt(numStr);

        Book book = new Book();
        book.setId(id);
        book.setNumber(num);
        Cart cart = (Cart) session.getAttribute("cart");
        cart.updateCart(book);

        session.setAttribute("cart", cart);

%>
<jsp:forward page="cartMain.jsp"></jsp:forward>

<%
    }
%>
</body>
</html>
```
## web-cartMain.jsp
```HTML
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>购物车</title>
  </head>   
  
  <body>
    <h2 align="center">您的购物车的图书</h2>
    <table border="1"  align="center" width="70%"  >
     <tr>  
       <th>图书名</th>
       <th>图书作者</th>
       <th>图书价格</th>
       <th>图书数量</th> 
     </tr>     
   
   <%
       request.setCharacterEncoding("UTF-8");
       Cart cart=(Cart)session.getAttribute("cart");
       if(cart!=null && cart.getCart().size()>0)
       {
          //购物车不是空的
          HashMap<Integer,Book> map=cart.getCart();
          Collection<Book> c= map.values();
			Iterator<Book> iter=c.iterator();
			while(iter.hasNext())
			{
             Book book=iter.next();
    %>
   
      <tr>
       <form action="cart.jsp?act=update&&id=<%=book.getId() %>" method="post">
         <td><%=book.getBookName()%></td>
         <td><%=book.getWriter()%></td>
         <td><%=book.getPrice()%></td>
         <td><input type="text" name="number" value=<%=book.getNumber()%>></td>
         
         <td><a href="cart.jsp?act=delete&&id=<%=book.getId()%>">删除</a>
         <td><input type="submit" value="修改数量" ></td>
          
      </form>
      </tr> 
    
    <%                  
          }    
       }
       else
       {
           //购物车是空的        
            out.println("<h3 align='center'><font color='red'>您还没有购书呢！</font></h3>");       
       }   
    %>   
   </table>   
   <h3 align="center"><a href="book.jsp">继续购物</a>
                      <a href="item.jsp">生成订单</a>
   </h3>   
  </body>
</html>
```
## web-item.jsp
```HTML
<html>
<head>
    <title>item</title>
</head>
<body>
<%
    request.setCharacterEncoding("UTF-8");
    Cart cart = (Cart)session.getAttribute("cart");
    if(cart == null){
        out.print("请购买图书!");
    }else{
        out.print(cart.showCart());
    }
%>
</body>
</html>
```