- # FastJson


## Json数据格式回顾

### 什么是json

JSON:(JavaScript Object Notation, JS 对象简谱) 是一种轻量级的数据交换格式。它基于 ECMAScript(欧洲计算机协会制定的js规范)的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。目前,Json处于数据交换语言的王者地位.

### Json数组格式

Json的数据本身是数组,中括号包裹,数组的元素之间逗号分开.数组元素的数据类型没有限制.

```javascript
var jsonArray = ["元素1","元素2","元素3"]; //定义数组格式json
console.log(jsonArray[0]); //访问json数组的元素
for(var i = 0 ; i < jsonArray.length ; i++){
    console.log(jsonArray[i]); //遍历数组,访问每个元素
}
```

### Json对象格式

Json的数据本身是对象,大括号包裹.对象采用键值对形式存储,键固定为字符串类型,值是任意类型的数据.键和值使用冒号分开.

```javascript
var jsonObject = {"k1":"v1","k2":"v2","k3":"v3"}; //定义对象格式json
console.log(jsonObject.k1); //取出键k1对应的值
```

### 数组对象相互嵌套格式

1. 数组中的元素是对象

   ```javascript
   var jsonArray = [
       {"k1":"v1"},{"k2":"v2"}
   ]; // 定义数组格式json,数组元素是对象
   console.log(jsonArray[0].k1); //访问数组0索引的元素,该元素的键k1对应的值
   ```

2. 对象中的值是数组

   ```javascript
   var jsonObject = {
       "k1":["元素1","元素2"],
       "k2":["元素1","元素2"]
   }; // 定义对象格式json,键是字符串类型,值是数组
   console.log(jsonObject.k1[0]); //访问对象的键是k1,对于的值为数组,数组的0索引元素
   ```

3. 你中有我,我中有你

   ```javascript
   var json = {
       "k1":[
         "元素1",{"key1":"value1"},{"key2":"value2"}  
       ],
       "k2":[
           {"key1":"value1"}
       ]
   }; //定义对象格式json,键是字符串,值是数组,数组的元素是对象
   console.log(json.k1[1].key1); //访问json对象的键k1,对应的是数组,访问数组的1索引,数组的1索引上的元素是对象,访问key1键对应的值
   ```

## FastJson介绍

FastJson 是阿里巴巴的开源JSON解析库,它可以解析 JSON 格式的字符串，支持将 Java Bean 序列化为 JSON 字符串，也可以从 JSON 字符串反序列化到 JavaBean。

**Fastjson 的优点**

- **速度快**
   fastjson相对其他JSON库的特点是快，从2011年fastjson发布1.1.x版本之后，其性能从未被其他Java实现的JSON库超越。
- **使用广泛**
   fastjson在阿里巴巴大规模使用，在数万台服务器上部署，fastjson在业界被广泛接受。在2012年被开源中国评选为最受欢迎的国产开源软件之一。
- **测试完备**
   fastjson有非常多的testcase，在1.2.11版本中，testcase超过3321个。每次发布都会进行回归测试，保证质量稳定。
- **使用简单**
   fastjson的 API 十分简洁。
- **功能完备**
   支持泛型，支持流处理超大文本，支持枚举，支持序列化和反序列化扩展。

## FastJson序列化API

序列化 : 是指将Java对象转成json格式字符串的过程.JavaBean对象,List集合对象,Map集合,为应用最广泛的.

- JSON.toJSONString

  - 序列化Java对象

  ```java
  public void objectToJson(){
      Student student = new Student();
      student.setId(1);
      student.setName("张三");
      student.setAge(20);
      student.setAddress("北京市");
      student.setEmail("zs@sina.com");
      String jsonString = JSON.toJSONString(student);
      System.out.println(jsonString);
  }
  ```

- JSON.toJSONString

  - 序列化List集合

  ```java
  public void listToJson(){
      Student student = new Student();
      student.setId(1);
      student.setName("张三");
      student.setAge(20);
      student.setAddress("北京市");
      student.setEmail("zs@sina.com");
  
      Student student2 = new Student();
      student2.setId(2);
      student2.setName("张三2");
      student2.setAge(22);
      student2.setAddress("北京市2");
      student2.setEmail("zs2@sina.com");
  
      List<Student> list = new ArrayList<Student>();
      list.add(student);
      list.add(student2);
      String jsonString = JSON.toJSONString(list);
      System.out.println(jsonString);
  }
  ```

- JSON.toJSONString

  - 序列化Map集合

  ```java
  public void mapToJson(){
      Student student = new Student();
      student.setId(1);
      student.setName("张三");
      student.setAge(20);
      student.setAddress("北京市");
      student.setEmail("zs@sina.com");
  
      Student student2 = new Student();
      student2.setId(2);
      student2.setName("张三2");
      student2.setAge(22);
      student2.setAddress("北京市2");
      student2.setEmail("zs2@sina.com");
      Map<String,Student> map = new HashMap<String, Student>();
      map.put("s1",student);
      map.put("s2",student2);
      String jsonString = JSON.toJSONString(map);
      System.out.println(jsonString);
  }
  ```

## FashJson反序列化API

- JSON.parseObject

  - 反序列化Java对象

  ```java
  public void jsonToObject(){
      String jsonString = "{\"address\":\"北京市\",\"age\":20,\"email\":\"zs@sina.com\",\"id\":1,\"name\":\"张三\"}";
      Student student = JSON.parseObject(jsonString, Student.class);
      System.out.println(student);
  }
  ```

- JSON.parseArray

  - 反序列化List集合

  ```java
  public void jsonToList(){
      String jsonString = "[{\"address\":\"北京市\",\"age\":20,\"email\":\"zs@sina.com\",\"id\":1,\"name\":\"张三\"},{\"address\":\"北京市2\",\"age\":22,\"email\":\"zs2@sina.com\",\"id\":2,\"name\":\"张三2\"}]";
      List<Student> list = JSON.parseArray(jsonString,Student.class);
      for (int i = 0; i < list.size(); i++) {
          Student student =  list.get(i);
          System.out.println(student);
      }
  }
  ```

- JSON.parseObject

  - 反序列化Map集合

  ```java
  public void jsonToMap(){
      String jsonString = "{\"s1\":{\"address\":\"北京市\",\"age\":20,\"email\":\"zs@sina.com\",\"id\":1,\"name\":\"张三\"},\"s2\":{\"address\":\"北京市2\",\"age\":22,\"email\":\"zs2@sina.com\",\"id\":2,\"name\":\"张三2\"}}";
      Map<String,Student> parse = JSON.parseObject(jsonString,new TypeReference<Map<String,Student>>(){});
  
      for(String s : parse.keySet()){
      	System.out.println(s + ":::"+parse.get(s));
      }
  }
  ```

## SerializerFeature枚举

  该枚举支持序列化的一些特性数据定义.

- 枚举常量 WriteMapNullValue 序列化为null的字段

  ```java
  public void testSerializerFeature(){
      Student student = new Student();
      student.setId(1);
      student.setName("张三");
      student.setAge(20);
      //student.setAddress("北京市");
      student.setEmail("zs@sina.com");
      String jsonString = JSON.toJSONString(student, SerializerFeature.WriteMapNullValue);
      System.out.println(jsonString);
  }
  ```

- 枚举常量 WriteNullStringAsEmpty 字段为null,序列化为""

  ```java
  public void testSerializerFeature(){
      Student student = new Student();
      student.setId(1);
      student.setName("张三");
      student.setAge(20);
      //student.setAddress("北京市");
      student.setEmail("zs@sina.com");
      String jsonString = JSON.toJSONString(student, SerializerFeature.WriteNullStringAsEmpty);
      System.out.println(jsonString);
  }
  ```

- 枚举常量 WriteNullNumberAsZero 字段为null,序列化为0

  ```java
  public void testSerializerFeature(){
      Student student = new Student();
      student.setId(1);
      student.setName("张三");
      //student.setAge(20);
      student.setAddress("北京市");
      student.setEmail("zs@sina.com");
      String jsonString = JSON.toJSONString(student, SerializerFeature.WriteNullNumberAsZero);
      System.out.println(jsonString);
  }
  ```

- 枚举常量 WriteNullBooleanAsFalse 字段值为null 输出false

- 枚举常量 WriteDateUseDateFormat  格式化日期格式

- 枚举常量 PrettyFormat格式化输出

  ```java
  public void testSerializerFeature2(){
      Person person = new Person();
      //person.setFlag(true);
      person.setDate(new Date());
      String jsonString = JSON.toJSONString(person,SerializerFeature.WriteNullBooleanAsFalse,
    SerializerFeature.WriteDateUseDateFormat,SerializerFeature.PrettyFormat);
      System.out.println(jsonString);
  }
  ```

## @JSonField注解

该注解作用于方法上,字段上和参数上.可在序列化和反序列化时进行特性功能定制.

- 注解属性 : name 序列化后的名字
- 注解属性 : ordinal序列化后的顺序
- 注解属性 :  format 序列化后的格式
- 注解属性 :  serialize 是否序列化该字段
- 注解属性 : deserialize 是否反序列化该字段
- 注解属性 : serialzeFeatures 序列化时的特性定义

## @ JSonType注解

该注解作用于类上,对该类的字段进行序列化和反序列化时的特性功能定制.

- 注解属性 : includes 要被序列化的字段.
- 注解属性 : orders 序列化后的顺序.
- 注解属性 : serialzeFeatures 序列化时的特性定义.

## SpringMVC集成 FastJson

SpringMVC框架中,默认使用的json序列化工具是jackson,我们需要在SpringMVM的配置文件中,配置消息转换器,由jackson切换到FastJson.

- 环境搭建

  - 创建Web项目
  - 导入相关的依赖jar包

  ```xml
   	<!-- FastJson -->
     <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>1.2.62</version>
      </dependency>
      <!-- 数据库驱动 -->
      <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.46</version>
      </dependency>
      <!-- spring框架 -->
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.0.2.RELEASE</version>
      </dependency>
  	<!--  springMVC -->
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.0.2.RELEASE</version>
      </dependency>
      <!--  spring jdbctemplate -->
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.0.2.RELEASE</version>
      </dependency>
  
  	<!-- 德鲁伊连接池 -->
      <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.1.10</version>
      </dependency>
  
      <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
      </dependency>
  
      <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.8</version>
      </dependency>
    </dependencies>
  ```
  
- 配置springmvc.xml

  ```xml
  <mvc:annotation-driven> 
      <mvc:message-converters register-defaults="false">
          <!-- FastJson的消息转换器-->
          <bean id = "fastJson" class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter">
              <!-- FastJsonHttpMessageConverter类属性赋值-->
              <property name="supportedMediaTypes">
                  <list>
                      <value>application/json;charset=UTF-8</value>
                  </list>
              </property>
          </bean>
      </mvc:message-converters>
  </mvc:annotation-driven>
  ```

  