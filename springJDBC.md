### JdbcTemplate
|流程|图示|
|---|---|
|1.引入jar包|![image](https://user-images.githubusercontent.com/87599765/148723135-1f3673a2-7c48-4baa-b15e-b7fd6e5f99e9.png)|
|2.配置连接池并注入到创建的jdbcTemplate对象|![image](https://user-images.githubusercontent.com/87599765/148723247-9e128b80-2f08-4795-8666-94953ada7107.png)|
|3.创建BookDao接口|![image](https://user-images.githubusercontent.com/87599765/148723290-923813bf-8ca0-45e1-869c-47ffe5e86574.png)|
|4.创建BookDaoImpl实现类添加注解并注入jdbcTemplate|![image](https://user-images.githubusercontent.com/87599765/148723380-3de93789-c259-480a-bf91-454fe1693ae2.png)|
|5.创建BookService添加注解并将BookDao注入|![image](https://user-images.githubusercontent.com/87599765/148723424-262d7324-07bf-45e5-897c-4f8381dd1266.png)|
|6.配置组件扫描|![image](https://user-images.githubusercontent.com/87599765/148723483-4b087081-7d24-4996-9a3a-01f3fa95150c.png)|

###  
### Jdbc操作数据库--向t_book表添加数据
|流程|图示|
|---|---|
|1.BookService添加操作数据库方法|![image](https://user-images.githubusercontent.com/87599765/148727594-793526fb-fce8-47c7-a169-e3dc843f07e5.png)|
|2.BookDao接口添加对应的方法|![image](https://user-images.githubusercontent.com/87599765/148727644-538a05df-35e7-48f0-9e57-6e893e89b03b.png)|
|3.继承重写方法|![image](https://user-images.githubusercontent.com/87599765/148727718-49c47e65-2f12-4061-8644-9fb0f760eb5e.png)|
|4.测试|![image](https://user-images.githubusercontent.com/87599765/148727774-07854dcf-1802-477d-99d6-fbaa87fa9664.png)|
|问题解决|![image](https://user-images.githubusercontent.com/87599765/148727904-0ef71b70-83ec-4b17-94b9-d6cdc9098b52.png)![image](https://user-images.githubusercontent.com/87599765/148727953-b98b0829-6f60-4904-898b-c860bbada823.png)|

### Jdbc操作数据库--修改、删除数据、查询记录总数
|...|图示|
|---|---|
|1|![image](https://user-images.githubusercontent.com/87599765/148731691-7a501fea-56b8-4a06-b143-ec15bfee948b.png)|
|2|![image](https://user-images.githubusercontent.com/87599765/148731736-fb6f2a45-ac4b-45c0-b1ce-e1d6d7e2f8dd.png)|
|3|![image](https://user-images.githubusercontent.com/87599765/148731855-83201e82-0202-48e6-9430-61ba45cd60d8.png)|

### Jdbc查询返回对象
![image](https://user-images.githubusercontent.com/87599765/148777684-f01bc9e0-0fc0-4210-9cd5-90333f444d80.png)
> 详细流程  
### 
|...|图示|
|---|---|
|1.BookService|![image](https://user-images.githubusercontent.com/87599765/148779638-33b0f792-c7d6-4700-8c51-703dfa4e7d34.png)|
|2.BookDao|![image](https://user-images.githubusercontent.com/87599765/148779725-02eb7c82-5001-442f-a81a-93fbe8f31a40.png)|
|3.BookDaoImpl|![image](https://user-images.githubusercontent.com/87599765/148779848-2034a816-bea9-4c16-ad6b-fd20fe1cfb37.png)|
|4.test|![image](https://user-images.githubusercontent.com/87599765/148779963-960424e6-7bdf-4edf-8045-da1238d41793.png)|

### Jdbc查询返回集合
![image](https://user-images.githubusercontent.com/87599765/148778776-9129a1bc-3b03-43aa-bcb7-d8f688ffb8c0.png)
> 详细流程  
### 
|...|图示|
|---|---|
|1.BookService|![image](https://user-images.githubusercontent.com/87599765/148780088-6368e03a-a064-44c3-a715-5dee12294d1c.png)|
|2.BookDao|![image](https://user-images.githubusercontent.com/87599765/148780169-8760196e-943a-4080-9ba9-a28f120fd015.png)|
|3.BookDaoImpl|![image](https://user-images.githubusercontent.com/87599765/148780269-3f7fd9c4-7a69-4c70-be6b-5a7ad1ae34fb.png)|
|4.test|![image](https://user-images.githubusercontent.com/87599765/148780339-efc6c5f4-4571-4825-a851-4955b8a2c3de.png)|
