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

#### FactoryBean
|...|图示|
|---|---|
|FactoryBean|![image](https://user-images.githubusercontent.com/87599765/148219554-db7cac40-5087-495b-b165-4538dfb08d8c.png)![image](https://user-images.githubusercontent.com/87599765/148219705-7ab81d86-859e-4830-bb83-f5d00d5238a5.png)|

#### bean作用域/生命周期
|bean作用域|图示|
|---|---|
|singleton--单实例对象|![image](https://user-images.githubusercontent.com/87599765/148221128-b5980aac-973b-427c-9980-930b7c92dad3.png)![image](https://user-images.githubusercontent.com/87599765/148221061-9e8f9d1d-dd9b-4bc3-8969-d6c03fe32f94.png)|
|prototype--多实例对象|![image](https://user-images.githubusercontent.com/87599765/148221233-0c948309-40d5-422e-885e-a442b273c60f.png)![image](https://user-images.githubusercontent.com/87599765/148221291-496939ee-8947-4bdc-b63c-e45574f0e0ad.png)|
|区别|![image](https://user-images.githubusercontent.com/87599765/148221478-ae5b00dd-afd8-4ee0-be97-943e26766640.png)|

|bean生命周期|图示|
|---|---|
|![image](https://user-images.githubusercontent.com/87599765/148224581-bb83d254-7796-4f34-b5b9-15d834d5e457.png)![image](https://user-images.githubusercontent.com/87599765/148224655-e01acbac-a852-45fb-9ecd-77511504bc52.png)|![image](https://user-images.githubusercontent.com/87599765/148224804-3d95ca81-64ed-412a-8030-e7679cee201c.png)![image](https://user-images.githubusercontent.com/87599765/148224849-bee991b6-f545-4165-85d5-4e2f047462c3.png)|
|完整生命周期|![image](https://user-images.githubusercontent.com/87599765/148225771-e27fc5a1-2ad2-4813-9468-4d41a0bd49c3.png)![image](https://user-images.githubusercontent.com/87599765/148226918-b21aa5c3-ef64-47bf-8aed-43a15f6de2cb.png)![image](https://user-images.githubusercontent.com/87599765/148226990-1a57b355-8596-442b-9580-22202f09dc25.png)![image](https://user-images.githubusercontent.com/87599765/148227032-57f596d8-d88e-4576-83e4-29dab87122b1.png)|

#### bean自动装配
|autowire|图示|
|---|---|
|![image](https://user-images.githubusercontent.com/87599765/148319340-21cef18e-8576-479b-894c-18d8b5e4bdbd.png)|![image](https://user-images.githubusercontent.com/87599765/148319400-b711d6cc-1597-4f69-b58c-1a6f12af596d.png)|
|![image](https://user-images.githubusercontent.com/87599765/148319447-f7d9c324-0b07-4082-b085-894d6386c9fd.png)|![image](https://user-images.githubusercontent.com/87599765/148319494-6b0d00a8-b431-4ca6-b8de-02957f69ffd5.png)|

#### bean引入外部属性文件--配置德鲁伊连接池连接mysql
|步骤|图示|
|---|---|
|引入名称空间|![image](https://user-images.githubusercontent.com/87599765/148411022-2bcb2835-ad0b-456d-b7ff-766e4d2bd065.png)|
|外部属性文件|![image](https://user-images.githubusercontent.com/87599765/148411104-2f92c658-d31d-4b5b-a55d-1ba36853b782.png)|
|直接连接xml文件配置|![image](https://user-images.githubusercontent.com/87599765/148411258-a0dfca7c-c0d7-44d4-aaa6-2163d4975595.png)|
|外部属性文件连接|![image](https://user-images.githubusercontent.com/87599765/148412633-e3d3979c-f12e-4f80-a4a8-9a183ad7f28d.png)|

#### 基于注解完成对象创建、属性注入
- spring里的组件扫描注解：@Component @Service @Contorller @Repository  
- spring里的属性注入注解：@AutoWired @Qualifier @Resource
![image](https://user-images.githubusercontent.com/87599765/148565011-dc1d2a28-1054-4f9c-9b20-a930d28bc4ce.png)

#### 
|完整步骤|图示|
|---|---|
|步骤1：引入aop jar包|![image](https://user-images.githubusercontent.com/87599765/148559601-f7d3be73-688b-4485-8f1a-df31608c4cf4.png)|
|步骤2：引入名称空间context|![image](https://user-images.githubusercontent.com/87599765/148560115-80f04106-d4cf-4d35-b422-b323b7805d03.png)|
|步骤3：加注解、扫描文件夹|![image](https://user-images.githubusercontent.com/87599765/148560500-2d5b3718-c256-414e-9d37-8b70a7b0f061.png)![image](https://user-images.githubusercontent.com/87599765/148560588-34565369-c1d2-412d-99f4-867a02ec2ef9.png)|
|步骤4：测试|![image](https://user-images.githubusercontent.com/87599765/148560637-3f52d2a8-a05b-4888-93f0-c0ce6f09e3f4.png)![image](https://user-images.githubusercontent.com/87599765/148560664-6e123a54-c28d-433f-9f64-e3649e244eda.png)|

####
|spring组件扫描细节|图示|
|---|---|
|设置扫描|![image](https://user-images.githubusercontent.com/87599765/148564218-a589383b-c72f-4087-8535-c13e054101f8.png)|
|设置不扫描|![image](https://user-images.githubusercontent.com/87599765/148564366-5e425d8a-5341-4a2d-be85-41ebdff53da6.png)|

####
|spring属性注入基于注解|图示|
|---|---|
|步骤1：创建UserDao、UserDaoImpl、UserService|![image](https://user-images.githubusercontent.com/87599765/148567919-10490502-6ed7-4807-8d48-83769cd16d83.png)|
|原来属性注入：|![image](https://user-images.githubusercontent.com/87599765/148568050-72138a64-1813-4378-be7f-36a7518e9fcf.png)|
|步骤2：接口实现类注解|![image](https://user-images.githubusercontent.com/87599765/148568149-e693a796-47d0-4356-9146-5571bdbe5105.png)|
|步骤3：service类组件扫描注解|![image](https://user-images.githubusercontent.com/87599765/148568280-cc306033-b177-4b39-8ee2-8f0ce6c5f53c.png)|
|步骤4：需要属性注入的对象进行注解|![image](https://user-images.githubusercontent.com/87599765/148568400-552f4d1f-bdde-411d-a031-00becf9ea9aa.png)|
|bean_annoProperty.xml|![image](https://user-images.githubusercontent.com/87599765/148568494-3bacc95f-38d9-45a8-9d62-5e5eaebe70e3.png)|

####
#### 指定属性注入的实现类--autowired配合qualifier使用
![image](https://user-images.githubusercontent.com/87599765/148569433-e9d171da-6e48-41ec-acba-178b4c088600.png)
