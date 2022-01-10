### JdbcTemplate
|流程|图示|
|---|---|
|1.引入jar包|![image](https://user-images.githubusercontent.com/87599765/148723135-1f3673a2-7c48-4baa-b15e-b7fd6e5f99e9.png)|
|2.配置连接池并注入到创建的jdbcTemplate对象|![image](https://user-images.githubusercontent.com/87599765/148723247-9e128b80-2f08-4795-8666-94953ada7107.png)|
|3.创建BookDao接口|![image](https://user-images.githubusercontent.com/87599765/148723290-923813bf-8ca0-45e1-869c-47ffe5e86574.png)|
|4.创建BookDaoImpl实现类添加注解并注入jdbcTemplate|![image](https://user-images.githubusercontent.com/87599765/148723380-3de93789-c259-480a-bf91-454fe1693ae2.png)|
|5.创建BookService添加注解并将BookDao注入|![image](https://user-images.githubusercontent.com/87599765/148723424-262d7324-07bf-45e5-897c-4f8381dd1266.png)|
|6.配置组件扫描|![image](https://user-images.githubusercontent.com/87599765/148723483-4b087081-7d24-4996-9a3a-01f3fa95150c.png)|

### Jdbc操作数据库--向t_book表添加数据
|流程|图示|
|---|---|
|1.BookService添加操作数据库方法|![image](https://user-images.githubusercontent.com/87599765/148727594-793526fb-fce8-47c7-a169-e3dc843f07e5.png)|
|2.BookDao接口添加对应的方法|![image](https://user-images.githubusercontent.com/87599765/148727644-538a05df-35e7-48f0-9e57-6e893e89b03b.png)|
|3.继承重写方法|![image](https://user-images.githubusercontent.com/87599765/148727718-49c47e65-2f12-4061-8644-9fb0f760eb5e.png)|
|4.测试|![image](https://user-images.githubusercontent.com/87599765/148727774-07854dcf-1802-477d-99d6-fbaa87fa9664.png)|
|问题解决|![image](https://user-images.githubusercontent.com/87599765/148727904-0ef71b70-83ec-4b17-94b9-d6cdc9098b52.png)![image](https://user-images.githubusercontent.com/87599765/148727953-b98b0829-6f60-4904-898b-c860bbada823.png)|
