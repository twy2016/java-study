lambda表达式算是Java8的最重要的一个特性，学会使用它，能使我们的代码更加简洁、漂亮、优雅。


lambda 表达式的语法格式如下：
(parameters) -> expression 或 (parameters) ->{ statements; }


### 1.匿名内部类
用() -> {}代码块替代了匿名内部类
```java
new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println(Thread.currentThread());
    }
}).start();

new Thread(()->{
    System.out.println(Thread.currentThread());
}).start();
```


### 2.集合的遍历forEach方法
User.java
```java
@Data
public class User {
    private String name;
    private int age;
    private String address;

    public User(String name, int age, String address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }
}
```


类名::方法名
```java
List<User> list = new ArrayList<>();
list.add(new User("twy",25,"杭州"));
list.add(new User("wxx",23,"芜湖"));
list.add(new User("gp",18,"芜湖"));
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}

list.forEach(item-> System.out.println(item));
list.forEach(System.out::println);
```


### 3.集合的过滤filter方法
按照条件过滤筛选集合的数据
```java
list.stream().filter(user -> user.getAge()==25).forEach(System.out::println);

输出结果：
User(name=twy, age=25, address=杭州)
```


### 4.map方法
对集合进行遍历，可以对其每个元素进行操作，转化为其他对象，如将集合中的每个user的年龄增加1岁
```java
list.stream().map(user -> new User(user.getName(), user.getAge() + 1, user.getAddress())).forEach(System.out::println);

输出结果：
User(name=twy, age=26, address=杭州)
User(name=wxx, age=24, address=芜湖)
User(name=gp, age=19, address=芜湖)
```


### 5.reduce方法
对集合进行遍历，将其中元素按照传入的逻辑计算合并为一个
若未定义了初始值则从第一个元素计算，否则则从初始值开始计算
```java
List<Integer> item = Arrays.asList(18, 20, 22, 25, 30);
int total1 = item.stream().reduce((sum, e) -> sum + e).get();//未定义初始值
int total2 = item.stream().reduce(5, (sum, e) -> sum + e);//定义初始值
System.out.println(total1);//115
System.out.println(total2);//120
```


### 6.collect方法
将操作后的对象转化为新的对象
```java
//转换为新的list
List newList = list.stream().map(user -> new User(user.getName(), user.getAge() + 1, user.getAddress())).collect(Collectors.toList());
newList.forEach(System.out::println);

输出结果：
User(name=twy, age=26, address=杭州)
User(name=wxx, age=24, address=芜湖)
User(name=gp, age=19, address=芜湖)

//转换为map
Map<String, Integer> map = list.stream().map(user -> new User(user.getName(), user.getAge() + 1, user.getAddress())).collect(Collectors.toMap(User::getName, User::getAge));
        map.forEach((k,v)-> System.out.println("key="+k+"-----value="+v));

//当map的key出现重复值
list.add(new User("gp", 20, "芜湖"));
 Map<String, Integer> map = list.stream().collect(Collectors.toMap(User::getName, User::getAge, (v1, v2) -> v2));

输出结果：
key=wxx-----value=24
key=twy-----value=26
key=gp-----value=19
```


### 7.limit方法
设置结果集返回的数据条数
```java
list.stream().limit(1).forEach(System.out::println);

输出结果：
User(name=twy, age=25, address=杭州)
```


### 8.sorted方法
通过sorted方法，可以按自定义的规则，对数据进行排序
```java
list.stream().sorted((u1,u2)->(u1.getAge()-u2.getAge())).forEach(System.out::println);
```


### 9.max、min方法
通过max、min方法，可以获取集合中最大、最小的对象
```java
list.stream().max(Comparator.comparing(User::getAge)).get()
list.stream().min(Comparator.comparing(User::getAge)).get()
```
