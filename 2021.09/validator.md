| 验证注解          | 验证的数据类型                                               | 说明                                                         |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| @NotNull          | 任意类型                                                     | 验证注解的元素不是null                                       |
| @Null             | 任意类型                                                     | 验证注解的元素是null                                         |
| @NotBlank         | CharSequence子类型                                           | 验证注解的元素不为空，只适用于字符串类型                     |
| @NotEmpty         | CharSequence子类型、Collection、Map、数组                    | 验证注解的元素值不为null且不为空（字符串长度不为0、集合大小不为0） |
| @Past             | java.util.Date,java.util.Calendar等日期类型                  | 验证注解的元素值（日期类型）比当前时间早                     |
| @Future           | 同@Past                                                      | 验证注解的元素值（日期类型）比当前时间晚                     |
| @PastOrPressent   | 同@Past                                                      | 今日或今日之前的日期                                         |
| @FutureOrPressent | 同@Past                                                      | 今日或今日之后的日期                                         |
| @Length           | CharSequence子类型                                           | 验证注解的元素值长度在min和max区间内                         |
| @Range            | BigDecimal,BigInteger,CharSequence, byte, short, int, long等原子类型和包装类型 | 验证注解的元素值在最小值和最大值之间                         |
| @Size             | 字符串、Collection、Map、数组等                              | 验证注解的元素值的在min和max（包含）指定区间之内，如字符长度、集合大小 |
| @Email            | CharSequence子类型                                           | 验证注解的元素值是Email，也可以通过regexp和flag指定自定义的email格式 |
| @Pattern          | CharSequence子类型                                           | 验证注解的元素值与指定的正则表达式匹配                       |
| @Min              | BigDecimal，BigInteger, byte,short, int, long，等任何Number或CharSequence（存储的是数字）子类型 | 验证注解的元素值大于等于@Min指定的值                         |
| @Max              | 同@Min                                                       | 验证注解的元素值小于等于@Max指定的值                         |
| @Digits           | 同@Min                                                       | 验证注解的元素值的整数位数和小数位数上限                     |
| @AssertTrue       | Boolean,boolean                                              | 验证注解的元素值是true                                       |
| @AssertFalse      | Boolean,boolean                                              | 验证注解的元素值是false                                      |

