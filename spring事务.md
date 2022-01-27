### 事务概念
![image](https://user-images.githubusercontent.com/87599765/149301479-6b90c180-edcb-4475-91ec-98e973ad6e8c.png)

<br><br/>

### 事务操作环境搭建
|流程|图示|
|---|---|
|1.分析|![image](https://user-images.githubusercontent.com/87599765/149302380-1ab54dbf-3924-4461-a07b-e3b2d551f486.png)|
|2.事务操作|图示|
|2.1在spring配置文件配置事务管理器|![image](https://user-images.githubusercontent.com/87599765/149335941-df738a5c-18a9-4a62-9130-99d76b790c7f.png)|
|2.2引入tx名称空间|![image](https://user-images.githubusercontent.com/87599765/149336044-6ced4bfa-289d-402d-9995-0a257cc65433.png)|
|2.3开启事务注解|![image](https://user-images.githubusercontent.com/87599765/149336202-285fbdbb-692c-433a-ad38-d43110d9d94f.png)|
|3.添加事务注解（加到类上所有方法适用，加到方法上单个方法适用）|![image](https://user-images.githubusercontent.com/87599765/149336386-4e88cb29-d653-4684-8b45-3ecc6bae4498.png)|

<br><br/>

### 事务注解@Transactional()参数详解
|参数|图示|
|---|---|
|1.有哪些？|![image](https://user-images.githubusercontent.com/87599765/149338665-fcd6dbae-4456-44d6-a0cc-359be344e7bb.png)|
|2.propagation--事务传播行为|![image](https://user-images.githubusercontent.com/87599765/149338844-cc4bba4b-5f89-4e7c-8646-da0d5c8acff7.png)|
|3.isolation--事务隔离级别||
|4.timeout--超时时间|![image](https://user-images.githubusercontent.com/87599765/149359385-d544a283-9f71-4bb1-95fb-da025da40bc3.png)|
|5.readOnly--是否只读|![image](https://user-images.githubusercontent.com/87599765/149359721-60cb94ec-0c4c-499d-a106-6b59fcdd77b5.png)|
|6.rollbackFor--回滚|设置出现哪些异常进行回滚|
|7.noRollbackFor--不回滚|设置出现哪些异常不进行回滚|

- 脏读：一个未提交事务读取到另一个未提交事务的数据![image](https://user-images.githubusercontent.com/87599765/149356952-6c5c49d8-462f-49f5-b147-35f4b1234952.png)
- 不可重复读：一个未提交事务读取到另一提交事务修改数据![image](https://user-images.githubusercontent.com/87599765/149357962-ca1375b9-7963-4142-a88a-ec8e0483309f.png)
- 虚读：一个未提交事务读取另一提交事务添加数据
- 解决：通过设置事务隔离级别，解决读问题。![image](https://user-images.githubusercontent.com/87599765/149358657-cb78e24b-0eef-475d-a1a6-3634c1673b46.png)


|实现的功能|||
|---|---|---|
|项目构成|||
|步骤1|||
|步骤2|||
|步骤3|||
