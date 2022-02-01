课程介绍

1. spring概念
2. IOC容器
3. Aop
4. JdbcTemplate
5. 事务管理
6. Spring5新特性

# spring概念

1. spring是轻量级的开源的JavaEE框架

2. spring可以解决企业应用开发的复杂性

3. spring有两个核心部分：IOC和Aop

- IOC:控制反转，把创建对象过程交给spring进行管理
- Aop:面向切面，不修改源代码进行功能增强

4. spring特点

   （1）方便解耦，简化开发

   （2）Aop编程支持

   （3）方便程序测试

   （4）可以和其他框架进行整合

   （5）方便进行事务操作

   （6）降低API开发难度

## 入门案例

1.[下载spring5](https://repo.spring.io/ui/native/release/org/springframework/spring/)

- 使用5.2.6稳定版本
- ![](E:\notes\images\spring-release.jpg)

- 解压后：

  ![](E:\notes\images\spring-5.2.6-release.png)

2.打开idea工具，创建普通工程

<img src="E:\notes\images\入门案例_1.png" style="zoom: 50%;" />

> 输入项目名字

<img src="E:\notes\images\入门案例_2.png" style="zoom:50%;" />

3.所需jar包导入

| jar包导入   | 图示                                                         |
| ----------- | ------------------------------------------------------------ |
| 需要的jar包 | ![](E:\notes\images\入门案例_jar包.png)                      |
| 导入步骤    | 1.项目创建一个lib文件夹                                      |
|             | 2.将jar包复制到文件夹                                        |
|             | 3.![](E:\notes\images\入门案例_3.png)                        |
|             | 4.<img src="E:\notes\images\入门案例_4.png" style="zoom:50%;" /> |

4.创建一个普通的类，在这个类创建一个普通的方法

<img src="E:\notes\images\入门案例_5.png" style="zoom:50%;" />

5.创建spring配置文件，在里面

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--配置User对象创建-->
    <bean id="user" class="com.fwzlym.spring5.User">
    </bean>
        
</beans>
```

6.进行测试

```java
public class TestSpring5 {

    @Test
    public void testUser() {
        //1.加载spring配置文件
        ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        //2.获取配置创建的对象
        User user = context.getBean("user", User.class);
        user.sayHello();
    }
}
```

# IOC容器

1. IOC底层原理
2. IOC接口(BeanFactory)
3. IOC操作Bean管理--xml方式
4. IOC操作Bean管理--注解方式

## IOC概念和原理

1. 什么是IOC

   （1）控制反转，把对象创建和对象之间的调用过程，交给spring管理

   （2）使用IOC目的：为了降低耦合度

   （3）做入门案例就是IOC实现

2. IOC底层原理

   （1）xml解析、工厂模式、反射

3. 画图讲解IOC底层原理

   | IOC原理  |                                                           |
   | -------- | --------------------------------------------------------- |
   | 原始方式 | <img src="E:\notes\images\IOC_1.png" style="zoom:67%;" /> |
   | 工厂模式 | <img src="E:\notes\images\IOC_2.png" style="zoom:67%;" /> |
   | IOC过程  | ![](E:\notes\images\Snipaste_2022-01-27_14-03-59.png)     |
   |          | ![](E:\notes\images\Snipaste_2022-01-27_14-05-53.png)     |
   |          |                                                           |

[^原始方式]: 耦合度高
[^工厂模式]: 解耦，但是耦合度仍没有降到最低
[^IOC]: 进一步降低耦合度！

## IOC（接口）

1. IOC思想基于IOC容器完成，IOC容器底层就是对象工厂

2. Spring提供IOC容器实现两种方式：（两个接口）

   - BeanFactory:IOC容器基本实现，是spring内部的使用接口，不提供开发人员使用

     > 加载xml配置文件时，不会创建对象，获取的时候才创建

   - **ApplicationContext**:BeanFactory接口的子接口，提供更多更强大的功能，一般由开发人员使用

     > 加载配置文件时候就会创建，好处是耗时耗资源的东西先创建。

3. ApplicationContext接口有实现类：

![](E:\notes\images\Snipaste_2022-01-27_14-20-09.png)

## IOC操作Bean管理

1. 什么是Bean管理
   - spring创建对象
   - spring注入属性
2. Bean管理操作有两种实现方式
   - 基于xml配置文件方式实现
   - 基于注解方式实现

### IOC操作Bean管理（基于xml方式）

1. 基于xml方式创建对象

   ```xml
   <!--配置User对象创建-->
       <bean id="user" class="com.fwzlym.spring5.User">
       </bean>
   ```

   | bean属性介绍 |                                      |
   | ------------ | ------------------------------------ |
   | id           | 对象别名，唯一标识                   |
   | class        | 创建对象的类所在的全路径（包类路径） |
   | *name        | 早期属性，与id一样                   |

   > 创建对象的时候，默认执行对象的类的无参数构造方法

2. 基于xml方式注入属性

   1. DI：依赖注入，就是注入属性

      | 注入属性    | 说明                               | 图示                                                  |
      | ----------- | ---------------------------------- | ----------------------------------------------------- |
      | 原始方式    | 1.set方法注入                      | ![](E:\notes\images\Snipaste_2022-01-27_14-54-39.png) |
      |             | 2.有参构造方法注入                 | ![](E:\notes\images\Snipaste_2022-01-27_14-56-21.png) |
      | **xml方式** | 1.set方法注入：设置好属性的set方法 | ![](E:\notes\images\Snipaste_2022-01-27_15-08-12.png) |
      |             |                                    | ![](E:\notes\images\Snipaste_2022-01-27_15-10-03.png) |
      |             |                                    | ![](E:\notes\images\Snipaste_2022-01-27_15-13-23.png) |
      |             | 2.有参构造进行注入                 | ![](E:\notes\images\Snipaste_2022-01-27_15-19-23.png) |
      |             |                                    | ![](E:\notes\images\Snipaste_2022-01-27_15-24-33.png) |
      |             |                                    | ![](E:\notes\images\Snipaste_2022-01-27_15-27-03.png) |

   2. *p名称空间注入--简化基于xml配置方式

      | p名称空间注入（了解一点） |                                                       |
      | ------------------------- | ----------------------------------------------------- |
      | 1.配置文件添加p名称空间   | ![](E:\notes\images\Snipaste_2022-01-27_15-41-00.png) |
      | 2.属性注入                | ![](E:\notes\images\Snipaste_2022-01-27_15-43-22.png) |

### IOC操作Bean管理（xml注入其他类型属性）

1. 字面量

   - null值

     ```xml
     	<!--IOC set方法注入属性 注入空值-->
         <bean id="book" class="com.fwzlym.spring5.Book">
             <property name="bname" value="赌侠"></property>
             <property name="bauthor" value="周星驰"></property>
             <property name="address">
                 <null></null>
             </property>
         </bean>
     ```

   - 特殊符号

     ![](E:\notes\images\Snipaste_2022-01-27_15-56-30.png)

2. 注入属性--外部bean

   - 先创建service类和dao类

     UserService.java

     ```java
     public class UserService {
         public void add() {
             System.out.println("service add ......");
         }
     }
     ```

     UserDao.interface

     ```java
     public interface UserDao {
         public void update();
     }
     ```

     UserDaoImpl.java

     ```java
     public class UserDaoImpl implements UserDao{
         @Override
         public void update() {
             System.out.println("userDaoImpl update ......");
         }
     }
     ```

   - **现在想在service里调用dao的方法**

     | service调dao方法 | 图示                                                      |
     | ---------------- | --------------------------------------------------------- |
     | 1.原始方式       | ![](E:\notes\images\Snipaste_2022-01-27_17-13-54.png)     |
     | 2.外部bean       | ![](E:\notes\images\Snipaste_2022-01-27_17-21-29.png)     |
     |                  | 测试![](E:\notes\images\Snipaste_2022-01-27_17-33-51.png) |

3. 注入属性--内部bean和级联赋值

   1. 一对多关系：部门和员工

      > 一个部门有多个员工，一个员工属于一个部门；部门是一，员工是多。

   2. 在实体类之间表示一对多关系

      > 部门类Dept.java

      ```java
      public class Dept {
          private String dname;
      
          public void setDname(String dname) {
              this.dname = dname;
          }
      
          @Override
          public String toString() {
              return dname;
          }
      }
      ```

      > 员工类Emp.java

      ```java
      public class Emp {
          private String ename;
          private String gender;
          //员工属于某一个部门--用对象形式表示
          private Dept dept;
      
          public void setEname(String ename) {
              this.ename = ename;
          }
      
          public void setGender(String gender) {
              this.gender = gender;
          }
      
          public void setDept(Dept dept) {
              this.dept = dept;
          }
      
          @Override
          public String toString() {
              return "Emp{" +
                      "ename='" + ename + '\'' +
                      ", gender='" + gender + '\'' +
                      ", dept=" + dept +
                      '}';
          }
      }
      ```

   3. 在配置文件中实现内部bean

      ```xml
      <bean id="emp" class="com.fwzlym.spring5.bean.Emp">
          <property name="ename" value="张若昀"></property>
          <property name="gender" value="男"></property>
          <!--内部bean注入对象-->
          <property name="dept">
              <bean id="dept" class="com.fwzlym.spring5.bean.Dept">
                  <property name="dname" value="安保部"></property>
              </bean>
          </property>
      </bean>
      ```

   4. 注入属性--级联赋值

      > 1.级联赋值：感觉就是外部bean啊~

      ```xml
      <bean id="emp" class="com.fwzlym.spring5.bean.Emp">
          <property name="ename" value="徐凤年"></property>
          <property name="gender" value="男"></property>
          <!--级联赋值-->
          <property name="dept" ref="dept"></property>
      </bean>
      <bean id="dept" class="com.fwzlym.spring5.bean.Dept">
          <property name="dname">
              <value><![CDATA[<<雪中悍刀行>>]]></value>
          </property>
      </bean>
      ```

      > 测试结果

      ![](E:\notes\images\Snipaste_2022-01-27_18-04-26.png)

      > 2.第二种写法--需要对象所在的类里创建getter方法，否则报错！

      ```xml
       <bean id="emp" class="com.fwzlym.spring5.bean.Emp">
           <property name="ename" value="徐凤年"></property>
           <property name="gender" value="男"></property>
           <!--级联赋值-->
           <property name="dept" ref="dept"></property>
           <property name="dept.dname" value="技术部"></property>
      </bean>
      <bean id="dept" class="com.fwzlym.spring5.bean.Dept"></bean>
      ```

### IOC操作Bean管理（xml注入集合属性）

1. 注入数组类型属性

2. 注入List集合类型属性

3. 注入Map集合类型属性

   1. 创建类，定义数组、List、map、set类型属性，并且生成对应setter方法。

      ```java
      public class Stu {
          //1.数组类型属性
          private String[] courses;
          //2.list集合类型属性
          private List<String> homeworkList;
          //3.map集合类型属性
          private Map<String, String> maps;
          //4.set集合类型属性
          private Set<String> set;
      
          public void setSet(Set<String> set) {
              this.set = set;
          }
      
          public void setHomeworkList(List<String> homeworkList) {
              this.homeworkList = homeworkList;
          }
      
          public void setMaps(Map<String, String> maps) {
              this.maps = maps;
          }
      
          public void setCourses(String[] courses) {
              this.courses = courses;
          }
      
          @Override
          public String toString() {
              return "Stu{" +
                      "courses=" + Arrays.toString(courses) +
                      ", homeworkList=" + homeworkList +
                      ", maps=" + maps +
                      ", set=" + set +
                      '}';
          }
      }
      ```

   2. 在spring配置文件进行配置完成集合类型属性注入

      > 代码总览

      ```xml
      <bean id="stu" class="com.fwzlym.spring5.collectiontype.Stu">
          <!--数组类型属性注入-->
          <property name="courses">
              <array>
                  <value>java课程</value>
                  <value>数据库</value>
                  <value>javaWeb</value>
              </array>
              <!--等价-->
              <!--<list>
                      <value>java课程</value>
                      <value>数据库</value>
                      <value>javaWeb</value>
                  </list>-->
          </property>
          <!--list类型属性注入-->
          <property name="homeworkList">
              <list>
                  <value>计算机网络</value>
                  <value>数据结构</value>
                  <value>科技论文写作</value>
              </list>
          </property>
          <!--map类型属性注入-->
          <property name="map">
              <map>
                  <entry key="JAVA" value="java"></entry>
                  <entry key="PHP" value="php"></entry>
              </map>
          </property>
          <!--set类型属性注入-->
          <property name="set">
              <set>
                  <value>MySQL</value>
                  <value>Redis</value>
                  <value>Redis</value>
              </set>
          </property>
      </bean>
      ```

      

      | 集合类型属性注入   | 图示                                                  |
      | ------------------ | ----------------------------------------------------- |
      | 1.数组类型属性注入 | ![](E:\notes\images\Snipaste_2022-01-27_18-31-53.png) |
      | 2.list类型属性注入 | ![](E:\notes\images\Snipaste_2022-01-27_18-32-43.png) |
      | 3.map类型属性注入  | ![](E:\notes\images\Snipaste_2022-01-27_18-33-57.png) |
      | 4.set类型属性注入  | ![](E:\notes\images\Snipaste_2022-01-27_18-35-12.png) |

   3. 以user与computer举例 -- **集合 + 对象** 如何注入属性？

      > User.java

      ```java
      public class User {
          private String uid;
      
          public void setUid(String uid) {
              this.uid = uid;
          }
      
          @Override
          public String toString() {
              return "User{" +
                      "uid='" + uid + '\'' +
                      '}';
          }
      }
      ```

      > Computer.java

      ```java
      public class Computer {
          private String cname;
      
          public void setCname(String cname) {
              this.cname = cname;
          }
      
          @Override
          public String toString() {
              return "Computer{" +
                      "cname='" + cname + '\'' +
                      '}';
          }
      }
      ```

      > Relation.java

      ```java
      public class Relation {
      	//定义用户与电脑一对一关系的map
          private Map<User, Computer> map;
      
          public void setMap(Map<User, Computer> map) {
              this.map = map;
          }
      
          @Override
          public String toString() {
              return "Relation{" +
                      "map=" + map +
                      '}';
          }
      }
      ```

      > xml配置

      ```xml
      <bean id="relation" class="com.fwzlym.spring5.collectiontype.Relation">
          <property name="map">
              <map>
                  <entry key-ref="user1" value-ref="com1"></entry>
                  <entry key-ref="user2" value-ref="com2"></entry>
              </map>
          </property>
      </bean>
      <!--用户与电脑对象创建-->
      <bean id="user1" class="com.fwzlym.spring5.collectiontype.User">
          <property name="uid" value="2017***112"></property>
      </bean>
      <bean id="com1" class="com.fwzlym.spring5.collectiontype.Computer">
          <property name="cname" value="神舟战神"></property>
      </bean>
      <bean id="user2" class="com.fwzlym.spring5.collectiontype.User">
          <property name="uid" value="2021***67"></property>
      </bean>
      <bean id="com2" class="com.fwzlym.spring5.collectiontype.Computer">
          <property name="cname" value="联想拯救者"></property>
      </bean>
      ```

      > 测试输出

      ![](E:\notes\images\Snipaste_2022-01-27_18-58-40.png)

      其他集合只需使用<ref bean=""></ref>即可完成属性注入。

   4. **提取**公共集合部分

      > 以Book为例

      ```java
      public class Book {
          private List<String> list;
      
          public void setList(List<String> list) {
              this.list = list;
          }
      
          @Override
          public String toString() {
              return "Book{" +
                      "list=" + list +
                      '}';
          }
      }
      ```

      > xml文件配置

      ![](E:\notes\images\Snipaste_2022-01-27_19-25-32.png)

      - 1.引入util名称空间
      - 2.集合抽取
      - 3.创建对象，使用抽取的集合

      > 测试

      ```java
          @Test
          public void testBook() {
              ApplicationContext context = new ClassPathXmlApplicationContext("bean3.xml");
              Book book1 = context.getBean("book1", Book.class);
              Book book2 = context.getBean("book2", Book.class);
              System.out.println(book1);
              System.out.println(book2);
          }
      ```

      > 测试结果

      ![](E:\notes\images\Snipaste_2022-01-27_19-28-09.png)

      

### IOC操作Bean管理（FactoryBean）

1. spring有两种类型bean，一种**普通bean**，另外一种是**工厂bean**（FactoryBean）

   - 普通bean：在配置文件中定义的bean类型就是返回类型
   - 工厂bean：在配置文件中定义的bean类型可以和**返回类型**不一样

2. 工厂类演示

   1. 创建类，让这个类作为工厂bean，实现接口FactoryBean

   2. 实现接口里面的方法，在实现的方法中定义返回的bean类型

      > MyBean.java

      ```java
      public class MyBean implements FactoryBean<User> {
          //定义返回bean类型
          @Override
          public User getObject() throws Exception {
              User user = new User();
              user.setUid("2021****7");
              return user;
          }
      
          @Override
          public Class<?> getObjectType() {
              return null;
          }
      
          @Override
          public boolean isSingleton() {
              return FactoryBean.super.isSingleton();
          }
      }
      ```

      > xml配置

      ```xml
      <bean id="myBean" class="com.fwzlym.spring5.factorybean.MyBean">
      </bean>
      ```

   3. 测试代码

      ```java
          @Test
          public void testMyBean() {
              ApplicationContext context = new ClassPathXmlApplicationContext("bean4.xml");
              User user = context.getBean("myBean", User.class);
              System.out.println(user);
          }
      ```

![](E:\notes\images\Snipaste_2022-01-28_12-58-04.png)

### IOC操作Bean管理（bean作用域）

1. 在spring里面，可以设置bean创建的实例是多实例还是单实例对象

2. 在spring里面，默认情况下，bean是单实例对象

   > 默认情况

   > User.java

   ```java
   public class User {
       private String uid;
   
       public void setUid(String uid) {
           this.uid = uid;
       }
   }
   ```

   > xml

   ```xml
   <bean id="user" class="com.fwzlym.spring5.collectiontype.User">
       <property name="uid" value="2021****7"></property>
   </bean>
   ```

   > test

   ```java
       @Test
       public void testUser() {
           ApplicationContext context = new ClassPathXmlApplicationContext("bean4.xml");
           User user1 = context.getBean("user", User.class);
           User user2 = context.getBean("user", User.class);
           System.out.println(user1);
           System.out.println(user2);
       }
   ```

   > output

   ![](E:\notes\images\Snipaste_2022-01-28_13-08-54.png)

3. 如何设置单实例对象还是多实例对象

   - 在spring配置文件bean标签里面有属性（scope）用于设置单实例还是多实例

   - scope属性值有

     1. singleton : 单实例对象
     2. prototype : 多实例对象
     3. request、session 了解*

     - 区别：
       1. 默认singleton，即单实例对象，加载配置文件时候就会创建
       2. 设置prototype时候，**获取**（ getBean() ）对象的时候才会创建。

   > 多实例情况

   > 修改xml增加scope

   ```xml
   <bean id="user" class="com.fwzlym.spring5.collectiontype.User" scope="prototype">
       <property name="uid" value="2021****7"></property>
   </bean>
   ```

   > output

   ![](E:\notes\images\Snipaste_2022-01-28_13-13-53.png)

### IOC操作Bean管理（bean生命周期）

1. 生命周期：从对象创建到对象销毁的过程

2. bean生命周期

   1. 通过构造器创建bean实例（无参构造）
   2. 为bean的属性设置值和对其他bean引用（调用set方法）
   3. 调用bean的初始化的方法（需要进行配置）
   4. bean可以使用--获取到
   5. 当容器关闭时候，调用bean销毁的方法（需要进行配置销毁的方法）

3. 演示bean生命周期

   > Orders.java

   ```java
   public class Orders {
   
       private String oname;
   
       public Orders() {
           System.out.println("生命周期1.执行无参构造创建bean实例");
       }
   
       public void setOname(String oname) {
           this.oname = oname;
           System.out.println("生命周期2.执行set方法设置属性值");
       }
   
       public void init() {
           System.out.println("生命周期3.执行初始化方法 -- 自己配置");
       }
   
       public void destroy() {
           System.out.println("生命周期5.执行bean销毁的方法 -- 自己配置");
       }
   }
   ```

   > xml

   ```xml
   <bean id="orders" class="com.fwzlym.spring5.bean.Orders" init-method="init" destroy-method="destroy">
       <property name="oname" value="苹果"></property>
   </bean>
   ```

   > test

   ```java
       @Test
       public void testOrders() {
           ApplicationContext context = new ClassPathXmlApplicationContext("bean4.xml");
           Orders orders = context.getBean("orders", Orders.class);
           System.out.println("生命周期4.获取到了对象实例");
           ((ClassPathXmlApplicationContext)context).close();
       }
   ```

   > output

   ![](E:\notes\images\Snipaste_2022-01-28_14-57-27.png)

4. 更完整的bean生命周期--7步

   1. 通过构造器创建bean实例（无参构造）
   2. 为bean的属性设置值和对其他bean引用（调用set方法）
      - 把bean实例传递给bean后置处理器的方法
   3. 调用bean的初始化的方法（需要进行配置）
      - 把bean实例传递给bean后置处理器的方法
   4. bean可以使用--获取到
   5. 当容器关闭时候，调用bean销毁的方法（需要进行配置销毁的方法）

5. 完整演示

   > Orders.java

   ```java
   public class Orders {
   
       private String oname;
   
       public Orders() {
           System.out.println("生命周期1.执行无参构造创建bean实例");
       }
   
       public void setOname(String oname) {
           this.oname = oname;
           System.out.println("生命周期2.执行set方法设置属性值");
       }
   
       public void init() {
           System.out.println("生命周期3.执行初始化方法 -- 自己配置");
       }
   
       public void destroy() {
           System.out.println("生命周期5.执行bean销毁的方法 -- 自己配置");
       }
   }
   ```

   > 创建MyBeanPost继承BeanPostProcessor并重写方法

   ```java
   public class MyBeanPost implements BeanPostProcessor {
       @Override
       public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
           System.out.println("生命周期在初始化之前执行的方法");
           return bean;
       }
   
       @Override
       public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
           System.out.println("生命周期在初始化之后执行的方法");
           return bean;
       }
   }
   ```

   > xml配置后置处理器，一经配置，所有bean都会有

   ```xml
   <bean id="orders" class="com.fwzlym.spring5.bean.Orders" init-method="init" destroy-method="destroy">
       <property name="oname" value="苹果"></property>
   </bean>
   <!--配置后置处理器-->
   <bean id="myBeanPost" class="com.fwzlym.spring5.bean.MyBeanPost"></bean>
   ```

   > test

   ```java
   @Test
   public void testOrders() {
       ApplicationContext context = new ClassPathXmlApplicationContext("bean4.xml");
       Orders orders = context.getBean("orders", Orders.class);
       System.out.println("生命周期4.获取到了对象实例");
       ((ClassPathXmlApplicationContext)context).close();
   }
   ```

   > output

   ![](E:\notes\images\Snipaste_2022-01-28_16-18-37.png)

### IOC操作Bean管理（xml自动装配）*

1. 什么是自动装配

   - 根据指定装配规则（**属性名称**或者**属性类型**），spring自动将匹配的属性值进行注入

2. 演示手动装配过程

   > Emp.java

   ```java
   public class Emp {
       private String ename;
       private Dept dept;
   
       public void setDept(Dept dept) {
           this.dept = dept;
       }
   
       public void setEname(String ename) {
           this.ename = ename;
       }
   
       @Override
       public String toString() {
           return "Emp{" +
                   "ename='" + ename + '\'' +
                   ", dept=" + dept +
                   '}';
       }
   }
   ```

   > Dept.java

   ```java
   public class Dept {
       private String dname;
   
       public void setDname(String dname) {
           this.dname = dname;
       }
   
       @Override
       public String toString() {
           return "'" + dname + "'";
       }
   }
   ```

   > 手动装配

   > xml

   ```xml
   <bean id="emp" class="com.fwzlym.spring5.autowire.Emp">
       <property name="ename" value="李连杰"></property>
       <property name="dept" ref="dept"></property>
   </bean>
   
   <bean id="dept" class="com.fwzlym.spring5.autowire.Dept">
       <property name="dname" value="演员"></property>
   </bean>
   ```

   > test

   ```java
   @Test
   public void testAutoWire() {
       ApplicationContext context = new ClassPathXmlApplicationContext("bean5.xml");
       Emp emp = context.getBean("emp", Emp.class);
       System.out.println(emp);
   }
   ```

   > output

   ![](E:\notes\images\Snipaste_2022-01-28_16-36-43.png)

3. 演示自动装配过程

   - bean标签属性autowire 有两个值

     - byName : 根据属性名称注入
       - 名称注入bean的 **id** 需要跟类的**属性的名称**一样
     - byType : 根据属性类型注入
       - 根据类型进行注入的问题是如果有同一个类实例化的两个不同id 的bean报错

   - 实际中很少用到，都是使用基于注解的方式

   - 需要修改的仅xml代码

     ```xml
     <bean id="emp" class="com.fwzlym.spring5.autowire.Emp" autowire="byName">
         <property name="ename" value="李连杰"></property>
     </bean>
     
     <bean id="dept" class="com.fwzlym.spring5.autowire.Dept">
         <property name="dname" value="演员"></property>
     </bean>
     ```

### IOC操作Bean管理（外部属性文件）

1. 直接配置数据库

   - 配置德鲁伊连接池
   - 引入德鲁伊连接池jar包

   ![](E:\notes\images\Snipaste_2022-01-28_19-20-03.png)

2. 配置德鲁伊连接池演示

   > 普通方式

   ```xml
   <!--配置连接池-->
   <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
       <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
       <property name="url" value="jdbc:mysql://localhost:3306/db1"></property>
       <property name="username" value="root"></property>
       <property name="password" value="root"></property>
   </bean>
   ```

   > 外部属性文件

   - 外部属性文件

   ```properties
   prop.driverClassName=com.mysql.cj.jdbc.Driver
   prop.url=jdbc:mysql://localhost:3306/db1
   prop.username=root
   prop.password=root
   ```

   - 外部属性文件引入

     - context 名称空间引入

       ![](E:\notes\images\Snipaste_2022-01-28_19-31-41.png)

     - 在spring配置文件中使用标签引入外部属性文件

       ```xml
       <!--引入外部属性文件-->
       <context:property-placeholder location="classpath:jdbc.properties"/>
       ```

     - 连接池配置

       ```xml
       <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
           <property name="driverClassName" value="${prop.driverClassName}"></property>
           <property name="url" value="${prop.url}"></property>
           <property name="username" value="${prop.username}"></property>
           <property name="password" value="${prop.password}"></property>
       </bean>
       ```

### IOC操作Bean管理（基于注解方式）

1. 什么是注解

   1. 注解是代码的特殊标记，格式：@注解名称（属性名称=属性值，属性名称=属性值）
   2. 使用注解，注解作用在 **类**、**方法**、**属性**上面
   3. 使用注解目的：简化xml配置

2. **Spring对Bean 管理中创建对象提供注解**

   1. @Component
      - 普通注解，都可以实现创建对象
   2. @Service
      - 用在业务逻辑层，或者service层
   3. @Controller
      - 用在web层上
   4. @Repository
      - 用在dao或者持久层上

   > 四个注解功能一样，都可以创建bean实例

3. **基于注解方式实现对象创建**

   1. 引入aop依赖

      ![](E:\notes\images\Snipaste_2022-01-28_19-49-39.png)

   2. 引入context 名称空间

      ![](E:\notes\images\Snipaste_2022-01-28_19-31-41.png)

   3. 开启组件扫描

      ```xml
      <!--开启组件扫描-->
      <context:component-scan base-package="com.fwzlym.spring5"></context:component-scan>
      ```

      - 扫描多个包

        ```xml
        <!--开启组件扫描
         扫描多个包 使用，隔开
        -->
        <context:component-scan base-package="com.fwzlym.spring5.dao,com.fwzlym.spring5.service"></context:component-scan>
        ```

      - 扫描上层目录

        ```xml
        <!--扫描spring5文件夹内所有的包-->
        <context:component-scan base-package="com.fwzlym.spring5"></context:component-scan>
        ```

   4. 添加注解

      > service里UserService.java

      ![](E:\notes\images\Snipaste_2022-01-28_20-03-09.png)

      > test

      ```java
      @Test
      public void testService() {
          ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
          UserService userService = context.getBean("userService", UserService.class);
          userService.add();
      }
      ```

      > output

      ![](E:\notes\images\Snipaste_2022-01-28_20-06-46.png)

   5. 组件扫描了解内容

      ```xml
      <!--示例一 只扫描Service-->
      <context:component-scan base-package="com.fwzlym" use-default-filters="false">
          <context:include-filter type="annotation" expression="org.springframework.stereotype.Service"/>
      </context:component-scan>
      ```

      ```xml
      <!--示例二 不扫描Service-->
      <context:component-scan base-package="com.fwzlym" use-default-filters="false">
          <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Service"/>
      </context:component-scan>
      ```

4. **基于注解方式实现属性注入**

   1. @AutoWired
      - 根据属性类型进行自动装配，不需要set 方法
   2. @Qualifier
      - 根据属性名称进行注入，要跟AutoWired一起使用，即 **类型** + **名称**
   3. @Resource
      - 可以根据属性类型注入，也可以根据名称注入。不建议用，外部扩展包里的。
   4. @Value
      - 注入普通类型属性

   - 注入演示 1

     > dao里UserDao.java

     ```java
     public interface UserDao {
         public void add();
     }
     ```

     > dao里UserDaoImpl.java

     ```java
     @Repository //组件扫描必备
     public class UserDaoImpl implements UserDao{
         @Override
         public void add() {
             System.out.println("自动装配演示......");
         }
     }
     ```

     > service里UserService.java

     ```java
     @Service(value = "userService") //组件扫描必备
     public class UserService {
     
         @Autowired //自动装配
         private UserDao userDao;
         public void add() {
             System.out.println("service add......");
             userDao.add();
         }
     }
     ```

     > xml

     ```xml
     <!--扫描spring5文件夹内所有的包-->
     <context:component-scan base-package="com.fwzlym.spring5"></context:component-scan>
     ```

     > test

     ```java
     @Test
     public void testAutoWired() {
         ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
         UserService userService = context.getBean("userService", UserService.class);
         userService.add();
     }
     ```

     > output

     ![](E:\notes\images\Snipaste_2022-01-28_21-48-37.png)

   - 注入演示 2 （AutoWired + Qualifier ）

     ![](E:\notes\images\Snipaste_2022-01-28_21-59-51.png)

   - 注入演示 3（Resource）

     ```java
     @Resource //根据属性类型注入
     private UserDao userDao;
     public void add() {
         System.out.println("service add......");
         userDao.add();
     }
     ```

     ```java
     @Resource(name = "userDao") //根据属性名称注入
     private UserDao userDao;
     public void add() {
         System.out.println("service add......");
         userDao.add();
     }
     ```

   - 注入演示 4（Value）

     ```java
     @Value(value = "addMethod")
     private String sname;
     ```

5. 完全注解开发 -- springboot 常用

   1. 替换xml配置文件

      ![](E:\notes\images\Snipaste_2022-01-28_22-17-06.png)

   2. test

      ```java
      @Test
      public void testFullAnno() {
          ApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);
          UserService userService = context.getBean("userService", UserService.class);
          userService.add();
      }
      ```



# AOP

## AOP概念

1. 什么是AOP
   - 面向切面编程（方面），利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高开发的效率
   - ![](E:\notes\images\Snipaste_2022-01-29_12-51-07.png)
   - 通俗描述：不通过修改源代码，在主干功能添加新功能
   - 使用登录例子说明AOP

## AOP（底层原理）

1. AOP底层使用动态代理

   - 有两种情况动态代理

     - 有接口情况，使用JDK动态代理，创建**接口实现类**代理对象，增强类的方法

       ![](E:\notes\images\Snipaste_2022-01-29_13-06-41.png)

     - 没有接口情况，使用CGLIB动态代理，创建**子类**的代理对象，增强类的方法

       ![](E:\notes\images\Snipaste_2022-01-29_13-07-11.png)

## AOP（JDK动态代理）

1. 使用JDK 动态代理，使用Proxy 类里面的方法创建代理对象

   ![](E:\notes\images\Snipaste_2022-01-29_14-23-41.png)

   - 调用newProxyInstance方法

     ![](E:\notes\images\Snipaste_2022-01-29_14-24-19.png)

     - 方法有三个参数
       1. 第一个参数，类加载器
       2. 第二个参数，增强方法所在的类，这个类实现的接口，支持多个接口
       3. 第三个参数，实现这个接口InvocationHandler，创建代理对象，写增强的方法

2. 编写JDk 动态代理代码

   - 底层代码演示

     > UserDao

     ```java
     public interface UserDao {
     
         public void add(int a, int b);
     
         public void update();
     }
     ```

     > UserDaoImpl

     ```java
     public class UserDaoImpl implements UserDao{
         @Override
         public void add(int a, int b) {
             System.out.println(a+"+"+b+"="+(a+b));
         }
     
         @Override
         public void update() {
             System.out.println("update......");
         }
     }
     ```

     > JDKProxy.java -- 演示创建代理对象

     ```java
     public class JDKProxy {
     
         public static void main(String[] args) {
             //创建接口实现类代理对象
             Class[] interfaces = {UserDao.class};
             /*Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new InvocationHandler() {
                 @Override
                 public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                     return null;
                 }
             });*/
             UserDaoImpl userDao = new UserDaoImpl();
             UserDao dao = (UserDao)Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new UserDaoProxy(userDao));
             dao.add(1,2);
             dao.update();
         }
     }
     
     //创建代理对象代码
     class UserDaoProxy implements InvocationHandler {
     
         //1.把创建的是谁的代理对象，把谁传递过来
         //有参构造
         private Object obj;
         public UserDaoProxy(Object obj) {
             this.obj=obj;
         }
     
         //增强的逻辑
         @Override
         public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
             //方法之前
             System.out.println("方法之前执行..."+method.getName()+":传递的参数..."+ Arrays.toString(args));
             //被增强的方法执行
             Object invoke = method.invoke(obj, args);
             //方法之后
             System.out.println("方法之后执行..."+obj);
     
             return invoke;
         }
     }
     ```

     > 图解

     ![](E:\notes\images\Snipaste_2022-01-29_15-06-37.png)

## AOP术语

1. 连接点
   - 类里面有哪些方法可以被增强，这些方法被称为连接点
2. 切入点
   - 实际被增强的方法，称为切入点

3. **通知**（增强）
   - 增强的逻辑部分称为通知（增强）
   - 通知有多种类型
     1. 前置通知 -- 方法前
     2. 后置通知 -- 方法后
     3. 环绕通知 -- 方法前后
     4. 异常通知
     5. 最终通知 -- 类型finally
4. 切面
   - 把通知应用到切入点的过程就称为通知

## AOP操作（准备）

1. Spring框架一般基于 **AspectJ **实现AOP操作
   - AspectJ
     - AspectJ 不是Spring组成部分，独立AOP 框架，一般把AspectJ 和Spring 框架一起使用，进行AOP 操作
2. 基于AspectJ 实现AOP 操作
   1. 基于xml 配置文件方式
   2. 基于注解方式实现（使用）

3. 引入aop 依赖

   ![](E:\notes\images\Snipaste_2022-01-29_15-47-42.png)

4. 切入点表达式

   - 表达式作用：知道对哪个类哪个方法进行增强
   - 语法结构：execution（[权限修饰符] [返回类型] [类全路径] [方法名称]([参数列表])）
   - 举例1：对com.fwzlym.dao.BookDao类里面的add方法进行增强
     - execution(* com.fwzlym.dao.BookDao.add(..))
   - 举例2：对com.fwzlym.dao.BookDao类里面所有的方法进行增强
     - execution(* com.fwzlym.dao.BookDao.*(..))
   - 举例3：对com.fwzlym.dao包里面所有类，类里面的所有方法进行增强
     - execution(* com.fwzlym.dao. * . *(..))

## AOP操作（AspectJ 注解）

1. 创建类，类里面定义方法

   ```java
   public class User {
       public void add() {
           System.out.println("add......");
       }
   }
   ```

2. 创建增强类（编写增强逻辑）

   > 在增强类里面，创建方法，让不同方法代表不同通知类型

   ```java
   public class UserProxy {
   
       public void before() {
           System.out.println("增强的逻辑......");
       }
   }
   ```
   
3. 进行通知的配置

   1. 在spring 配置文件中，开启**注解扫描**

      - context 名称空间

        ```xml
        <!--开启注解扫描-->
        <context:component-scan base-package="com.fwzlym.spring5"></context:component-scan>
        ```

   2. 使用注解创建User 和 UserProxy对象

      > User

      ![](E:\notes\images\Snipaste_2022-01-29_16-40-14.png)

      > UserProxy

      ![](E:\notes\images\Snipaste_2022-01-29_16-42-48.png)

   3. 在增强类上面添加注解@Aspect -- 见上图

   4. 在spring配置文件中开启生成代理对象

      - aop 名称空间

        ![](E:\notes\images\Snipaste_2022-01-29_16-34-27.png)

      ```xml
      <!--开启Aspect生成代理对象--> 
      <aop:aspectj-autoproxy></aop:aspectj-autoproxy>
      ```

4. 配置不同类型的通知

   > UserProxy.java

   ```java
   @Component
   @Aspect
   public class UserProxy {
   
       //前置通知
       @Before(value = "execution(* com.fwzlym.spring5.aopanno.User.add(..))")
       public void before() {
           System.out.println("增强的前置通知......");
       }
   
       @After(value = "execution(* com.fwzlym.spring5.aopanno.User.add(..))")
       public void after() {
           System.out.println("增强的后置通知......");
       }
   
       @AfterReturning(value = "execution(* com.fwzlym.spring5.aopanno.User.add(..))")
       public void afterReturning() {
           System.out.println("增强的afterReturning通知......");
       }
   
       @AfterThrowing(value = "execution(* com.fwzlym.spring5.aopanno.User.add(..))")
       public void afterThrowing() {
           System.out.println("增强的afterThrowing通知......");
       }
   
       @Around(value = "execution(* com.fwzlym.spring5.aopanno.User.add(..))")
       public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable{
           System.out.println("增强的环绕通知之前......");
           proceedingJoinPoint.proceed();
           System.out.println("增强的环绕通知之后......");
       }
   }
   
   ```

   > test

   ```java
   @Test
   public void testAopAnno() {
       ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
       User user = context.getBean("user", User.class);
       user.add();
   }
   ```

   > output

   - 无异常输出

   ![](E:\notes\images\Snipaste_2022-01-29_17-47-15.png)

   - 异常输出

     ![](E:\notes\images\Snipaste_2022-01-29_17-49-14.png)

   > conclusion

   - After无论异常都会执行
   - AfterReturning 在返回值后才执行
   - Around 要设置ProceedingJoinPoint
   - 感觉代理对象表面上看更像一个原对象的附属物

5. 切入点抽取

   - 演示

     ```java
     //相同切入点抽取
     @Pointcut(value = "execution(* com.fwzlym.spring5.aopanno.User.add(..))")
     public void pointdemo() {
     
     }
     ```

     ![](E:\notes\images\Snipaste_2022-01-29_17-59-38.png)

6. 设置增强类的优先级

   > UserProxy优先级

   ```java
   @Component
   @Aspect
   @Order(3) //设置优先级3 比0低
   public class UserProxy {
   
       //相同切入点抽取
       @Pointcut(value = "execution(* com.fwzlym.spring5.aopanno.User.add(..))")
       public void pointdemo() {
   
       }
       //前置通知
       @Before(value = "pointdemo()")
       public void before() {
           System.out.println("增强的前置通知......");
       }
   
       @After(value = "pointdemo()")
       public void after() {
           System.out.println("增强的后置通知......");
       }
   
       @AfterReturning(value = "pointdemo()")
       public void afterReturning() {
           System.out.println("增强的afterReturning通知......");
       }
   
       @AfterThrowing(value = "pointdemo()")
       public void afterThrowing() {
           System.out.println("增强的afterThrowing通知......");
       }
   
       @Around(value = "pointdemo()")
       public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable{
           System.out.println("增强的环绕通知之前......");
           proceedingJoinPoint.proceed();
           System.out.println("增强的环绕通知之后......");
       }
   }
   ```

   > PersonProxy优先级

   ```java
   @Component
   @Aspect
   @Order(1) //优先级1 比3高
   public class PersonProxy {
   
       @Before(value = "execution(* com.fwzlym.spring5.aopanno.User.add(..))")
       public void before() {
           System.out.println("test priority ......");
       }
   }
   ```

   > output

   ![](E:\notes\images\Snipaste_2022-01-29_18-06-17.png)
   
7. **AspectJ** 完全注解开发

   > Book.java 被增强类

   ```java
   @Component //可以被组件扫描
   public class Book {
   
       public void buy() {
           System.out.println("buy......");
       }
   }
   ```

   > BookProxy.java 增强类

   ```java
   @Component //可以被组件扫描
   @Aspect //生成代理对象
   public class BookProxy {
   
       @Pointcut(value = "execution(* com.fwzlym.spring5.aopxml.Book.buy(..))") //抽取切入点
       public void pointBuy() {
   
       }
   
       @Before(value = "pointBuy()") //前置通知
       public void before() {
           System.out.println("增强前置通知......");
       }
   }
   ```

   > BookConfig.java 创建配置类

   ```java
   @Configuration //配置类 -- 代替xml
   @ComponentScan(basePackages = {"com.fwzlym.spring5"}) //开启组件扫描，扫描位置
   @EnableAspectJAutoProxy(proxyTargetClass = true) //自动代理对象生成
   public class BookConfig {
   }
   ```

   > test

   ```java
   @Test
   public void testFullAnno() {
       ApplicationContext context = new AnnotationConfigApplicationContext(BookConfig.class);
       Book book = context.getBean("book", Book.class);
       book.buy();
   }
   ```

   > output

   ![](E:\notes\images\Snipaste_2022-01-30_14-23-46.png)

## AOP操作（AspectJ 配置文件）*

1. 创建两个类，增强类和被增强类，创建方法
2. 在spring配置文件中创建两个类对象
3. 在spring配置文件中配置切入点

- 演示

  > Book.java

  ```java
  public class Book {
  
      public void buy() {
          System.out.println("buy......");
      }
  }
  ```

  > BookProxy.java

  ```java
  public class BookProxy {
  
      public void before() {
          System.out.println("增强前置通知......");
      }
  }
  ```

  > xml

  ```xml
  <!--1.创建对象-->
  <bean id="book" class="com.fwzlym.spring5.aopxml.Book">
  </bean>
  <bean id="bookProxy" class="com.fwzlym.spring5.aopxml.BookProxy">
  </bean>
  <!--2.配置aop增强-->
  <aop:config>
      <!--切入点-->
      <aop:pointcut id="p" expression="execution(* com.fwzlym.spring5.aopxml.Book.buy(..))"/>
      <!--切面-->
      <aop:aspect ref="bookProxy">
          <!--增强作用在具体的方法上-->
          <aop:before method="before" pointcut-ref="p"></aop:before>
      </aop:aspect>
  </aop:config>
  ```

  > test

  ```java
  @Test
  public void testXml() {
      ApplicationContext context = new ClassPathXmlApplicationContext("bean2.xml");
      Book book = context.getBean("book", Book.class);
      book.buy();
  }
  ```

  > output

  ![](E:\notes\images\Snipaste_2022-01-30_14-12-15.png)



# JdbcTemplate

## JdbcTemplate（概念与准备）

1. 什么是JdbcTemplate
   - spring框架对Jdbc进行封装，使用JdbcTemplate方便对数据库进行操作

2. 准备工作

   - 引入依赖

     ![](E:\notes\images\Snipaste_2022-01-30_15-32-03.png)

   - 在spring配置文件配置数据库连接池

     > xml配置

     ```xml
     <!--引入外部属性文件 需要context名称空间-->
     <context:property-placeholder location="classpath:jdbc.properties"></context:property-placeholder>
     <!--配置德鲁伊连接池 使用外部属性文件-->
     <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
         <property name="driverClassName" value="${prop.driverClassName}"></property>
         <property name="url" value="${prop.url}"></property>
         <property name="username" value="${prop.username}"></property>
         <property name="password" value="${prop.password}"></property>
     </bean>
     ```

     > 外部属性文件

     ```properties
     prop.driverClassName=com.mysql.cj.jdbc.Driver
     prop.url=jdbc:mysql://localhost:3306/db1
     prop.username=root
     prop.password=root
     ```

3. 配置JdbcTemplate 对象，注入DataSource

   ```xml
   <!--配置JdbcTemplate对象，注入DataSource-->
   <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
       <!--注入数据源信息-->
       <property name="dataSource" ref="dataSource"></property>
   </bean>
   ```

- 过程演示

  - 举例：创建service类，创建dao类，在dao注入jdbcTemplate对象

  > BookDao.java

  ```java
  public interface BookDao {
  }
  ```

  > BookDaoImpl.java

  ```java
  @Repository //组件扫描
  public class BookDaoImpl implements BookDao{
  
      //注入JdbcTemplate
      @Autowired //自动装配
      private JdbcTemplate jdbcTemplate;
  }
  ```

  > BookService.java

  ```java
  @Service //组件扫描
  public class BookService {
  
      //注入dao
      @Autowired //自动装配
      private BookDao bookDao;
  
  }
  ```

  > xml

  ```xml
  <!--引入外部属性文件-->
  <context:property-placeholder location="classpath:jdbc.properties"></context:property-placeholder>
  <!--配置德鲁伊连接池-->
  <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
      <property name="driverClassName" value="${prop.driverClassName}"></property>
      <property name="url" value="${prop.url}"></property>
      <property name="username" value="${prop.username}"></property>
      <property name="password" value="${prop.password}"></property>
  </bean>
  <!--配置JdbcTemplate对象，注入DataSource-->
  <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
      <!--注入数据源信息-->
      <property name="dataSource" ref="dataSource"></property>
  </bean>
  
  <!--开启组件扫描-->
  <context:component-scan base-package="com.fwzlym.spring5"></context:component-scan>
  ```

  > 不支持MySQL的版本，需要升级

  ![](E:\notes\images\Snipaste_2022-01-30_16-25-23.png)

## JdbcTemplate操作数据库（添加、修改、删除操作）

1. 添加操作演示

   > Book.java --向数据库添加书

   ```java
   public class Book {
   
       private String id;//标号
       private String bname;//名称
       private String status;//状态
   
       public String getId() {
           return id;
       }
   
       public String getBname() {
           return bname;
       }
   
       public String getStatus() {
           return status;
       }
   	//有参构造
       public Book(String id, String bname, String status) {
           this.id = id;
           this.bname = bname;
           this.status = status;
       }
   }
   ```

   > BookService.java

   ```java
   @Service
   public class BookService {
   
       //注入dao -- 使用dao的方法添加
       @Autowired
       private BookDao bookDao;
   
       public void addBook(Book book) {
           bookDao.addBook(book);
       }
   }
   ```

   > BookDao.java

   ```java
   public interface BookDao {
       //添加书的方法
       void addBook(Book book);
   }
   ```

   > BookDaoImpl.java

   ```java
   @Repository//组件扫描
   public class BookDaoImpl implements BookDao{
   
       //注入JdbcTemplate , 在方法实现类中注入jdbc直接使用
       @Autowired
       private JdbcTemplate jdbcTemplate;
   
       @Override
       public void addBook(Book book) {
           //1.sql
           String sql = "insert into t_book values(?,?,?)";
           //2.调用方法实现
           Object[] args = {book.getId(), book.getBname(), book.getStatus()};
           jdbcTemplate.update(sql, args);//操作数据库
       }
   }
   ```

   > test

   ```java
   @Test
   public void testBook() {
       ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
       BookService bookService = context.getBean("bookService", BookService.class);
       Book book1 = new Book("001", "钢铁是怎样炼成的", "余1000");
       bookService.addBook(book1);
   }
   ```

   > 数据库

   ![](E:\notes\images\Snipaste_2022-01-30_16-42-54.png)

2. 修改和删除演示

   - 修改

     > BookService

     ```java
     public void updateBook(Book book) {
         bookDao.updateBook(book);
     }
     ```

     > BookDao

     ```java
     void updateBook(Book book);
     ```

     > BookDaoImpl

     ```java
     @Override
     public void updateBook(Book book) {
         //1.sql -- 修改数据库表t_book bId位置的其他数据信息
         String sql = "update t_book set bName=?,bStatus=? where bId=?";
         //参数要一一对应
         Object[] args = {book.getBname(), book.getStatus(), book.getId()};
         //2.调用模板
         int update = jdbcTemplate.update(sql, args);
         System.out.println(update);
     }
     ```

     > test

     ```java
         @Test
         public void testBook() {
             ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
             BookService bookService = context.getBean("bookService", BookService.class);
             Book book = new Book("001", "安徒生童话", "余59");
             bookService.updateBook(book);
         }
     ```

     > 数据库

     ![](E:\notes\images\Snipaste_2022-01-30_17-02-58.png)

   - 删除

     > BookService

     ```java
     public void delBook(String id) {
         bookDao.delBook(id);
     }
     ```

     > BookDao

     ```java
     void delBook(String id);
     ```

     > BookDaoImpl

     ```java
     @Override
     public void delBook(String id) {
         //1.sql -- 删除bId的那一行
         String sql = "delete from t_book where bId=?";
         //2.调用
         int update = jdbcTemplate.update(sql, id);
         System.out.println(update);
     }
     ```

     > test

     ```java
         @Test
         public void testBook() {
             ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
             BookService bookService = context.getBean("bookService", BookService.class);
             bookService.delBook("004");
         }
     ```

     > 数据库之前

     ![](E:\notes\images\Snipaste_2022-01-30_17-09-56.png)

     > 数据库之后

     ![](E:\notes\images\Snipaste_2022-01-30_17-10-37.png)

## JdbcTemplate操作数据库（查询操作）

1. 查询数据库表记录总数

   - jdbcTemplate.queryForObject(String sql, Class<T> requiredType)

     - sql:数据库操作语句
     - requiredType:返回值类型

   - 演示

     > BookService

     ```java
     //查询表中记录总数
     public int countBook() {
         return bookDao.count();
     }
     ```

     > BookDao

     ```java
     int count();
     ```

     > BookDaoImpl

     ```java
     @Override
     public int count() {
         //1.sql
         String sql = "select count(*) from t_book";
         //2.调用模板
         Integer count = jdbcTemplate.queryForObject(sql, Integer.class);
         return count;
     }
     ```

     > test

     ```java
         @Test
         public void testBook() {
             ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
             BookService bookService = context.getBean("bookService", BookService.class);
             int i = bookService.countBook();
             System.out.println(i);
         }
     ```

     > output

     > 3

2. 查询返回对象

   - jdbcTemplate.queryForObject(String var1, RowMapper<T> var2, @Nullable Object... var3)

     - var1: sql语句

     - var2: RowMapper,接口，返回不同类型数据，使用这个接口里面实现类可以实现数据封装

       ```java
       //需要返回什么类型的数据就注明
       new BeanPropertyRowMapper<Book>(Book.class)
       new BeanPropertyRowMapper<>()
       ```

     - var3: sql语句对应的值

     - **该方法是先创建一个空参构造器，再调用对应属性的set方法对属性进行赋值！**
     
   - 演示
   
     > BookService
   
     ```java
     //通过id查询返回对象
     public Book findOne(String id) {
         return bookDao.findBookInfo(id);
     }
     ```
   
     > BookDao
   
     ```java
     Book findBookInfo(String id);
     ```
   
     > BookDaoImpl
   
     ```java
     @Override
     public Book findBookInfo(String id) {
         //1.sql
         String sql = "select * from t_book where bId=?";
         //2.调用
         Book book1 = jdbcTemplate.queryForObject(sql, new BeanPropertyRowMapper<Book>(Book.class), id);
         return book1;
     }
     ```
   
     > test
   
     ```java
         @Test
         public void testBook() {
             ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
             BookService bookService = context.getBean("bookService", BookService.class);
             Book one = bookService.findOne("001");
             System.out.println(one);
         }
     ```
   
     > output
   
     ![](E:\notes\images\Snipaste_2022-01-31_19-38-41.png)
   
   - 注意事项
   
     - queryForObject参数中设置的返回类型的类比如Book类定义的属性要和数据库一致或者符合小驼峰命名规范，否则返回对象部分属性为null或全为null
   
3. 查询全部对象

   - List<T> query(String sql, RowMapper<T> rowMapper)

   - 演示

     > BookService

     ```java
     //查询返回全部对象
     public List<Book> findAll() {
         return bookDao.findAll();
     }
     ```

     > BookDao

     ```java
     List<Book> findAll();
     ```

     > BookDaoImpl

     ```java
     @Override
     public List<Book> findAll() {
         //1.sql语句
         String sql = "select * from t_book";
         //2.调用
         List<Book> bookList = jdbcTemplate.query(sql, new BeanPropertyRowMapper<Book>(Book.class));
         return bookList;
     }
     ```

     > test

     ```java
         @Test
         public void testBook() {
             ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
             BookService bookService = context.getBean("bookService", BookService.class);
             List<Book> all = bookService.findAll();
             System.out.println(all);
         }
     ```

     > output

     ![](E:\notes\images\Snipaste_2022-01-31_19-57-28.png)

## JdbcTemplate操作数据库（批量操作）

1. 批量操作：操作表里面的多条记录

2. JdbcTemplate实现批量添加操作

   - 方法：batchUpdate(String sql, List<Object []> batchArgs)

     - sql:数据库操作语句
     - batchArgs:List集合，添加多条记录

   - 演示

     > BookService

     ```java
     //批量添加操作
     public void batchAdd(List<Object[]> batchArgs) {
         bookDao.batchAddBook(batchArgs);
     }
     ```

     > BookDao

     ```java
     void batchAddBook(List<Object[]> batchArgs);
     ```

     > BookDaoImpl

     ```java
     @Override
     public void batchAddBook(List<Object[]> batchArgs) {
         //1.sql
         String sql = "insert into t_book values(?,?,?)";
         //2.调用
         int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
         System.out.println(Arrays.toString(ints));
     }
     ```

     > test

     ```java
         @Test
         public void testBook() {
             ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
             BookService bookService = context.getBean("bookService", BookService.class);
             //批量添加
             List<Object[]> batchArgs = new ArrayList<>();
             Object[] o1 = {"004","雪山飞狐","余22"};
             Object[] o2 = {"005", "连城诀", "余34"};
             Object[] o3 = {"006", "活着", "余199"};
             batchArgs.add(o1);
             batchArgs.add(o2);
             batchArgs.add(o3);
             bookService.batchAdd(batchArgs);
         }
     ```

     > output

     ![](E:\notes\images\Snipaste_2022-02-01_12-13-25.png)

3. 批量修改操作

   - 演示

     > BookService

     ```java
     //批量修改
     public void batchUpdate(List<Object[]> batchArgs) {
         bookDao.batchUpdateBook(batchArgs);
     }
     ```

     > BookDao

     ```java
     void batchUpdateBook(List<Object[]> batchArgs);
     ```

     > BookDaoImpl

     ```java
     @Override
     public void batchUpdateBook(List<Object[]> batchArgs) {
         //1.sql 注意对应值 bName bStatus bId
         String sql = "update t_book set bName=?,bStatus=? where bId=?";
         //2.调用
         int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
         System.out.println(Arrays.toString(ints));
     }
     ```

     > test

     ```java
         @Test
         public void testBook() {
             ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
             BookService bookService = context.getBean("bookService", BookService.class);
             //批量修改
             List<Object[]> batchArgs = new ArrayList<>();
             Object[] o1 = {"辛德勒的名单", "余21", "004"};
             Object[] o2 = {"美丽人生", "余29", "005"};
             Object[] o3 = {"唐诗三百首", "余109", "006"};
             batchArgs.add(o1);
             batchArgs.add(o2);
             batchArgs.add(o3);
             bookService.batchUpdate(batchArgs);
         }
     ```

     > output

     ![](E:\notes\images\Snipaste_2022-02-01_12-25-37.png)

4. 批量删除操作

   - 演示

     > BookService

     ```java
     //批量删除
     public void batchDelete(List<Object[]> batchArgs) {
         bookDao.batchDeleteBook(batchArgs);
     }
     ```

     > BookDao

     ```java
     void batchDeleteBook(List<Object[]> batchArgs);
     ```

     > BookDaoImpl

     ```java
     @Override
     public void batchDeleteBook(List<Object[]> batchArgs) {
         //1.sql
         String sql = "delete from t_book where bId=?";
         //2.
         int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
         System.out.println(Arrays.toString(ints));
     }
     ```

     > test

     ```java
         @Test
         public void testBook() {
             ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
             BookService bookService = context.getBean("bookService", BookService.class);
             //批量删除
             List<Object[]> batchArgs = new ArrayList<>();
             Object[] o1 = {"004"};
             Object[] o2 = {"005"};
             Object[] o3 = {"006"};
             batchArgs.add(o1);
             batchArgs.add(o2);
             batchArgs.add(o3);
             bookService.batchDelete(batchArgs);
         }
     ```

     > output

     ![](E:\notes\images\Snipaste_2022-02-01_12-32-15.png)

5. JdbcTemplate完整演示

   ```java
   @Service
   public class BookService {
   
       //注入dao
       @Autowired
       private BookDao bookDao;
   
       //添加书
       public void addBook(Book book) {
           bookDao.addBook(book);
       }
   
       //修改书记录
       public void updateBook(Book book) {
           bookDao.updateBook(book);
       }
   
       //删除书
       public void delBook(String id) {
           bookDao.delBook(id);
       }
   
       //查询表中记录总数
       public int countBook() {
           return bookDao.count();
       }
   
       //查询返回对象
       public Book findOne(String id) {
           return bookDao.findBookInfo(id);
       }
   
       //查询返回全部对象
       public List<Book> findAll() {
           return bookDao.findAll();
       }
   
       //批量添加操作
       public void batchAdd(List<Object[]> batchArgs) {
           bookDao.batchAddBook(batchArgs);
       }
   
       //批量修改
       public void batchUpdate(List<Object[]> batchArgs) {
           bookDao.batchUpdateBook(batchArgs);
       }
   
       //批量删除
       public void batchDelete(List<Object[]> batchArgs) {
           bookDao.batchDeleteBook(batchArgs);
       }
   }
   ```

   ```java
   public interface BookDao {
       void addBook(Book book);
   
       void updateBook(Book book);
   
       void delBook(String id);
   
       int count();
   
       Book findBookInfo(String id);
   
       List<Book> findAll();
   
       void batchAddBook(List<Object[]> batchArgs);
   
       void batchUpdateBook(List<Object[]> batchArgs);
   
       void batchDeleteBook(List<Object[]> batchArgs);
   }
   ```

   ```java
   @Repository
   public class BookDaoImpl implements BookDao {
   
       //注入JdbcTemplate
       @Autowired
       private JdbcTemplate jdbcTemplate;
   
       @Override
       public void addBook(Book book) {
           //1.sql
           String sql = "insert into t_book values(?,?,?)";
           //2.调用方法实现
           Object[] args = {book.getbId(), book.getbName(), book.getbStatus()};
           int update = jdbcTemplate.update(sql, args);
           System.out.println(update);
       }
   
       @Override
       public void updateBook(Book book) {
           //1.sql
           String sql = "update t_book set bName=?,bStatus=? where bId=?";
           Object[] args = {book.getbName(), book.getbStatus(), book.getbId()};
           //2.
           int update = jdbcTemplate.update(sql, args);
           System.out.println(update);
       }
   
       @Override
       public void delBook(String id) {
           //1.sql
           String sql = "delete from t_book where bId=?";
           //2.
           int update = jdbcTemplate.update(sql, id);
           System.out.println(update);
       }
   
       @Override
       public int count() {
           //1.sql
           String sql = "select count(*) from t_book";
           //2.
           Integer count = jdbcTemplate.queryForObject(sql, Integer.class);
           return count;
       }
   
       @Override
       public Book findBookInfo(String id) {
           //1.sql
           String sql = "select * from t_book where bId=?";
           //2.
           Book book1 = jdbcTemplate.queryForObject(sql, new BeanPropertyRowMapper<Book>(Book.class), id);
           return book1;
       }
   
       @Override
       public List<Book> findAll() {
           //1.sql
           String sql = "select * from t_book";
           List<Book> bookList = jdbcTemplate.query(sql, new BeanPropertyRowMapper<Book>(Book.class));
           return bookList;
       }
   
       @Override
       public void batchAddBook(List<Object[]> batchArgs) {
           //1.sql
           String sql = "insert into t_book values(?,?,?)";
           //2.
           int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
           System.out.println(Arrays.toString(ints));
       }
   
       @Override
       public void batchUpdateBook(List<Object[]> batchArgs) {
           //1.sql
           String sql = "update t_book set bName=?,bStatus=? where bId=?";
           //2.调用
           int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
           System.out.println(Arrays.toString(ints));
       }
   
       @Override
       public void batchDeleteBook(List<Object[]> batchArgs) {
           //1.sql
           String sql = "delete from t_book where bId=?";
           //2.
           int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
           System.out.println(Arrays.toString(ints));
       }
   }
   ```

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                              http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">
   
       <!--引入外部属性文件-->
       <context:property-placeholder location="classpath:jdbc.properties"></context:property-placeholder>
       <!--配置德鲁伊连接池-->
       <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
           <property name="driverClassName" value="${prop.driverClassName}"></property>
           <property name="url" value="${prop.url}"></property>
           <property name="username" value="${prop.username}"></property>
           <property name="password" value="${prop.password}"></property>
       </bean>
       <!--配置JdbcTemplate对象，注入DataSource-->
       <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
           <!--注入数据源信息-->
           <property name="dataSource" ref="dataSource"></property>
       </bean>
   
       <!--开启组件扫描-->
       <context:component-scan base-package="com.fwzlym.spring5"></context:component-scan>
   
   </beans>
   ```

   ```properties
   prop.driverClassName=com.mysql.cj.jdbc.Driver
   prop.url=jdbc:mysql://localhost:3306/db1
   prop.username=root
   prop.password=root
   ```

   ```java
   public class Book {
   
       private String bId;
       private String bName;
       private String bStatus;
   
       public Book() {
       }
   
       public Book(String bId, String bName, String bStatus) {
           this.bId = bId;
           this.bName = bName;
           this.bStatus = bStatus;
       }
   
       public String getbId() {
           return bId;
       }
   
       public void setbId(String bId) {
           this.bId = bId;
       }
   
       public String getbName() {
           return bName;
       }
   
       public void setbName(String bName) {
           this.bName = bName;
       }
   
       public String getbStatus() {
           return bStatus;
       }
   
       public void setbStatus(String bStatus) {
           this.bStatus = bStatus;
       }
   
       @Override
       public String toString() {
           return "Book{" +
                   "bId='" + bId + '\'' +
                   ", bName='" + bName + '\'' +
                   ", bStatus='" + bStatus + '\'' +
                   '}';
       }
   }
   ```

   ```java
   public class TestBook {
       @Test
       public void testBook() {
           ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
           BookService bookService = context.getBean("bookService", BookService.class);
   //        Book book1 = new Book("004", "重生之我是大明神探", "余37");
   //        bookService.addBook(book1);
   //        Book book = new Book("001", "安徒生童话", "余59");
   //        bookService.updateBook(book);
   //        int i = bookService.countBook();
   //        System.out.println(i);
   //        List<Book> all = bookService.findAll();
   //        System.out.println(all);
           //批量添加
   //        List<Object[]> batchArgs = new ArrayList<>();
   //        Object[] o1 = {"004","雪山飞狐","余22"};
   //        Object[] o2 = {"005", "连城诀", "余34"};
   //        Object[] o3 = {"006", "活着", "余199"};
   //        batchArgs.add(o1);
   //        batchArgs.add(o2);
   //        batchArgs.add(o3);
   //        bookService.batchAdd(batchArgs);
           //批量修改
   //        List<Object[]> batchArgs = new ArrayList<>();
   //        Object[] o1 = {"辛德勒的名单", "余21", "004"};
   //        Object[] o2 = {"美丽人生", "余29", "005"};
   //        Object[] o3 = {"唐诗三百首", "余109", "006"};
   //        batchArgs.add(o1);
   //        batchArgs.add(o2);
   //        batchArgs.add(o3);
   //        bookService.batchUpdate(batchArgs);
           //批量删除
           List<Object[]> batchArgs = new ArrayList<>();
           Object[] o1 = {"004"};
           Object[] o2 = {"005"};
           Object[] o3 = {"006"};
           batchArgs.add(o1);
           batchArgs.add(o2);
           batchArgs.add(o3);
           bookService.batchDelete(batchArgs);
       }
   }
   ```
