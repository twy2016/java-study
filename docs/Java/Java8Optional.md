核心用法为判断空值，简化if-else判断
```java
// 允许传递为 null 参数
Optional<Integer> test = Optional.ofNullable(1);
// 不允许传递为 null 参数，否则会报空指针异常
Optional<Integer> test1 = Optional.of(1);

//常用的链式方法
orElse();
orElseGet();
orElseThrow();
```
```java
public static void main(String[] args) {
    Integer value1 = null;
    Integer value2 = new Integer(10);
    Integer result = Optional.ofNullable(value2).orElse(setNum());
    System.out.println("第一个参数为空则设置值:" + result);
    Integer result2 = Optional.ofNullable(value2).orElseGet(() -> setNum());
    System.out.println("第一个参数为空则设置值:" + result2);
    Optional.ofNullable(value1).orElseThrow(NullPointerException::new);

}

private static Integer setNum() {
    System.out.println("设置值");
    return 100;
}

返回结果：
设置值
第一个参数为空则设置值:10
第一个参数为空则设置值:10
Exception in thread "main" java.lang.NullPointerException
	at java.util.Optional.orElseThrow(Optional.java:290)
	at com.twy.featurejava.streamapi.OptionalApi.main(OptionalApi.java:34)
```
`orElse()` 它的工作方式非常直接，如果有值则返回该值，否则返回传递给它的参数值
`orElseGet()` 这个方法会在有值的时候返回值，如果没有值，它会执行作为参数传入的 Supplier(供应者) 函数式接口，并将返回其执行结果
两者区别是：orElse（）一定会执行，orElseGet()只有在入参不是空时才会执行
`orElseThrow()` 它会在对象为空的时候抛出异常，而不是返回备选的值
