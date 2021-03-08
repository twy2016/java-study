

# SpringBoot(2)Json数据的处理

> 本文介绍SpringBoot的对Json数据的自定义配置

### 1.SpringBoot默认对Json的处理

SpringBoot默认使用jackson对数据进行处理，我们先看下默认的处理方式

#### 1.1创建User实体类

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private int id;
    private String username;
    private String password;
    private Date birthday;
}
```

#### 1.2创建Controller类

```java
@RestController
@RequestMapping("/user")
public class UserController {

    @GetMapping(value = "/one")
    public User getUser() {
        User user = new User(1, "唐万言", "123456", new Date());
        return user;
    }

    @GetMapping(value = "/list")
    public List<User> getUserList() {
        User u1 = new User(1, "唐万言", "123456", new Date());
        User u2 = new User(2, "测试", null, new Date());
        List<User> list = new ArrayList<>();
        list.add(u1);
        list.add(u2);
        return list;
    }
}
```

#### 1.3测试返回结果

请求：127.0.0.1:8081/user/one

```json
{
    "id": 1,
    "username": "唐万言",
    "password": "123456",
    "birthday": "2021-03-08T14:06:46.845+00:00"
}
```

请求：127.0.0.1:8081/user/list

```json
[
    {
        "id": 1,
        "username": "唐万言",
        "password": "123456",
        "birthday": "2021-03-08T14:08:01.698+00:00"
    },
    {
        "id": 2,
        "username": "测试",
        "password": null,
        "birthday": "2021-03-08T14:08:01.698+00:00"
    }
]
```

#### 1.4 自定义json的格式化配置

从返回值可以看出返回值都可以转成相应的 json 格式，但是格式都是默认，我们可以自己写一个配置类修改返回的格式

```java
@Configuration
public class JsonConfig {

    @Bean
    ObjectMapper objectMapper(){
        ObjectMapper objectMapper = new ObjectMapper();
        //格式化日期
        objectMapper.setDateFormat(new SimpleDateFormat("yyyy/MM/dd"));
        //null值转为空字符串
        objectMapper.getSerializerProvider().setNullValueSerializer(new JsonSerializer<Object>() {
            @Override
            public void serialize(Object o, JsonGenerator jsonGenerator, SerializerProvider serializerProvider) throws IOException {
                jsonGenerator.writeString("");
            }
        });
        return objectMapper;
    }
}
```

请求：127.0.0.1:8081/user/list

```json
[
    {
        "id": 1,
        "username": "唐万言",
        "password": "123456",
        "birthday": "2021/03/08"
    },
    {
        "id": 2,
        "username": "测试",
        "password": "",
        "birthday": "2021/03/08"
    }
]
```

### 2.使用FastJson的设置

#### 2.1 引入依赖

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.35</version>
</dependency>
```

#### 2.2 添加配置

fastjson需要添加配置，不然json还是用默认的jackson处理

```java
@Configuration
public class FastJsonConfiguration {

    @Bean
    FastJsonHttpMessageConverter fastJsonHttpMessageConverter(){
        FastJsonHttpMessageConverter converter = new FastJsonHttpMessageConverter();
        FastJsonConfig config = new FastJsonConfig();
        converter.setFastJsonConfig(config);
        config.setDateFormat("yyyy-MM-dd");
        config.setSerializerFeatures(SerializerFeature.WriteNullStringAsEmpty);
        converter.setDefaultCharset(Charset.forName("UTF-8"));
        //解决中文乱码问题
        List<MediaType> mediaTypes = new ArrayList<>();
        mediaTypes.add(MediaType.APPLICATION_JSON);
        converter.setSupportedMediaTypes(mediaTypes);
        return converter;
    }
}
```
请求：127.0.0.1:8081/user/list
```json
[
    {
        "birthday": "2021-03-08",
        "id": 1,
        "password": "123456",
        "username": "唐万言"
    },
    {
        "birthday": "2021-03-08",
        "id": 2,
        "password": "",
        "username": "测试"
    }
]
```

