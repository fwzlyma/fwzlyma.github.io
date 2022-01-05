## 内容简介
![image](https://user-images.githubusercontent.com/87599765/148055211-b84b5fb8-7dac-4683-bc0b-7e0015b63866.png)

## spring框架概述
![image](https://user-images.githubusercontent.com/87599765/148056091-00b823dd-2a61-4244-8b7a-3178af54cb27.png)

## 入门案例
![image](https://user-images.githubusercontent.com/87599765/148057236-f99f57b4-cc94-4ac6-a514-7267c32ad6ab.png)
- [下载地址](https://repo.spring.io/ui/native/release/org/springframework/spring/)
- 版本号：5.2.6 下载*dist.zip
1. 打开idea 创建一个普通的java工程 java-> helloworld
2. 导入相关jar包 如图:
![image](https://user-images.githubusercontent.com/87599765/148059636-fec013ec-dd0d-489e-97d4-cb1f9a42c094.png)
3. 创建一个普通类，在类里创建一个普通的方法
![image](https://user-images.githubusercontent.com/87599765/148061344-bd36247a-7ca3-487d-84c6-007055fca232.png)
#### spring对象创建
![image](https://user-images.githubusercontent.com/87599765/148061694-33146b6c-515c-4e8d-b4b8-157a376c0518.png)
#### spring测试
![image](https://user-images.githubusercontent.com/87599765/148065055-789c4abd-7ab3-4a91-86a7-86a787de8c78.png)

## IOC容器
(1)IOC底层原理--将耦合度降到最低  
![image](https://user-images.githubusercontent.com/87599765/148066534-0deadf45-d854-4836-a994-894bc6d619d3.png)  
![image](https://user-images.githubusercontent.com/87599765/148067225-be056d47-bb8b-4cb8-bf0d-50a61e5784ac.png)  
![image](https://user-images.githubusercontent.com/87599765/148068650-77cd9fa1-e930-4e20-977a-7e4326f3542b.png)  
- ApplicationContext接口有实现类  
![image](https://user-images.githubusercontent.com/87599765/148069142-28a8723d-19b4-40b6-850f-cc2a60f0d824.png)  
(2)IOC接口(BeanFactory)--解耦  
(3)IOC操作Bean管理(基于xml)  
(4)IOC操作Bean管理(基于注解)  
### IOC 操作Bean管理
1. 什么是Bean管理
- Bean管理指的是两个操作
- Spring创建对象
- Spring注入属性
2. 实现方式
- xml
- 注解
#### 基于xml方式创建对象
![image](https://user-images.githubusercontent.com/87599765/148070079-e4e8a43d-997f-4af0-a56c-f603978b54bd.png)
#### 属性注入
|方式|图示|
|---|---|
|set方法注入|![image](https://user-images.githubusercontent.com/87599765/148168986-50fe7c53-fdf5-4575-ae61-3530289372db.png)|
|有参构造方法注入|![image](https://user-images.githubusercontent.com/87599765/148169068-4cfc2b1a-ad0b-4695-8813-f4647df6866f.png)|
|p命名空间--set注入|![image](https://user-images.githubusercontent.com/87599765/148169191-dd758af5-6ce8-4cd0-8714-4b74245658f7.png)|

#### 注入特殊值
|特殊值|图示|
|---|---|
|null|![image](https://user-images.githubusercontent.com/87599765/148170042-3aae35e1-a4dd-4d74-a409-ca6e5ae12111.png)|
|<<南京>>|![image](https://user-images.githubusercontent.com/87599765/148170256-1ba3f7ed-e032-4a85-a82d-5662dda4aea0.png)|

#### 注入外部bean
|注入属性--外部bean|图示|
|---|---|
|给userService中的userDao注入接口实现类|![image](https://user-images.githubusercontent.com/87599765/148173397-9d422bf8-12b8-4314-8f4c-8bb50cfdf414.png)![image](https://user-images.githubusercontent.com/87599765/148173524-1ea9bf2f-d9a0-4818-a01d-738a3a22b990.png)|

#### 注入内部bean/级联赋值
|注入方法|图示|
|---|---|
|注入内部bean|![image](https://user-images.githubusercontent.com/87599765/148176158-30cd5b22-1acd-4094-8f1f-07e67d156ef8.png)![image](https://user-images.githubusercontent.com/87599765/148176271-a8919c00-8b7a-4ac6-a6e5-e2a44d920754.png)|
|注入外部bean、特殊符号|![image](https://user-images.githubusercontent.com/87599765/148177811-db2e8ed2-fb41-4279-95fd-312f1cde1ccc.png)|
|级联赋值|![image](https://user-images.githubusercontent.com/87599765/148178903-1735ac38-fff1-4de0-b78c-d49d53039a3b.png)![image](https://user-images.githubusercontent.com/87599765/148179098-cfbd3da2-64cd-432d-8489-96d87b920a18.png)|

#### 集合类型属性注入
|集合|图示|
|---|---|
|数组|![image](https://user-images.githubusercontent.com/87599765/148197699-7799932a-6534-42e7-b7ca-88eceb08d41a.png)|
|list|![image](https://user-images.githubusercontent.com/87599765/148197776-dc47a6bf-4f0e-4567-b16c-96a1b7ee3479.png)|
|map|![image](https://user-images.githubusercontent.com/87599765/148197890-3066e400-b5d4-43d7-9047-bf8108c9fc53.png)|
|set|![image](https://user-images.githubusercontent.com/87599765/148197953-7be8d3e6-d154-43ed-a62a-0b4ec0792ace.png)|
|补充：数组输出为字符串|![image](https://user-images.githubusercontent.com/87599765/148198077-10cca770-5494-467a-a77f-28d5e786a28f.png)|
|集合类型注入对象|![image](https://user-images.githubusercontent.com/87599765/148203103-f373e1a2-265f-4946-9d57-c97f7e55710e.png)|
|提取注入部分--公共使用,需要引入util名称空间|![image](https://user-images.githubusercontent.com/87599765/148203316-d0f0d02d-9b2b-4401-99fd-983792a50de8.png)![image](https://user-images.githubusercontent.com/87599765/148203410-04354c93-1c83-4c94-bc5d-86b585a74a1c.png)|
