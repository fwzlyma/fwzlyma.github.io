## AOP概念
![image](https://user-images.githubusercontent.com/87599765/148632873-63a5186c-96c3-4a33-9e25-ed36be830033.png)
![image](https://user-images.githubusercontent.com/87599765/148632822-7c91d1c2-db39-442c-aabe-09784b34dcc3.png)


## AOP底层原理
![image](https://user-images.githubusercontent.com/87599765/148633077-d01834bd-965c-47c5-adf2-07eb725b01d0.png)
![image](https://user-images.githubusercontent.com/87599765/148633088-663ebd78-f4c8-4219-80c9-109df18a42a3.png)

## AOP（JDK动态代理对象）
|代理创建过程|图示|
|---|---|
|创建接口|![image](https://user-images.githubusercontent.com/87599765/148634763-ec308478-6141-485e-b3b8-16c6945ffe2d.png)|
|创建接口实现类|![image](https://user-images.githubusercontent.com/87599765/148634768-0ac63579-8b2a-4bb2-a722-ceba880a8963.png)|
|创建代理对象|![image](https://user-images.githubusercontent.com/87599765/148634896-65c6683e-dfa5-4ffb-8237-720a3269289d.png)|
|结果演示|![image](https://user-images.githubusercontent.com/87599765/148634919-f3b7b214-348f-4239-937f-e9b3b0ce72e4.png)|

## AOP术语
![image](https://user-images.githubusercontent.com/87599765/148635098-3a117380-65e5-49d3-83f1-1c1e4368c1e6.png)

## AOP操作准备
1. AspectJ.独立于AOP框架，将AspectJ和Spring结合进行AOP操作。
2. 基于AspectJ实现AOP两种方式：（1）xml配置文件 （2）注解
3. 准备jar包  
![image](https://user-images.githubusercontent.com/87599765/148635471-bb50f0e4-b7f9-4b33-ae9d-460d74220b66.png)
4. 切入点表达式：知道对哪个类的哪个方法进行增强。
>> 1.切入点表达式作用:知道对哪个类的哪个方法进行增强  
>> 2.语法结构：execution(【权限修饰符】【返回类型】【类全路径】【方法名称】(【参数列表】))
![image](https://user-images.githubusercontent.com/87599765/148636140-96e485b3-6e6d-4a19-a97d-b1f7b2bee99b.png)
![image](https://user-images.githubusercontent.com/87599765/148636200-1a400c49-6fa5-42ef-ada0-e2a72adc4b86.png)

## AOP -- AspectJ注解
|...|图示|
|---|---|
|1.创建User类，添加组件扫描|![image](https://user-images.githubusercontent.com/87599765/148649379-70e0c06e-c4e3-44c0-9743-52fc9bfd64ed.png)|
|2.创建UserProxy代理对象类,添加组件扫描，添加生成代理对象|![image](https://user-images.githubusercontent.com/87599765/148649477-567c9274-2cbd-458b-91f0-a571f275bb9f.png)|
|3.创建bean.xml,添加名称空间context、aop，开启组件扫描、开启Aspect生成代理对象|![image](https://user-images.githubusercontent.com/87599765/148649565-55c8fe67-3fc0-42f2-8121-673d633673c9.png)|
|测试结果|![image](https://user-images.githubusercontent.com/87599765/148649579-0178a0b5-e72c-4bf4-90a2-3d465e8e758b.png)|
|异常时结果|![image](https://user-images.githubusercontent.com/87599765/148649606-84bab4ab-7f66-46bf-9f93-ad302c5767fc.png)|
|相同切入点抽取|![image](https://user-images.githubusercontent.com/87599765/148650042-eba84c67-57e3-4d2c-81ef-aff4139db0ad.png)|

> 多个代理对象执行，设置优先级：![image](https://user-images.githubusercontent.com/87599765/148650301-5c77c868-3641-40f8-ab29-d1ff913874e0.png)![image](https://user-images.githubusercontent.com/87599765/148650327-468b0544-9118-4433-ad86-8ea0f6e25c5b.png)

### AOP -- Aspect配置文件 （了解非重点）
|过程|图示|
|---|---|
|1.创建被增强类Book|![image](https://user-images.githubusercontent.com/87599765/148651038-77d30de5-8ffc-491b-abf2-ceb9c06bdf38.png)|
|2.创建增强类BookProxy|![image](https://user-images.githubusercontent.com/87599765/148651053-e3a7cabc-6ab5-40e2-bba9-612d475da465.png)|
|3.创建bean2.xml配置文件配置AOP|![image](https://user-images.githubusercontent.com/87599765/148651098-c27d67bf-54c4-44d4-96ed-49888d1b13df.png)|

## AOP -- 全注解开发
|...|图示|
|---|---|
|User.java|![image](https://user-images.githubusercontent.com/87599765/148651147-acd57e41-08b2-4746-8be2-6c4b1123f02c.png)|
|UserProxy.java|![image](https://user-images.githubusercontent.com/87599765/148651158-262d56a8-d2c6-4c93-b4fe-7d0badfb32cc.png)|
|AopConfig.java|![image](https://user-images.githubusercontent.com/87599765/148651179-dd6e567f-3d3e-476d-8c29-7763a1f3a0e5.png)|
|Test.java|![image](https://user-images.githubusercontent.com/87599765/148651210-7e34b08a-310c-4ee6-bf94-a0a334082a75.png)|
