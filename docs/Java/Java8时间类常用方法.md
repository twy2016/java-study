`Java 8` 为处理本地的日期时间提供了三个类 `LocalDate 、LocalTime` 和 `LocalDateTime`。分别用于处理 本地日期、本地时间 和 本地日期时间。
### 获取当前时间
```java
/**
 * @author gongpeng
 * @date 2021/1/16 15:58
 */
public class NewDateApi {

    public static void main(String[] args) {
        getNow();
    }

    /**
     * 获取当前时间
     */
    public static void getNow(){
        LocalDate date = LocalDate.now();
        LocalTime time = LocalTime.now();
        LocalDateTime dateTime = LocalDateTime.now();
        System.out.println(date);
        System.out.println(time);
        System.out.println(dateTime);
    }
}

返回结果：
当前日期:2021-01-16
当前时间:16:56:28.965
当前日期时间:2021-01-16T16:56:28.965
```
### 获取详细的时间信息
```java
public static void getDetailDate() {
    LocalDateTime now = LocalDateTime.now();
    System.out.println("当前年份:" + now.getYear());
    System.out.println("当前月份:" + now.getMonth());
    System.out.println("当前月份的值:" + now.getMonthValue());
    System.out.println("当前小时:" + now.getHour());
    System.out.println("当前分钟:" + now.getMinute());
    System.out.println("当前秒:" + now.getSecond());
    System.out.println("当前年份的天数:" + now.getDayOfYear());
    System.out.println("当前月份的天数:" + now.getDayOfMonth());
    System.out.println("当前时间是星期几:" + now.getDayOfWeek());
}

返回结果：
当前年份:2021
当前月份:JANUARY
当前月份的值:1
当前小时:17
当前分钟:9
当前秒:5
当前年份的天数:16
当前月份的天数:16
当前周的天数:SATURDAY
```
### with方法
修改日期得到一个新的日期实例，对原有的日期也不会有改变
```java
public static void with() {
    LocalDateTime now = LocalDateTime.now();
    LocalDateTime dateTime = now.withYear(2020).withMonth(10).withDayOfMonth(12)
        .withHour(10).withMinute(15).withSecond(20);
    System.out.println("当前时间:" + now);
    System.out.println("当前时间:" + dateTime);
}

返回结果：
当前时间:2021-01-16T17:23:07.293
当前时间:2020-10-12T10:15:20.293
```
### of方法
指定日期
```java
public static void of() {
    LocalDate date = LocalDate.of(2020, 1, 1);
    LocalTime time = LocalTime.of(12, 11, 01);
    LocalDateTime dateTime = LocalDateTime.of(2021, 1, 12, 11, 11, 11);
    System.out.println("当前日期:" + date);
    System.out.println("当前时间:" + time);
    System.out.println("当前日期时间:" + dateTime);
}

返回结果：
当前日期:2020-01-01
当前时间:12:11:01
当前日期时间:2021-01-12T11:11:11
```
### 字符串解析为日期
```java
public static void parse() {
    LocalDateTime datetime = LocalDateTime.parse("2020-11-11T11:58:00");
    System.out.println("日期时间是:" + datetime);
    LocalDate date = LocalDate.parse("2020-11-10");
    System.out.println("日期是: " + date);
    LocalTime time = LocalTime.parse("11:11:11");
    System.out.println("时间是: " + time);
    LocalDate dateParse = LocalDate.parse("20210116", DateTimeFormatter.BASIC_ISO_DATE);
    System.out.println("字符串转换为日期:" + dateParse);
}

返回结果：
日期时间是:2020-11-11T11:58
日期是: 2020-11-10
时间是: 11:11:11
字符串转换为日期:2021-01-16
```
### 时区
```java
public static void zone() {
    ZonedDateTime now = ZonedDateTime.now();
    System.out.println("当前日期时间:" + now);
    ZonedDateTime dateTime = ZonedDateTime.parse("2020-11-11T11:58:00+08:00");
    System.out.println("当前日期时间:" + dateTime);
    LocalDate date = now.toLocalDate();
    System.out.println("本地日期是:" + date);
    LocalTime time = now.toLocalTime();
    System.out.println("本地时间是:" + time);
    ZoneId nowZoneId = now.getZone();
    ZoneId zoneId = ZoneId.systemDefault();
    System.out.println("当前时区:" + nowZoneId);
    System.out.println("当前时区:" + zoneId);
    //时区设置
    ZonedDateTime dateTimeInTokyo = ZonedDateTime.of(LocalDateTime.now(), ZoneId.of("Asia/Tokyo"));
    System.out.println("日本时间:" + dateTimeInTokyo);
}

返回结果：
当前日期时间:2021-01-16T23:01:31.605+08:00[Asia/Shanghai]
当前日期时间:2020-11-11T11:58+08:00
本地日期是:2021-01-16
本地时间是:23:01:31.605
当前时区:Asia/Shanghai
当前时区:Asia/Shanghai
日本时间:2021-01-16T23:01:31.606+09:00[Asia/Tokyo]
```
### 格式化
```java
public static void formatter() {
    String now = LocalDateTime.now().format(DateTimeFormatter.ISO_DATE_TIME);
    String now2 = LocalDateTime.now().format(DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss"));
    System.out.println("当前时间:" + now);
    System.out.println("当前时间:" + now2);
}

返回结果：
当前时间:2021-01-16T23:01:31.606
当前时间:2021/01/16 23:01:31
```
### 时间计算
```java
public static void calculate() {
    LocalDate date = LocalDate.now();
    //日期计算
    date.plus(1, ChronoUnit.DAYS);
    date.minus(1, ChronoUnit.DAYS);

    LocalTime time = LocalTime.now();
    //时间计算
    time.plus(1, ChronoUnit.HOURS);
    time.minus(1, ChronoUnit.HOURS);

    //判断是不是闰年
    boolean leapYear = date.isLeapYear();
    System.out.println("2021年是不是闰年:" + leapYear);

    //计算两个日期间的年数、月数、天数
    LocalDate one = LocalDate.of(2019, 1, 1);
    LocalDate two = LocalDate.now();
    Period period = Period.between(one, two);
    int years = period.getYears();
    int months = period.getMonths();
    int days = period.getDays();
    System.out.println("年数" + years);
    System.out.println("月数" + months);
    System.out.println("天数" + days);
    //实际计算相隔天数
    long result = two.toEpochDay() - one.toEpochDay();
    System.out.println("2019年1月1号至今已有" + result + "天");

    //日期比较
    LocalDate today = LocalDate.now();
    LocalDate tomorrow = today.plus(1, ChronoUnit.DAYS);
    LocalDate yesterday = today.minus(1, ChronoUnit.DAYS);
    System.out.println(today.isBefore(tomorrow));
    System.out.println(today.isAfter(yesterday));
    System.out.println(today.isEqual(yesterday));
}

返回结果：
2021年是不是闰年:false
年数2
月数0
天数15
2019年1月1号至今已有746天
true
true
false
```
