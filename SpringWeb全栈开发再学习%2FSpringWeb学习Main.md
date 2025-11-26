# SpringWeb学习教程



## 创建一个Spring Boot应用程序

### 主应用类

SpringBoot应用的入口类

使用@SpringBootApplication注解来启动自动配置

```
@SpringBootApplication注解包含了三个重要注解：
     @Configuration: 标记这是一个配置类
     @EnableAutoConfiguration: 启用Spring Boot的自动配置
     @ComponentScan: 启用组件扫描
```

```java
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        // 启动Spring Boot应用
        SpringApplication.run(DemoApplication.class, args);
        System.out.println("应用启动成功！");
    }
}
```

### 创建REST控制器

控制器负责处理HTTP请求，@RestController简化了RESTful API的开发

@RestController = @Controller + @RespnseBody



- • `@RestController`：声明这是一个REST控制器
- • `@RequestMapping`：定义请求的基础路径
- • `@GetMapping`：处理HTTP GET请求
- • `@PostMapping`：处理HTTP POST请求
- • `@PathVariable`：获取URL路径中的参数
- • `@RequestBody`：获取请求体中的数据



# MongoDB

MongoDB是一个流行的NoSQL数据库，使用文档存储数据。

## 核心概念

### MongoDB

- 数据库(Database)**：数据的物理容器
- **集合(Collection)**：相当于关系数据库中的表
- **文档(Document)**：相当于关系数据库中的行
- **字段(Field)**：相当于关系数据库中的列

### 与关系数据库对比

- MySQL的表(Table) → MongoDB的集合(Collection)
- MySQL的行(Row) → MongoDB的文档(Document)
- MySQL的列(Column) → MongoDB的字段(Field)
- MySQL的JOIN → MongoDB的嵌入文档或引用



## 创建实体类

在Spring Data MongoDB中，使用@Document注解来映射MongoDB的文档

@Document注解制定了这个类对应MongoDB中的那个集合

如果不指定collection属性，默认使用类名的小写形式

```java
@Document(collection = "users")
```

@Id 注解标记这是文档的主键

在MongoDB中，主键字段名是_id

```java
@Id
private String id;
```

@Field注解可以指定字段在MongoDB中的名称，不指定则默认使用Java字段名

```java
@Field("user_name")
private String username;
```

创建构造函数时可以使用构造器语句，设定创建时间，在传参时也可以通过this()来初始化时间



实体类中可以嵌入文档

作为嵌入文档就不需要加上@Document注解了

嵌入文档中可以重写toString()方法



## 创建Repository接口

Spring Data的Repository模式是的只需要定义接口，不需要实现类就可以完成数据访问操作

```java
@Repository
public interface UserRepository extends MongoRepository<User, String> {  //查找方法...   }
```

继承MongoRepository接口，获得基本的CRUD功能

 * MongoRepository<User, String>中的泛型参数：
 * - User: 实体类类型
 * - String: 主键类型
 * @Repository注解将这个接口标记为数据访问组件

Repository方法命名规范：

方法命名

1. 查询动词开头
2. 条件关键字连接属
3. 排序与分页
4. 特殊场景处理

[实例](./Repository方法命名规范.md)



# 创建Service层

Service层负责业务逻辑，调用Repository完成数据操作

extend 非常重要

@Service注解标记这是一个服务组件

@Transactional注解启用事务管理

```java
@Service
@Transactional
public class UserService {}
```

[Service](./branch_Service层.md)

```java
 @Autowired
    private UserRepository userRepository;
```

```java
public List<User> findAll() {
        return userRepository.findAll();
    }
    
public Optional<User> findById(String id) {
        return userRepository.findById(id);
    }
```

```java
/**
     * 保存用户
     * 
     * @param user 用户对象
     * @return 保存后的用户对象
     * @throws IllegalArgumentException 如果用户名或邮箱已存在
     */
    public User save(User user) {
        // 验证用户名和邮箱的唯一性
        if (user.getUsername() != null && userRepository.existsByUsername(user.getUsername())) {
            throw new IllegalArgumentException("用户名已存在: " + user.getUsername());
        }
        
        if (user.getEmail() != null && userRepository.existsByEmail(user.getEmail())) {
            throw new IllegalArgumentException("邮箱已存在: " + user.getEmail());
        }
        
        // 设置更新时间
        if (user.getId() != null) {
            user.setUpdatedAt(java.time.LocalDateTime.now());
        }
        
        return userRepository.save(user);
    }
    
    /**
     * 删除用户
     * 
     * @param id 用户ID
     */
    public void deleteById(String id) {
        userRepository.deleteById(id);
    }
    
    /**
     * 根据用户名删除用户
     * 
     * @param username 用户名
     */
    public void deleteByUsername(String username) {
        userRepository.deleteByUsername(username);
    }
```

需要传入参数时，可以判断一下传入的判断参数是否有效(大于0，是否为空等)

```java
if (minAge < 0 || maxAge < 0) {
            throw new IllegalArgumentException("年龄不能为负数");
        }
        
        if (minAge > maxAge) {
            throw new IllegalArgumentException("最小年龄不能大于最大年龄");
        }
return userRepository.findByAgeBetween(minAge, maxAge);
```

```java
if (city == null || city.trim().isEmpty()) {
            throw new IllegalArgumentException("城市名称不能为空");
        }
        
        return userRepository.findByCity(city);
```

```java
public void deleteByUsername(String username) {
        userRepository.deleteByUsername(username);
    }
```

```java
public List<User> searchByUsername(String keyword) {
        if (keyword == null || keyword.trim().isEmpty()) {
            return userRepository.findAll();
        }
        
        // 使用正则表达式进行模糊匹配
        String regex = ".*" + keyword + ".*";
        return userRepository.findByUsernameRegex(regex);
    }
```



# 创建REST控制器

控制器负责处理HTTP请求，调用Service层完成业务逻辑。

@RestController标记REST控制器

@RequestMapping [类]定义基础URL路径



@GetMapping  无参或者("")/("/{...}")

```java
@GetMapping("/{id}")
public ResponseEntity<User> getUserById(@PathVariable String id) {
        Optional<User> user = userService.findById(id);
        
        if (user.isPresent()) {
            return ResponseEntity.ok(user.get());
        } else {
            return ResponseEntity.notFound().build();
        }
    }
```

```java
/**
     * 根据用户名获取用户
     * 
     * @param username 用户名
     * @return 用户对象或404状态
     */
  @GetMapping("/username/{username}")
    public ResponseEntity<User> getUserByUsername(@PathVariable String username) {
        Optional<User> user = userService.findByUsername(username);
        
        if (user.isPresent()) {
            return ResponseEntity.ok(user.get());
        } else {
            return ResponseEntity.notFound().build();
        }
    }
```



#### **核心构成说明**

- **返回类型 ResponseEntity<User>**：
  - `ResponseEntity`：封装HTTP响应的状态码（如200 OK、404 Not Found）、响应头（如Content-Type）和响应体（`User`对象）。
  - `<User>`：泛型指定响应体的数据类型为自定义的`User`实体类（通常包含id、username、email等字段）。
- **方法参数 @PathVariable String username**：
  - 通过`@PathVariable`注解从URL路径中提取`username`参数（例如请求`/users/alice`时，`username`值为`"alice"`）。

### **1. @GetMapping：处理“查询”请求（获取资源）**

- **对应HTTP方法**：`GET`

- **核心作用**：从服务器**读取/查询资源**（如获取用户信息、商品列表），不修改数据。

- 特点

  ：

  - 参数会通过URL明文传递（如 `/users?id=123`），长度有限制，安全性较低。
  - 可被浏览器缓存，适合频繁查询的场景。

- 示例

  ：

  ```
  @GetMapping("/users/{id}")  // URL: /users/123
  public User getUser(@PathVariable Long id) {
      return userService.findById(id);  // 返回ID=123的用户信息
  }
  ```

### **2. @PostMapping：处理“提交”请求（创建资源）**

- **对应HTTP方法**：`POST`

- **核心作用**：向服务器**提交新数据**（如创建用户、提交表单），通常会导致服务器资源增加。

- 特点

  ：

  - 参数通过请求体（Body）传递，不在URL中显示，长度无限制，安全性较高。
  - 不可被浏览器缓存，适合敏感数据（如密码）或大量数据提交。

- 示例

  ：

  ```
  @PostMapping("/users")  // URL: /users
  public ResponseEntity<User> createUser(@RequestBody User user) {
      User savedUser = userService.save(user);  // 保存新用户
      return ResponseEntity.status(201).body(savedUser);  // 返回创建的用户信息
  }
  ```

### **3. @DeleteMapping：处理“删除”请求（删除资源）**

- **对应HTTP方法**：`DELETE`

- **核心作用**：从服务器**删除指定资源**（如删除用户、删除订单）。

- 特点

  ：

  - 通常通过URL路径参数指定要删除的资源ID（如 `/users/123`）。
  - 操作具有破坏性，需谨慎使用，建议在权限校验后执行。

- 示例

  ：

  ```
  @DeleteMapping("/users/{id}")  // URL: /users/123
  public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
      userService.deleteById(id);  // 删除ID=123的用户
      return ResponseEntity.noContent().build();  // 返回204无内容状态
  }
  ```

### **三者对比总结表**

| **维度**     | **@GetMapping**        | **@PostMapping**           | **@DeleteMapping**          |
| ------------ | ---------------------- | -------------------------- | --------------------------- |
| **HTTP方法** | `GET`                  | `POST`                     | `DELETE`                    |
| **核心操作** | 查询资源（读）         | 创建资源（增）             | 删除资源（删）              |
| **参数传递** | URL明文（QueryString） | 请求体（Body）             | URL路径参数（PathVariable） |
| **安全性**   | 较低（参数可见）       | 较高（参数隐藏）           | 需权限控制                  |
| **幂等性**   | 是（多次请求结果一致） | 否（多次请求可能重复创建） | 是（多次删除结果一致）      |

### **扩展说明**

- 三者均为 **@RequestMapping** 的简化版，例如 `@GetMapping("/users")` 等价于 `@RequestMapping(value = "/users", method = RequestMethod.GET)`。
- 除这三个注解外，Spring MVC还提供 **@PutMapping**（更新资源，对应 `PUT` 方法），共同构成RESTful API的常用操作（CRUD）。

