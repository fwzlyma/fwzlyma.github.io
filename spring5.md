JdbcTemplate完整演示

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
