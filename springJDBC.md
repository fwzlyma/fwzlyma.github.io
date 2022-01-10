### JdbcTemplate
|流程|图示|
|---|---|
|1.引入jar包|![image](https://user-images.githubusercontent.com/87599765/148723135-1f3673a2-7c48-4baa-b15e-b7fd6e5f99e9.png)|
|2.配置连接池并注入到创建的jdbcTemplate对象|![image](https://user-images.githubusercontent.com/87599765/148723247-9e128b80-2f08-4795-8666-94953ada7107.png)|
|3.创建BookDao接口|![image](https://user-images.githubusercontent.com/87599765/148723290-923813bf-8ca0-45e1-869c-47ffe5e86574.png)|
|4.创建BookDaoImpl实现类添加注解并注入jdbcTemplate|![image](https://user-images.githubusercontent.com/87599765/148723380-3de93789-c259-480a-bf91-454fe1693ae2.png)|
|5.创建BookService添加注解并将BookDao注入|![image](https://user-images.githubusercontent.com/87599765/148723424-262d7324-07bf-45e5-897c-4f8381dd1266.png)|
|6.配置组件扫描|![image](https://user-images.githubusercontent.com/87599765/148723483-4b087081-7d24-4996-9a3a-01f3fa95150c.png)|
