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
>> 2.语法结构：execution(【权限修饰符】【返回类型】【类全路径】【方法名称】【参数列表】)
