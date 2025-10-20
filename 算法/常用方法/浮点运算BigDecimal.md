# 加减乘除

```java
import java.math.BigDecimal;

public class BigDecimalExample {
    public static void main(String[] args) {
        BigDecimal num1 = new BigDecimal("10.5");
        BigDecimal num2 = new BigDecimal("5.25");

        // 加法
        BigDecimal sum = num1.add(num2);
        System.out.println("和：" + sum);

        // 减法
        BigDecimal difference = num1.subtract(num2);
        System.out.println("差：" + difference);

        // 乘法
        BigDecimal product = num1.multiply(num2);
        System.out.println("积：" + product);

        // 除法
        BigDecimal quotient = num1.divide(num2, 2, RoundingMode.HALF_UP);
        System.out.println("商：" + quotient);
    }
}
```

# 除法的精度保留和四舍五入规则

`BigDecimal` 类的 `divide` 方法用于执行高精度的除法运算。该方法的基本签名如下：

```java
public BigDecimal divide(BigDecimal divisor, int scale, int roundingMode)
```

1. divisor

   :

   - 类型: `BigDecimal`
   - 说明: 被除数，即你要除以的数。

2. scale

   :

   - 类型: `int`
   - 说明: 指定结果的小数位数。这个参数决定了结果中保留多少位小数。

3. roundingMode

   :

   - 类型: `RoundingMode` (枚举类型)
   - 说明: 指定舍入模式，用于处理在除法运算中产生的小数部分。Java 提供了多种舍入模式，常用的包括：
     - `RoundingMode.UP`: 向上舍入。
     - `RoundingMode.DOWN`: 向下舍入。
     - `RoundingMode.HALF_UP`: 四舍五入（常用）。
     - `RoundingMode.HALF_DOWN`: 五舍六入。
     - `RoundingMode.HALF_EVEN`: 银行家舍入法（即如果最后一位是5，则看前一位是奇数还是偶数，奇数进位，偶数不进位）。

注意：从 Java 5 开始，推荐使用 `RoundingMode` 枚举代替旧的 `BigDecimal.ROUND_XXX` 常量。

# 保留两位有效数字

```java
import java.math.BigDecimal;
import java.math.RoundingMode;

double input = 3.1415926;
BigDecimal bd = new BigDecimal(input);
String result = bd.setScale(2, RoundingMode.HALF_UP).toString();
 
// 3.00->3;  3.010->3.01
result = result.replaceAll("\\\\.0+$|0+$", "");
System.out.println(result); // 输出：3.14
```