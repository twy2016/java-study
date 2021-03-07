请求实体
```java
@Data
@EqualsAndHashCode(callSuper = false)
@TableName("test")
public class Test implements Serializable {

    private static final long serialVersionUID = 1L;

    @TableId(value = "id", type = IdType.AUTO)
    private Integer id;

    private String name;

    private LocalDateTime createTime;

}
```
测试请求：
```java
@RestController
@RequestMapping("/test")
@AllArgsConstructor
public class TestController {

    private final TestService testService;

    @PostMapping("save1")
    public boolean save1(@RequestBody Test test) {
        return testService.save(test);
    }

    @PostMapping("save2")
    public boolean save2(@RequestParam String name, @RequestParam LocalDateTime createTime) {
        Test test = new Test();
        test.setName(name);
        test.setCreateTime(createTime);
        return testService.save(test);
    }
    
    @GetMapping("save3")
    public boolean save3(Test test) {
        return testService.save(test);
    }
}
```
### @RequestParam与@RequestBody区别
#### @RequestParam
GET/POST请求都可以使用，默认是必传参数，如果不传则会报错`Required parameter 'XXX' is not present`，如果是非必传参数需要加上`@RequestParam(required = false)`，Get请求要传一个对象时，直接`Test test`，实体类接收即可
@RequestBody
只有POST请求才可以使用
### 两者对日期格式的支持
#### @RequestBody


1.日期参数带T
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1613660186199-b0c6da3d-53e7-4789-bcd4-b76ae0e1a73d.png#align=left&display=inline&height=493&margin=%5Bobject%20Object%5D&name=image.png&originHeight=493&originWidth=830&size=43754&status=done&style=none&width=830)
2.添加自定义格式转换
```java
@JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss")
private LocalDateTime createTime;
```
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1613660879448-7413e6d0-7e67-4376-a0e2-36f9ffbe9179.png#align=left&display=inline&height=472&margin=%5Bobject%20Object%5D&name=image.png&originHeight=472&originWidth=822&size=44000&status=done&style=none&width=822)
3.全局配置处理(支持Date日期类型，不支持LocalDateTime)
```yaml
spring:
  jackson:
    time-zone: GMT+8
    date-format: yyyy-MM-dd HH:mm:ss
```
#### @RequestParam
在请求参数前添加`@DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss")`即可
```java
    @PostMapping("save2")
    public boolean save2(@RequestParam(required = false) String name, @RequestParam @DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss") LocalDateTime createTime) {
        Test test = new Test();
        test.setName(name);
        test.setCreateTime(createTime);
        return testService.save(test);
    }
```
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1613662082438-b9e0901c-4fac-4522-890e-3dae2d5f5926.png#align=left&display=inline&height=622&margin=%5Bobject%20Object%5D&name=image.png&originHeight=622&originWidth=832&size=50427&status=done&style=none&width=832)
#### 直接实体传参
Get请求直接实体传参时，需要加上`@DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss")`
```java
@DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss")
private LocalDateTime createTime;
```


