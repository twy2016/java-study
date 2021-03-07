### 结论
- **任何执行try 或者catch中的return语句之前，都会先执行finally语句**
- **如果finally中有return语句，那么程序就return了，所以finally中的return是一定会被return的**
- **return返回是最后执行的，所以finally语句是在retrun返回之前执行的**
### 测试代码
```java
public class ReturnTest {

    public static void main(String[] args) {
        System.out.println("返回结果：" + method1());
        System.out.println("返回结果：" + method2());
        System.out.println("返回结果：" + method3());
    }

    public static int method1() {
        try {
            int i = 1 / 0;
        } catch (Exception e) {
            System.out.println("catch方法");
            return 1;
        } finally {
            System.out.println("finally方法");
            return 2;
        }
    }

    public static Test method2() {
        Test test = new Test(1, "aaa");
        try {
            return test;
        } catch (Exception e) {
            System.out.println("catch方法");
            test.setId(2);
            return test;
        } finally {
            System.out.println("finally方法");
            test.setId(3);
            test.setName("ccc");
        }
    }

    public static String method3() {
        String str = "aaa";
        try {
            str = str + "111";
            return str;
        } catch (Exception e) {
            System.out.println("catch方法");
            str = str + "222";
            return str;
        } finally {
            System.out.println("finally方法");
            str = str + "333";
        }
    }
}
```
返回结果：
```bash
catch方法
finally方法
返回结果：2
finally方法
返回结果：Test(id=3, name=ccc)
finally方法
返回结果：aaa111
```
1.不管有没有出现异常，finally块中代码都会执行
2.当try和catch中有return时，finally仍然会执行
3.如果finally中没有return语句，但是改变了要返回的值，这里有点类似与引用传递和值传递的区别，分以下两种情况：
1）如果return的数据是基本数据类型或文本字符串，则在finally中对该基本数据的改变不起作用，try中的return语句依然会返回进入finally块之前保留的值

2）如果return的数据是引用数据类型，而在finally中对该引用数据类型的属性值的改变起作用，try中的return语句返回的就是在finally中改变后的该属性的值

5.finally中最好不要包含return，否则程序会提前退出，返回值不是try或catch中保存的返回值
