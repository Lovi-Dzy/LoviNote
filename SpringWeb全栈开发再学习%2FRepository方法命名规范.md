[Spring Data命名规范 CSDN博客](https://blog.csdn.net/zzhongcy/article/details/134372292)



1. 查询动词开头(三者功能一致，推荐用findBy)：

   - findBy
   - readBy
   - getBy

2. 条件关键字连接属

   - GreaterThan


   - LessThan
   - Between
   - Like
   - OrderBy...Desc
   - And/Or

3. 排序与分页规范

   - 排序：使用OrderBy+属性+Asc/Desc(默认Asc升序，可省)
   - 分页：通过参数Pageable实现，需要放在方法参数最后

4. 特殊场景处理

   - 块级属性查询：使用 _ 连接级联属性
   - @Query自定义查询(适用于命名规则无法满足的复杂查询，如多表关联，聚合函数等)
     ```
     @Query("SELECT u FROM User u WHERE u.age > ?1 ORDER BY u.age DESC")  
     List<User> findByAgeGreaterThanCustom(Integer age);  
     ```

#### **五、错误示例与避坑点**

- ❌ 错误：`findByageGreaterThan(...)`（属性名 `age` 首字母未大写）
- ❌ 错误：`findByAgeGreaterThanOrderByAgeDesc(age)`（参数未声明类型）
- ✅ 正确：`List<User> findByAgeGreaterThanOrderByAgeDesc(Integer age);`



```java
Optional<User> findByUsername(String username);
```

Spring Data会根据方法名自动生成查询语句

```java
/**
     * 根据邮箱查找用户
     * 
     * @param email 邮箱地址
     * @return 包含用户的Optional对象
     */
    Optional<User> findByEmail(String email);
    
    /**
     * 根据年龄范围查找用户
     * 
     * @param minAge 最小年龄
     * @param maxAge 最大年龄
     * @return 用户列表
     */
    List<User> findByAgeBetween(Integer minAge, Integer maxAge);
    
    /**
     * 根据用户名模糊查询
     * 
     * @param username 用户名关键字
     * @return 匹配的用户列表
     */
    List<User> findByUsernameLike(String username);
    
    /**
     * 使用@Query注解自定义查询语句
     * 这里使用的是MongoDB的查询语法
     * 
     * @param city 城市名称
     * @return 该城市的用户列表
     */
    @Query("{'address.city': ?0}")
    List<User> findByCity(String city);
    
    /**
     * 根据标签查找用户
     * 
     * @param tag 标签
     * @return 包含该标签的用户列表
     */
    @Query("{'tags': ?0}")
    List<User> findByTag(String tag);
    
    /**
     * 统计某个年龄段的用户数量
     * 
     * @param minAge 最小年龄
     * @param maxAge 最大年龄
     * @return 用户数量
     */
    Long countByAgeBetween(Integer minAge, Integer maxAge);
    
    /**
     * 根据用户名删除用户
     * 
     * @param username 用户名
     */
    void deleteByUsername(String username);
    
    /**
     * 检查用户名是否存在
     * 
     * @param username 用户名
     * @return 如果存在返回true，否则返回false
     */
    Boolean existsByUsername(String username);
    
    /**
     * 检查邮箱是否存在
     * 
     * @param email 邮箱地址
     * @return 如果存在返回true，否则返回false
     */
    Boolean existsByEmail(String email);
    
    /**
     * 查找年龄大于指定值的用户并按年龄降序排列
     * 
     * @param age 年龄
     * @return 用户列表
     */
    List<User> findByAgeGreaterThanOrderByAgeDesc(Integer age);
    
    /**
     * 查找包含所有指定标签的用户
     * 
     * @param tags 标签列表
     * @return 用户列表
     */
    @Query("{'tags': {'$all': ?0}}")
    List<User> findByTagsContainingAll(List<String> tags);
    
    /**
     * 查找创建时间在指定范围内的用户
     * 
     * @param start 开始时间
     * @param end 结束时间
     * @return 用户列表
     */
    List<User> findByCreatedAtBetween(java.time.LocalDateTime start, java.time.LocalDateTime end);
    
    /**
     * 使用正则表达式查找用户名匹配的用户
     * 
     * @param regex 正则表达式
     * @return 用户列表
     */
    @Query("{'username': {'$regex': ?0, '$options': 'i'}}")
    List<User> findByUsernameRegex(String regex);
}
```

