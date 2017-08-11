## 2017年8月3号
Markdown中的换行：  
空格空格＋回车

## 2017年8月11号
抛出service中捕获的异常，这样，外层才能捕获异常。

```java
//用这种方式，当Object为String类型时，会产生类型转换异常
(boolean)Object == true;

//用这种方式，则不会有问题
Boolean.parseBoolean(Object) == true;
```
***
Linux中快捷命令在 ~/.bashrc 中创建  
vi ~/.bashrc 即可编辑。

***
对数据库中数据进行加减时，最好直接在sql中进行加减操作，防止并发，比如：  
UPDATE tablename SET column = column + addition;