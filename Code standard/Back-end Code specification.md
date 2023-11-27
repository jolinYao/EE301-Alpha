[toc]

# Back-end code specification


## (I) Naming regulations

1. **[Mandatory]** No naming in code can begin or end with an underscore or dollar sign.

```
反例： _name / __name / $Object / name_ / name$ / Object$
```
2. **[Mandatory]** It is strictly forbidden to use Pinyin mixed with English in the naming of the code, and it is not allowed to use Chinese directly.

> Note: Correct English spelling and grammar can make it easier for the reader to understand and avoid ambiguity.
> Note that even pure Pinyin naming should be avoided.

```
反例： DaZhePromotion [打折] / getPingfenByName()  [评分] / int某变量 = 3
正例： alibaba / taobao / youku / hangzhou等国际通用的名称，可视同英文。
```

3. **[Mandatory]** Class names use the UpperCamelCase style and must follow the CamelCase form, with the following exceptions: DO/BO/DTO/VO, etc.

```
正例：MarcoPolo / UserDO / XmlService / TcpUdpDeal /   TaPromotion
反例：macroPolo / UserDo / XMLService / TCPUDPDeal /   TAPromotion
```
4. **[Mandatory]** Method names, parameter names, member variables, and local variables all use the lowerCamelCase style and must follow the camel form.

```
正例： localValue / getHttpMessage() /  inputUserId
```
5. **[Mandatory]** The names of constants are all capitalized, and the words are separated by underscores, so that the semantic expression is complete and clear, and the names are not too long.

```
正例： MAX_STOCK_COUNT
反例： MAX_COUNT
```
6. **[Mandatory]** An abstract class is named starting with Abstract or Base; an exception class is named ending with Exception; and a test class is named starting with the name of the class it is testing and ending with Test.

7. **[Mandatory]** The brackets are part of the array type, which is defined as follows: String [] args;

```
反例：请勿使用String  args[]的方式来定义。
```
8. **[Mandatory]** Do not add is to variables of Boolean type in POJO class, otherwise some frame parsing will cause serialization errors.

```
反例：定义为基本数据类型boolean isSuccess；的属性，
它的方法也是isSuccess()，RPC框架在反向解析的时候，“以为”对应的属性名称是success，导致属性获取不到，进而抛出异
常。
```
9. **[Mandatory]** Package names are uniformly lowercase, with one and only one English word with natural semantics between the dot separators. Package names are uniformly singular, but class names can be plural if they have plural meanings.

```
正例：应用工具类包名为com.alibaba.open.util、类名为MessageUtils（此规则参考spring的框架结构）
```
10. **[Mandatory]** Put an end to completely non-standard abbreviations and avoid looking at the text without knowing its meaning.

```
反例： AbstractClass“缩写”命名成AbsClass；condition“缩写”命名成 condi，此类随意缩写严重降低了代码的可阅读性。
```
11. **[Recommended]** If design patterns are used, it is recommended that the specific pattern be reflected in the class name.

> Description: The design pattern is embodied in the name, which is helpful for the reader to quickly understand the architecture design idea.

```
正例：public class OrderFactory;
public class LoginProxy;
public class ResourceObserver;
```
12. **[Recommended]** Keep the methods and properties in the interface class free of any decorative symbols (as well as public), keep the code concise, and add valid Javadoc comments. Try not to define variables in the interface. If you must define a variable, it must be related to the interface method and is the basic constant of the whole application.

```
正例：接口方法签名：void f();
接口基础常量表示：String COMPANY = "alibaba";
反例：接口方法定义：public abstract void f();
说明：JDK8中接口允许有默认实现，那么这个default方法，是对所有实现类都有价值的默认实现。
```
13. There are two sets of rules for naming interface and implementation classes:

* **[Mandatory]** For Service and DAO classes, based on the concept of SOA, the exposed service must be an interface, and the internal implementation class is distinguished from the interface by the suffix of Impl.
```
正例：CacheServiceImpl实现CacheService接口。
```
**[Recommended]** If it is an interface name that describes an ability, take the corresponding adjective as the interface name (usually in the form of – able).
```
正例：AbstractTranslator实现 Translatable。
```
14. **[Reference]** Enum suffixes are recommended for enumeration class names. Enum member names should be all uppercase, with words separated by underscores.

> Note: Enumerations are just special constant classes, and constructors are forced to be private by default.

```
正例：枚举名字：DealStatusEnum，成员名称：SUCCESS / UNKNOWN_REASON。
```
15. **[Reference]** Naming conventions for each layer:

* Service/DAO Layer Method Naming Convention

1. Methods that get a single object are prefixed with get.
2. Methods that get multiple objects are prefixed with list.
3. The method of obtaining the statistical value is prefixed with count.
4. The insert method is prefixed with save (recommended) or insert.
5. The delete method is prefixed with remove (recommended) or delete.
6. The modified method is prefixed with update.


* Domain Model Naming Convention

1. Data object: XXX DO, XXX is the name of the data table.
2. Data transfer object: XXX DTO, where XXX is the name related to the business field.
3. Display object: XXX VO, XXX is usually the name of the webpage.
4. POJO is a general term for DO/DTO/BO/VO. It is forbidden to name it as xxxPOJO.

## (II) Definition of constant

1. **[Mandatory]** No magic values (i.e., undefined constants) are allowed to appear directly in the code.

```
反例： String key="Id#taobao_"+tradeId；
cache.put(key,  value);
```

2.  **[Mandatory]** For the initial assignment of long or long, you must use an uppercase L, not a lowercase l. Lowercase is easily confused with the number 1, causing misunderstanding.

> Description: Long a = 2l; Is it a number of 21 or a Long type of 2?

3. **[Recommended]** Do not use a constant class to maintain all constants, but classify them according to their functions and maintain them separately. For example, the cache-related constants are placed under the class: CacheConsts; the system configuration-related constants are placed under the class: ConfigConsts.

> Note: For a large and complete constant class, you have to use the search function to locate the modified constant, which is not conducive to understanding and maintenance.

4. **[Recommended]** There are five reuse levels of constants: shared constants across applications, shared constants within applications, shared constants in sub-projects, shared constants in packages, and shared constants within classes.

- Cross-application shared constant: It is placed in the two-party library, usually under the constant directory in the client. Jar.
- Shared constants within the application: placed in the constant directory in the modules of one library.

```
反例：易懂变量也要统一定义成应用内共享常量，两位攻城师在两个类中分别定义了表示“是”的变量：
类A中：public  static final String YES = "yes";
类B中：public  static final String YES = "y";
A.YES.equals(B.YES)，预期是true，但实际返回为false，导致产生线上问题。
```



- Shared constant inside the sub-project: under the constant directory of the current sub-project.
- Shared constants within the package: that is, in a separate constant directory under the current package.
- Shared constants within a class: defined directly within the class as private static final.

5. **[Recommended]**Use the Enum class if the value of the variable changes only within a range. If you have an extended attribute other than a name, you must use the Enum class. The number in the positive example below is the extended information, indicating the day of the week.

```
正例：publicEnum{MONDAY(1),TUESDAY(2),WEDNESDAY(3),THURSDAY(4),FRIDAY(5),SATURDAY(6), SUNDAY(7);}
```

## (III) Format specification

1. **[Mandatory]** Conventions for the use of braces. If the curly brackets are empty, simply write { } without a new line; if the code block is not empty, then:

* Do not wrap before the opening brace.
* Wrap after open brace.
* Wrap line before closing brace.
* The closing brace is followed by an else and so on without a line break; this means that the closing brace must be followed by a line break.

2.  **[Mandatory]** No space appears between the left parenthesis and the next character; similarly, no space appears between the right parenthesis and the previous character. For details, please refer to the positive example at the bottom of Article 5.

3.  **[Mandatory]** Reserved words such as if/for/while/switch/do must have a space between them and the left and right parentheses.

4.  **[Mandatory]** A space must be added to the left and right of any operator.

> Note: Operators include assignment operator =, logical operator & &, addition, subtraction, multiplication and division symbol, trinary operator, etc.

5. **[Mandatory]** Indentation is 4 spaces and the tab character is not allowed.

> Note: If you use tab indent, you must set 1 tab to 4 spaces. When IDEA sets the tab to 4 spaces, do not check Use tab character; in eclipse, you must check insert spaces for tabs.

```
正例：（涉及1-5点）
public static void main(String args[]) {
	//缩进4个空格
	String say = "hello";
	//运算符的左右必须有一个空格
	int flag = 0;
	//关键词if与括号之间必须有一个空格，括号内的f与左括号，0与右括号不需要空格
	if (flag == 0) {
		System.out.println(say);
	}
	//左大括号前加空格且不换行；左大括号后换行
	if (flag == 1) {
		System.out.println("world");
		//右大括号前换行，右大括号后有else，不用换行
	} else {
		System.out.println("ok");
		//在右大括号后直接结束，则必须换行
	}
}
```
6. **[Mandatory]** The number of characters in a single line shall not exceed 120. If the number exceeds 120, a line feed is required. The following principles shall be followed during line feed:

* The second line is indented 4 spaces relative to the first line, starting from the third line, without further indentation. Refer to the example.
* Operator wraps with the following text.
* The dot notation for the method call wraps with the following text.
* Wrap lines after multiple parameters are too long and commas.
* Do not wrap before the parentheses. See counterexample.
```
正例：
StringBuffer sb = new StringBuffer();
//超过120个字符的情况下，换行缩进4个空格，并且方法前的点符号一起换行
sb.append("zi").append("xin")...
	.append("huang")...
	.append("huang")...
	.append("huang");
反例：
StringBuffer sb = new StringBuffer();
//超过120个字符的情况下，不要在括号前换行
sb.append("zi").append("xin")...append
	("huang");
//参数很多的方法调用可能超过120个字符，不要在逗号前换行
method(args1, args2, args3, ...
	, argsX);
```
7. **[Mandatory]** Multiple parameter commas must be followed by a space when method parameters are defined and passed in.

```
正例：下例中实参的"a",后边必须要有一个空格。
method("a", "b", "c");
```
8. **[Mandatory]** The IDE's text file encoding is set to UTF-8; Use the Unix format, not the windows format, for line breaks in files in the IDE. 

9. **[Recommended]** It is not necessary to add a number of spaces to align the characters on one line with the corresponding characters on the previous line.

```
正例：
int a = 3;
long b = 4L;
float c = 5F;
StringBuffer sb = new StringBuffer();
说明：增加sb这个变量，如果需要对齐，则给a、b、c都要增加几个空格，在变量比较多的
```
10. **[Recommended]** A blank line is inserted between groups of execution statements in a method body, between groups of variable definition statements, between different business logics, or between different semantics. There is no need to insert a blank line between the same business logic and semantics.

> Note: It is not necessary to insert multiple lines of spaces to separate them.

## (4) Control statement

1. **[Mandatory]** Within a switch block, each case is either terminated by a break/return, etc., or annotated to indicate up to which case the program will continue; within a switch block, a default statement must be included at the end, even if it has no code.

2.  **[Mandatory]** You must use braces  in if/else/for/while/do statements, even if there is only one line of code. Avoid the following form: if (condition) statements;

3. **[Recommended]** It is recommended to use else as little as possible, and the if-else method can be rewritten as:

```
if(condition){
	...
	return obj;
}
//接着写else的业务逻辑代码;
说明：如果非得使用if()...else if()...else...方式表达逻辑，【强制】请勿超过 3层，
超过请使用状态设计模式。
正例：逻辑上超过 3层的if-else代码可以使用卫语句，或者状态模式来实现。
```
4. **[Recommended]** Except for common methods (such as getXxx/isXxx), do not execute other complex statements in conditional judgment. Assign the result of complex logical judgment to a meaningful Boolean variable name to improve readability.

> Note: The logic in many if statements is quite complex. The reader needs to analyze the final result of the conditional expression to determine what kind of condition executes what kind of statement. So, what if the reader analyzes the logical expression incorrectly?

```
正例：
//伪代码如下
boolean existed = (file.open(fileName, "w") != null) && (...) || (...);
if (existed) {
...
}
反例：
if ((file.open(fileName, "w") != null) && (...) || (...)) {
...
}
```
5. **[Recommended]** The statements in the loop body should be considered for performance. The following operations should be moved outside the loop body as far as possible, such as defining objects, variables, obtaining database connections, and performing unnecessary try-catch operations (whether this try-catch can be moved outside the loop body).

6. **[Recommended]** Interface input parameter protection. In this scenario, the common interface is used for batch operations.

7. **[Reference]** Scenarios requiring parameter verification in the method:

* Methods that are called infrequently.
* For methods with high time overhead, the parameter verification time is almost negligible, but if the intermediate execution rollback or error is caused by parameter errors, the loss outweighs the gain.
* Methods that require extreme stability and availability.
* Open interface provided externally, whether it is RPC/API/HTTP interface.
* Sensitive permission entry.

8.  **[Reference]** Scenarios that do not require parameter validation in the method:

* Parameter validation is not recommended for methods that are likely to be called in a loop. However, the external parameter check must be noted in the method statement.
* The underlying method call frequency is relatively high, and it is generally not verified. After all, like the last step of pure water filtration, parameter errors are unlikely to be exposed at the bottom. Generally, the DAO layer and the Service layer are in the same application and deployed in the same server, so the parameter verification of DAO can be omitted.
* A method that is declared private will only be called by its own code. If you can be sure that the parameters passed by the code calling the method have been checked or that there will be no problem, you can not check the parameters at this time.

## (5) Notes and regulations

1. **[Mandatory]** The annotation of class, class attribute and class method must use Javadoc specification, use/** content */format, and must not use//XXX mode.

> Note: In the IDE editing window, Javadoc mode will prompt the relevant comments, and the generated Javadoc can correctly output the corresponding comments; In IDE, when the project calls the method, it can float the meaning of the method, parameter and return value without entering the method to improve the reading efficiency.

2. **[Mandatory]** All abstract methods (including methods in interfaces) must be annotated with Javadoc. In addition to return values, parameters, and exception descriptions, they must also indicate what the method does and what it does.

> Note: Please specify the implementation requirements for the subclass or the calling considerations.

3. **[Mandatory]** All classes must have creator information added.

4. **[Mandatory]**A single line comment inside a method. Start a new line above the commented statement. Use the//comment. Multi-line comments inside a method use the/* */comment, taking care to align with the code.

5. **[Mandatory]** All enumerated type fields must have comments that describe the purpose of each data item.

6. **[Recommended]** Instead of "half-baked" English annotations, it is better to use Chinese annotations to clarify the problem. Proper nouns and keywords can be kept in the original English.

```
反例：“TCP连接超时”解释成“传输控制协议连接超时”，理解反而费脑筋。
```
7.  **[Recommended]** At the same time of code modification, comments should also be modified accordingly, especially parameters, return values, exceptions, core logic and so on.

> Explanation: The code is out of sync with the annotation update, just like the road network is out of sync with the navigation software update. If the navigation software is seriously lagging behind, it will lose the meaning of navigation.

8. **[Reference]** Commented-out code should be as descriptive as possible, rather than simply commented out.

> Note: There are two possibilities for code to be commented out:

> 1) Resume the code logic of this section later.

> 2) Never use.

> If the former has no annotation information, it is difficult to know the annotation motivation. The latter is recommended to be deleted directly (the code repository stores historical codes).

9. **[Reference]** Requirements for comments:

* First, it can accurately reflect the design ideas and code logic;
* Second, it can describe the business meaning, so that other programmers can quickly understand the information behind the code. A large piece of code with no comments at all is like a book to the reader. Comments are for yourself, so that you can clearly understand the train of thought at that time, even after a long time. Comments are also for successors, so that they can quickly take over their work.

10. **[Reference]** Good naming and code structure are self-explanatory, and annotations strive to be concise, accurate and well-expressed. Avoid one extreme of comments: too many comments. Once the logic of the code is changed, it is quite a burden to change the comments.

```
反例：
// put elephant into fridge
put(elephant, fridge);
方法名put，加上两个有意义的变量名elephant和fridge，已经说明了这是在干什么，语义清晰的代码不需要额外的注释。
```
11. **[Reference]** For special comment mark, please indicate the mark person and mark time. Take care to deal with these marks in a timely manner, and clean up such marks frequently through mark scanning. Online faults sometimes originate from the codes at these markers.

* To Do (TODO): (tag by, tag time, [estimated processing time]) represents functionality that needs to be implemented, but is not currently implemented. This is actually a tag for Javadoc, which is not yet implemented, but is widely used. Can only be applied to classes, interfaces, and methods (because it is a Javadoc tag).
* Error, not working (FIXME): (Tag by, tag time, [estimated processing time]) Use FIXME in comments to mark a situation where a code is wrong, does not work, and needs to be corrected in a timely manner.

## (VI) Others

1. **[Mandatory]** In the use of regular expressions, the use of its pre-compilation function can effectively accelerate the speed of regular matching.

> Note: Do not define in method bodies: Pattern pattern = Pattern. Compile (rule);

2. **[Mandatory]** When calling the attribute of POJO class, it is recommended to directly use the attribute name to obtain the value, and the template engine will automatically call the getXxx () of POJO according to the specification. The isXxx () method is automatically called.

> Note: If it is a Boolean wrapper object, the getXxx () method is called first.

3. **[Mandatory]** Variables delivered to the page in the background must be marked with $! { var }, an exclamation point in the middle.

> Note: If var = null or does not exist, ${ var } will be displayed directly on the page.

4. **[Mandatory]** Note that the method of Math. Random () returns the type of double. Note that the range of values is 0 ≤ X < 1 (the value can be taken to zero, and note the exception of division by zero). If you want to obtain a random number of integer type, do not multiply X by 10 and then round it. Use the nextInt or next Long method of the Random object directly.

5. **[Mandatory]** Acquire that System. CurrentTimeMillis of the current millisecond (); Instead of new Date ().getTime ();

> Note: If you want to get a more accurate nanosecond time value, use the System. NanoTime (). In JDK8, the Instant class is recommended for scenarios such as counting time.

6. **[Recommended]** Try not to add variable declarations, logical operators, or any complex logic to the VM template.

7. **[Recommended]** Any construction or initialization of a data structure should specify a size to prevent the data structure from growing indefinitely and eating up memory.

8. **[Recommended]** For "explicitly discontinued code and configuration", such as methods, variables, classes, configuration files, dynamic configuration properties, etc., we must resolutely clean them out of the program to avoid causing too much garbage.



> Reference: Alibaba JAVA Development Manual
