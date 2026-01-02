---
title: 个人信息管理系统-JavaWeb项目总结分析
date: 2020-10-07 17:57:54
tags:
  - Website
  - Code
cover: https://user-images.githubusercontent.com/60562661/109179168-96122900-77c4-11eb-80fd-1f9848fe0bb1.jpg
---

> 最近学习 `javaweb` 阶段 ，基本学习了原始的 `jsp` 开发，完成了一个比较综合的案例，记录一下各种操作的逻辑，以及具体的代码实现细节。

![](https://user-images.githubusercontent.com/60562661/95356015-c9791780-08f8-11eb-9e70-574262bbdd03.gif)

### 技术概览：

**前端** 页面采用 **原生**   `html `+ `css `+ `javascript` ;

**后端** 采用  **Java， Jsp**开发，具体包含原生 `servlet`，`request`，`response`；

**该系统主要包含功能**：

- 登录
- 显示用户信息
  - 分页显示
- 添加联系人
- 删除联系人：
  - 单条删除
  - 多选删除
  - 全选全部选
- 修改联系人；
- 根据条件查询联系人；

---



### 项目架构设计



![](https://user-images.githubusercontent.com/60562661/95356038-ced66200-08f8-11eb-8d0d-141a07eb8554.png)



如图，首先按web三层结构（ **浏览器 --> 服务器 --> 数据库 **）来分

-  **web 表示层**  ---  包括  控制器 **Servlet**  **Jsp页面**
- **业务逻辑层** --- 业务实现逻辑
- **数据访问层** --- 具体操作数据库

首先拿到前端页面，修改一下逻辑

---

### 功能实现



#### 登录 Login

-  `login.jsp` 表单提交到  `loginServlet` ;

```jsp
<form action="${pageContext.request.contextPath}/loginServlet" method="post">
```

- ` loginServlet`  逻辑
  - 验证码校验：

```java
// 获取填写的验证码值
String verifycode = request.getParameter("verifycode");
// 获取真实验证码值
HttpSession session = request.getSession();
String checkcode_server = (String) session.getAttribute("CHECKCODE_SERVER");
session.removeAttribute("CHECKCODE_SERVER");
//判断 验证码错误转发到该页面
// 转发仅在当前页面
if(!checkcode_server.equalsIgnoreCase(verifycode)){
    request.setAttribute("login_msg","验证码错误");
    request.getRequestDispatcher("/login.jsp").forward(request,response);
    return;
}
```

- 
  - 获取参数，封装User对象，
  - 传入 `service.login(user)`
  - 结果不为空，返回  `User`  对象，重定向到首页

  ```
  response.sendRedirect(request.getContextPath()+"/index.jsp");
  ```

  - 结果为空，设置错误信息，转发到当前页面

  ```java
  request.getRequestDispatcher("/login.jsp").forward(request,response);
  ```

-  `servlet.login`   数据库实现

```sql
String sql = "select * from user where username=? and password=?";
User loginUser = template.queryForObject(sql, new BeanPropertyRowMapper<User>(User.class), user.getUsername(), user.getPassword());
return user;
```



#### 添加联系人

- 添加联系人的页面  `add.jsp`  ，填写表单信息后提交到  `addInfoServlet` 



```html
<form action="${pageContext.request.contextPath}/addInfoServlet" method="post" id="form">
```



> 填写信息之后要进行表单校验，采用 js 实现：
>
> ```javascript
> window.onload = function () {
> 	function nameChecked() {
>                 var name = document.getElementById("name").value;
>                 var reg_name = /^[\u4e00-\u9fa5]{1,8}$/;
>                 var flag = reg_name.test(name);
>                 var block = document.getElementById("n_c");
>                 if (!flag) {
>                     block.innerHTML = "名字只能输入汉字哦！";
>                 }else {
>                     block.innerHTML = " ";
> 
>                 }
> 
>                 return flag;
>             }
>     document.getElementById("name").onblur = nameChecked;
>     document.getElementById("form").onsubmit = function () {
>                 return nameChecked();
>             }
> }
> ```



 `addInfoServlet`   逻辑

- 获取参数信息，封装对象

  ```java
  Map<String, String[]> infoMap = request.getParameterMap();
  ```

- 调用`service.addInfo(addUser)`  添加信息

- 重定向到展示信息页面

  ```java
  response.sendRedirect(request.getContextPath()+"/findUserByPageServlet");
  ```





service.addInfo(addUser)`  数据库操作

```java
String sql = "insert into user (name,gender,age,address,qq,email)  values " +
                "(?,?,?,?,?,?)";
template.update(sql, user.getName(), user.getGender(), user.getAge(), user.getAddress(), user.getQq(), user.getEmail());        
```



#### 删除联系人

- 单条信息删除，点击删除后跳转至 `deleteInfoServlet` ，并且通过后缀 `?id=${user.id}` 传入参数 

```jsp
<a href="${pageContext.request.contextPath}/deleteInfoServlet?id=${user.id}">删除</a>
```

- 根据**当前**`id` 删除该条信息

```java
String sql = "delete from user where id=?";
template.update(sql, id);
```

- 重定向到信息展示页面



#### 修改联系人信息

- 点击修改按钮，传入当前id，跳转至  `FindUserServlet`  

```jsp
<a class="btn btn-default btn-sm" href="${pageContext.request.contextPath}/FindUserServlet?id=${user.id}"> 修改 </a>
```

- 获取当前联系人信息记录，将`User`对象设置到域对象，转发到 `update.jsp` 文件中，在该文件中信息输入框设置 `value`属性，将设置的Usre信息回显
-  将  `update.jsp`  表单信息提交到  `updateInfoServlet`  ，在该servlet中，与上述逻辑类似，更新信息。



#### 分页显示信息

封装page对象返回给浏览器，具体包含：

```java
private int totalCount; // 总记录数
private int totalPage;  // 总页数
private List<T> list;   // 每页数据
private int currentPage; // 当前页数
private int rows; // 每页的数目
```

需要浏览器传给服务器 `currentPage ` 和 `rows`  参数

![image-20201007231426556](https://user-images.githubusercontent.com/60562661/95356011-c8e08100-08f8-11eb-9bd7-090d9e6639f4.png)

![image-20201007231724903](https://user-images.githubusercontent.com/60562661/95356003-c67e2700-08f8-11eb-8bc2-209bc3fa622f.png)



```java
@WebServlet("/findUserByPageServlet")
public class FindUserByPageServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        request.setCharacterEncoding("utf-8");


        String currentPage = request.getParameter("currentPage");
        String rows = request.getParameter("rows");

        if(currentPage == null || "".equals(currentPage) ){
            currentPage = "1";
        }

        if (rows==null || "".equalsIgnoreCase(rows)){
            rows = "7";
        }

        Map<String, String[]> conditions = request.getParameterMap();


        UserService service = new UserServiceImpl();
        PageBean<User> pageUsers =  service.findUserByPage(currentPage, rows, conditions);
//        System.out.println(pageUsers);
        request.setAttribute("pageUsers",pageUsers);
        request.setAttribute("condition",conditions);
        request.getRequestDispatcher("/list.jsp").forward(request,response);


    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}


```



```java
 public PageBean<User> findUserByPage(String _currentPage, String _rows, Map<String,String[]> condition) {

        int currentPage = Integer.parseInt(_currentPage);
        int rows = Integer.parseInt(_rows);

        if(currentPage<=0){
            currentPage = 1;
        }

        PageBean<User> page = new PageBean<>();

        page.setRows(rows);

        page.setCurrentPage(currentPage);


        int totalCount = dao.findTotalCount(condition);
        page.setTotalCount(totalCount);

        int start = (currentPage - 1) * rows;
        List<User> userList = dao.findUserByPage(start, rows, condition);
        page.setList(userList);

        int totalPage = totalCount % rows == 0 ? totalCount / rows : totalCount / rows + 1;
        page.setTotalPage(totalPage);

        return page;
    }
}
```



```java
 public int findTotalCount(Map<String, String[]> condition) {

        String sql = "select count(*) from user where 1=1 ";
        StringBuilder sb = new StringBuilder();
        sb.append(sql);

        List<Object> params = new ArrayList<Object>();

        for (String key : condition.keySet()) {

            if ("currentPage".equals(key) || "rows".equals(key)) {
                continue;
            }

            String value = condition.get(key)[0];
            if (value != null && !"".equals(value)) {
                sb.append(" and " + key + " like ? ");
                params.add("%" + value.replaceAll(" ","") + "%");
            }
        }
        return template.queryForObject(sb.toString(), Integer.class, params.toArray());
    }
```



```java
public List<User> findUserByPage(int start, int rows, Map<String, String[]> condition) {
    String sql = "select * from user where 1 = 1 ";
    StringBuilder sb = new StringBuilder();
    sb.append(sql);

    List<Object> params = new ArrayList<Object>();

    for (String key : condition.keySet()) {

        if ("currentPage".equals(key) || "rows".equals(key)) {
            continue;
        }

        String value = condition.get(key)[0];
        if (value != null && !"".equals(value)) {
            sb.append(" and " + key + " like ? ");
            params.add("%" + value.replaceAll(" ","")  + "%");
        }
    }
    params.add(start);
    params.add(rows);
    sb.append(" limit ?, ? ");
    List<User> userList = template.query(sb.toString(), new BeanPropertyRowMapper<User>(User.class), params.toArray());
    return userList;
}
```