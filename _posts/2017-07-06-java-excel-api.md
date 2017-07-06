---
layout: post
title: JAVA Excel API 详解
---
# 简介
## 背景
后端开发中静态文件的导入导出十分常见, 虽然越来越多的服务可以被转移到前端, 后端处理文件仍有代码结构清晰, 组织数据容易的优势.
目前流行的Office操作有两套, 分别是
- [Apache POI](http://poi.apache.org/)
- [Java Excel API]( http://jexcelapi.sourceforge.net/)

**目前POI是更为高效和方便的选择.**

## POI封装框架
由于POI是通过代码直接操纵Office文件, 会带来
- 代码结构不清晰, 大量冗余代码, 增加系统复杂度.
- 每次添加新的导入导出操作都可能使用不同的逻辑, 导致维护工作困难

因此产生了第三方再次封装的框架, 如
- [JXLS]( http://jxls.sourceforge.net/samples/simple_exporter.html )
将复杂度置入Office文件写成的模板中, 最大化减少系统的复杂度, 可以实现很多效果, 但有一定学习成本.

- [EasyPoi](http://git.oschina.net/jueyue/easypoi)
国人开发, 功能如同名字easy,主打的功能就是容易,让一个没见接触过poi的人员 就可以方便的写出Excel导入导出,Excel模板导出,Word模板导出,通过简单的注解使用5行代码即可完成Excel导出, 同样支持模板 语言, 但由于是个人维护, 功能并不丰富, 版本也不是很稳定

- [简易框架]( http://www.zslin.com/web/article/detail/30)
将源码嵌入程序的简易框架, 代码量很少, 可以用来观察如何将POI封装为第三方框架

# 框架使用
## [Apache POI](http://poi.apache.org/)
[Apache POI](http://poi.apache.org/)是Apache基金组织Jakarta项目的子项目，它包括一系列的API，可以操作多种格式的Microsoft Office文件，通过这些API使Java更方便的操作Excel、Word等格式的Office文件

## [JXLS]( http://jxls.sourceforge.net/samples/simple_exporter.html)
### Getting Started
	1. Adding Maven dependency
	 - core Jxls module

  ```Maven
    <dependency>
      <groupId>org.jxls</groupId>
      <artifactId>jxls</artifactId>
      <version>2.4.0</version>
    </dependency>
  ```

	- To use Apache POI API based transformer implementation add the following dependency

  ```Maven
    <dependency>
      <groupId>org.jxls</groupId>
      <artifactId>jxls-poi</artifactId>
      <version>1.0.12</version>
    </dependency>
  ```

	- To use Java Excel API based transformer implementation add the following dependency

  ```Maven
    <dependency>
      <groupId>org.jxls</groupId>
      <artifactId>jxls-jexcel</artifactId>
      <version>1.0.6</version>
    </dependency>
  ```
	2. Editing pure POJO Entity
```Java
  public class Employee {
    private String name;
    private Date birthDate;
    private BigDecimal payment;
    private BigDecimal bonus;
    // ... constructors
    // ... getters/setters
  }
```
	3. Create an Excel template using a special markup


	4. Use Jxls API to process the prepared template and fill it with the employee data
```Java
  //...
    List<Employee> employees = generateSampleEmployeeData();
    try(InputStream is = ObjectCollectionDemo.class.getResourceAsStream("object_collection_template.xls")) {
        try (OutputStream os = new FileOutputStream("target/object_collection_output.xls")) {
            Context context = new Context();
            context.putVar("employees", employees);
            JxlsHelper.getInstance().processTemplate(is, os, context);
        }
    }
    //...

	5.
```

### 主要概念
Jxls 有如下3个主要概念
- XlsArea
- Command
- Transformer

下面将依次讨论
1. XlsArea

XlsArea 代表Excel文件中的一个矩形区域.它很可能由一个 cell range 定义 或通过具体说明 一个区域开始的cell 和范围(行列数) . XlsArea 包含具体指明范围内的所有Excel cells.
每个XlsArea 可能有一系列的 Commands 与之关联, 这些 Commands 将在区域处理过程中被Jxls引擎执行. XlsArea 也可以有嵌套在其中的自区域. 每个子区域也是一个 XlsArea , 包含它自己的 Commands和子区域.

XlsArea 可以被下列方式定义
- 通过在Excel模板中使用一系列特定的句法. Jxls提供一套默认的标签和其 XlsCommentAreaBuilder. 如果需要的话也可以定制相应的标签.
- 通过使用XML configuration. Jxls 提供XmlAreaBuilder 类作为默认的XML标签的实现.
- 通过使用 Jxls Java API
你能在 here 找到更多细节

	2. Command
Command 代表在单个或多重 XlsAreas区域中的一个转换动作.
相应的Java接口类似于如下
public interface Command {
    String getName();
    List<Area> getAreaList();
    Command addArea(Area area);
    Size applyAt(CellRef cellRef, Context context);
    void reset();
}
所有Command 中主要的方式是 Size applyAt(CellRef cellRef, Context context) . 方法通过context 变量传递的数据在cell cellRef 上执行Command 动作. Context 效果类似于map 并且被用来向command传递数据. 该方法通过 Sizeobject返回转换过的区域的新的尺寸.
目前Jxls 提供下列内建 commands
• Each-Command - 用来处理遍历一个对象集合的command
• If-Command - 用来处理依赖于特定情况的command
• Image-Command - command to render an image
当然你可以很容易的定义 自订commands, 具体介绍在Custom-Command中
传递到 Command 中的数据将被执行, 这些数据应当被组织为Context 对象, 这个对象与map非常相似, 由 keys在XLS 模板中声明的keys 和data设定的values组成.
	3. Transformer
接口Transformer 允许XlsArea 不依赖任何特定的实现与 Excel交互.它意味着通过提供不同的Transformer接口的实现, 我们可以使用不同的 Java-to-Excel 类库.
接口实现如下
public interface Transformer {
    void transform(CellRef srcCellRef, CellRef targetCellRef, Context context, boolean updateRowHeight);
void setFormula(CellRef cellRef, String formulaString);
Set<CellData> getFormulaCells();
CellData getCellData(CellRef cellRef);
List<CellRef> getTargetCellRef(CellRef cellRef);
void resetTargetCellRefs();
void resetArea(AreaRef areaRef);
void clearCell(CellRef cellRef);
List<CellData> getCommentedCells();
void addImage(AreaRef areaRef, byte[] imageBytes, ImageType imageType);
void write() throws IOException;
TransformationConfig getTransformationConfig();
void setTransformationConfig(TransformationConfig transformationConfig);
boolean deleteSheet(String sheetName);
void setHidden(String sheetName, boolean hidden);
void updateRowHeight(String srcSheetName, int srcRowNum, String targetSheetName, int targetRowNum);
}
### XLS Area
	1. Introduction
XLS Area 是JxlsPlus中的主要概念. 基本上它代表了一个Excel文件中需要被转换的矩形区域. 每个XLS Area可能有一组关联的转换 Commands和一些列嵌套的子区域. 每个子区域也是一个拥有一系列Commands和子区域的 XLS Area.一个 top-level(顶级) XLS Area是一个没有父区域的区域 (即没有嵌套在任何XLS Area中).
	2. XLS Area 结构
有三种构建XLS Area的方式
• Excel markup(Excel标签)
• XML configuration(XML配置)
• Java API(Java接口)
下面解释每种方法的细节
使用Excel markup构建XLS Area
你可以在Excel 模板中使用特殊的标签去组织XLS area. 标签应该放在Excel的第一个cell(格)的comment(评注)中, 看起来像这样
jx:area(lastCell = "$AREA_LAST_CELL")
$AREA_LAST_CELL 是定义的最后一个区域.
这个标签定义了一个top-level area开始于包含标签的comment所在的cell, 结束与 <AREA_LAST_CELL> 定义的位置.
一个简单例子来展示这个 Output Object Collection sample

一个区域被定义在A1 单元格的comment(批注)中, 通过
jx:area(lastCell="D4")
这样我们就有了一个覆盖 A1:D4 范围的单元格.
为了转换标记并创建 XlsArea 对象, 我们应该使用下面展示的 XlsCommentAreaBuilder 类
// getting input stream for our report template file from classpath
InputStream is = ObjectCollectionDemo.class.getResourceAsStream("object_collection_template.xls");
// creating POI Workbook
Workbook workbook = WorkbookFactory.create(is);
// creating JxlsPlus transformer for the workbook
PoiTransformer transformer = PoiTransformer.createTransformer(workbook);
// creating XlsCommentAreaBuilder instance
AreaBuilder areaBuilder = new XlsCommentAreaBuilder(transformer);
// using area builder to construct a list of processing areas
List<Area> xlsAreaList = areaBuilder.build();
// getting the main area from the list
Area xlsArea = xlsAreaList.get(0);
下面两行代码做了构建区域的所有主要工作
AreaBuilder areaBuilder = new XlsCommentAreaBuilder(transformer);
List<Area> xlsAreaList = areaBuilder.build();
首先你要通过实例化XlsCommentAreaBuilder去构建 AreaBuilder. 第二步是调用 areaBuilder.build() 方法通过模板中的标记构建一列Area 对象.
当你拿到这列顶级区域后你就可以使用它们去处理 Excel 转换.
使用XML 配置去构建XLS Area
如果你更喜欢通过XML标签的方式去构建 XLS Area, 下列方法可能更适合你.
首先你必须创建一个 XML 配置文件定义你的区域.
作为例子让我们看一个简单 XML 配置 从 Object Collection output with XML Builder
<xls>
    <area ref="Template!A1:D4">
        <each items="employees" var="employee" ref="Template!A4:D4">
            <area ref="Template!A4:D4"/>
        </each>
    </area>
</xls>
根元素是xls. 之后你可以定义一系列 area 元素去定义每个顶级区域.
这里是一个单顶级区域的例子,将生成在Template sheet的 A1:D4区域中 .
<area ref="Template!A1:D4">
在 area元素内 我们通过特定的元素定义相关的 commands.在这个例子中我们通过each xml 元素定义 each command . 与这个 each command 相连的区域被ref 属性定义.
<each items="employees" var="employee" ref="Template!A4:D4">
在 each command 内部还有一个嵌套的区域参数
<area ref="Template!A4:D4"/>
使用Java API去构建 XLS Area
使用Java API去构建 XLS Area你将会使用XlsArea 类的某个构造方法.可用的有
public XlsArea(AreaRef areaRef, Transformer transformer);
public XlsArea(String areaRef, Transformer transformer);
public XlsArea(CellRef startCell, CellRef endCell, Transformer transformer);
public XlsArea(CellRef startCellRef, Size size, List<CommandData> commandDataList, Transformer transformer);
public XlsArea(CellRef startCellRef, Size size);
public XlsArea(CellRef startCellRef, Size size, Transformer transformer);
构建顶级区域你需要提供一个 Transformer 实例so that the area can use it for transformation.这样这个区域就能使用它完成转换.
其次你必须定义区域单元格通过一个字符串类型的单元格范围 或通过创建 CellRef (单元格相关的对象)并且设置区域的 Size.
这里有个代码片段有关于构造一系列嵌套的XLS模板区域及其commands
// create Transformer instance
// ...
// Create a top level area
XlsArea xlsArea = new XlsArea("Template!A1:G15", transformer);
// Create 'department' area
XlsArea departmentArea = new XlsArea("Template!A2:G13", transformer);
// create 'EachCommand' to iterate through departments
EachCommand departmentEachCommand = new EachCommand("department", "departments", departmentArea);
// create an area for employee 'each' command
XlsArea employeeArea = new XlsArea("Template!A9:F9", transformer);
// create an area for 'if' command
XlsArea ifArea = new XlsArea("Template!A18:F18", transformer);
// create 'if' command with the specified areas
IfCommand ifCommand = new IfCommand("employee.payment <= 2000", ifArea,
        new XlsArea("Template!A9:F9", transformer));
// adding 'if' command instance to employee area
employeeArea.addCommand(new AreaRef("Template!A9:F9"), ifCommand);
// create employee 'each' command and add it to department area
Command employeeEachCommand = new EachCommand( "employee", "department.staff", employeeArea);
departmentArea.addCommand(new AreaRef("Template!A9:F9"), employeeEachCommand);
// add department 'each' command to top-level area
xlsArea.addCommand(new AreaRef("Template!A2:F12"), departmentEachCommand);
### Excel mark-up
Jxls的Excel标签可以分为3个部分
• Bean 属性标签
• Area 定义标签
• Command 定义标签
Jxls 提供XlsCommentAreaBuilder 类来读取Excel单元格上评注(comments)内的标签. XlsCommentAreaBuilder 实现自AreaBuilder 接口.
public interface AreaBuilder {
    List<Area> build();
}
这是一个只有一个方法的简单接口, 用来返回一组 Area(区域) 对象.
所以如果想自订标签, 你应该创建你自己的AreaBuilder 实现 并解析输入的Excel模板(或其它形式)为你想要的结果
	1. Bean 属性标签
Jxls 使用Apache JEXL expression language to process表达是语言去处理
未来发布的表达式语言引擎或许可以被定制, 这样你将能替换JEXL为你需要的任何表达式语言.
JEXL 表达式语言的句法可以参考这里 JEXL Syntax.
Jxls 要求 JEXL表达式放置在  XLS 模板文件的 ${ }中.
举个例子就如下列单元格内容 ${department.chief.age} years 告诉Jxls 去使用JEXL表达式语言解析 department.chief.age using JEXL (假设department 对象已经被设定在 Context中. 如果表达式 department.getChief().getAge() 的结果是 35, Jxls 将在XlsArea 处理过程中把 35 years放在相应单元格.
	2. XLS Area markup
Jxls 区域标记用来定义 要由Jxls引擎处理的根XlsArea(s) . XlsCommentAreaBuilder 支持在Excel单元格评注内使用下列句法去定义区域
jx:area(lastCell="<LAST_CELL>")
这里<LAST_CELL> 定义了矩形区域最右下角的单元格. 而其实单元格被定义为 Excel 评注所在的位置.
所以假设我们在A1 单元格中有下列comment jx:area(lastCell="G12") ,根区域就是 A1:G12.
XlsCommentAreaBuilder 被用来从模板文件中读取所有区域. 如下面代码 片段将读取所有区域到xlsAreaList中并存储第一个区域到 xlsArea 变量中
    AreaBuilder areaBuilder = new XlsCommentAreaBuilder(transformer);
    List<Area> xlsAreaList = areaBuilder.build();
    Area xlsArea = xlsAreaList.get(0);
在大多数例子中定义一个根 XlsArea 就足够了.
	3. Command markup
Commands 应该被定义在一个XlsArea中. XlsCommentAreaBuilder 接受下面的 标记创建的Excel 单元格评注
jx:<command_name>(attr1='val1' attr2='val2' ... attrN='valN' lastCell=<last_cell> areas=["<command_area1>", "<command_area2", ... "<command_areaN>"])
<command_name> 是一个内置或手工注册在XlsCommentAreaBuilder中的command 的名字. 目前有如下内置command
• each
• if
• image
自订的 commands可以通过 XlsCommentAreaBuilder类的static void addCommandMapping(String commandName, Class clazz) 方法手工注册.
attr1, attr2,…, attrN 是command 具体的属性
如 If-Command 有condition 属性去设置条件表达式.
<last_cell>  定义了command 控制区域的右下角的单元格. 而左上角的位置则被command 标记标注的位置所说明.
<command_area1>, <command_area2>, … <command_areaN> - XLS 区域被当做参数传递给command.
如 If-Command 要求下列区域被定义
• ifArea 是一个涉及 If-command 条件为true时输出的区域
• elseArea 则是党 If-command 条件结果为false 时输出(可选)
所以当定义 If-command 时它的区域参数可能看起来像这样areas=["A8:F8","A13:F13"]
在一个单元格评注内你可以定义多个 Commands. 如 Each 和If command definitions may look like this共同定义可能如下例
jx:each(items="department.staff", var="employee", lastCell="F8")
jx:if(condition="employee.payment <= 2000", lastCell="F8", areas=["A8:F8","A13:F13"])

### Each-Command(遍历指令)
	1. 介绍
Each-Command 用来遍历集合并复制到command XLS 区域. 和Java 的操作很相同.
	2. Command 属性
Each-Command有下列属性
• var 是Jxls 上下文中用来存放遍历集合时每一个新对象的变量的名字
• items 是存放用来遍历的集合的上下文的变量的名字
• area 是用来标识一个 XLS Area 来作为 each command 的范围
• direction 是 Direction 枚举的值, 包含 DOWN 或RIGHT 来指明朝什么方向重复command 躯干 - 即通过行还是通过列来排列集合. 默认值是DOWN.
• select 是一个表示选择器用来在遍历时过滤集合的项
• groupBy 通过遍历对象的一个属性分组
• groupOrder 标明分组的排序规则 (‘desc’ or ‘asc’)
• cellRefGenerator 是自订的目标单元格生成策略
• multisheet是一个上下文变量,包含用来输出集合的一组工作表名称
• lastCell 是所有command 的常规属性, 指出了 command 区域的最后一个单元格
The var and items attributes are mandatory while others can be skipped.
有关使用 cellRefGenerator 和multisheet 属性的更多信息, 请查看Multiple sheets section.
	3. 构建Command
作为一个Jxls command 你可以使用 Java API 或Excel 标签或XML 配置 任意一种方式去定义 Each-command
3.1 使用Java API
下面是一个创建 Each-Command 的例子, 见 Jxls examples at BitBucket
// creating a transformer and departments collection
    ...
// creating department XlsArea
    XlsArea departmentArea = new XlsArea("Template!A2:G13", transformer);
// creating Each Command to iterate departments collection and attach to it "departmentArea"
    EachCommand departmentEachCommand = new EachCommand("department", "departments", departmentArea);
3.2 使用Excel 标签
使用Excel 标签创建 Each Command 你应该在command 范围的起始单元格的评注中使用专属的句法jx:each(items="employees" var="employee" lastCell="D4")
所以我们使用jx:each 以及一对圆括号中被空格分割的数个command 属性. lastCell 属性则定义了 command XlsArea 的范围.
3.3 使用XML标签
使用XML配置来创建 Each Command 将使用下列标签
<each items="employees" var="employee" ref="Template!A4:D4">
    <area ref="Template!A4:D4"/>
</each>
这里ref 属性定义了Each-Command的区域范围. 而内部区域定义了Each-Command的躯干. 通常他们是相同的.
3.4 重复方向
默认的 Each-Command direction(方向) 属性是 DOWN, 也就是说数据会向下对Excel的每行赋值.
如果你想从左向右按列赋值 direction 属性应该为 RIGHT .
Java API you do this like如下
//... creating EachCommand to iterate departments
// setting its direction to RIGHT
departmentEachCommand.setDirection(EachCommand.Direction.RIGHT);
3.5 分组数据
Each-Command 支持通过 groupBy 属性进行分组. groupOrder 属性则设置了排列顺序( desc 或 asc)
在excel 标签中类似如下
jx:each(items="employees" var="myGroup" groupBy="name" groupOrder="asc" lastCell="D6")
在这个例子中每个分组可以通过 myGroup 变量调用, 其能在context中简单取得.
当前分组的对象可以通过 myGroup.item调用. 所以想要调用 employee 的名字可以使用
${myGroup.item.name}

所有分组中的对象都可以通过 分组的items 属性访问, 如jx:each(items="myGroup.items" var="employee" lastCell="D6")
你也可以略过 var 属性, 这样默认的分组变量名应为be _group.
具体实例在 Grouping Example

### If-Command
#### 简介
If-Command 是一种有条件的指令, 用来根据特定条件( 标注在command中的condition 属性)输出一个特定区域.
#### Command 属性
If-Command has the following attributes有下列属性
• condition is a conditional expression to test是用来测试的条件表达式
• ifArea 是一个特定区域的编号, 当condition结果为ture时数据将被输入到此区域
• elseArea 与 ifArea 相反, 当condition结果为false时数据将被输入到此区域
• lastCell command 的通用属性, 指出了command区域的最后一个单元格ifArea 和condition 属性是必须的.
#### Command 构建
就像此前的任何 Jxls command你可以使用 Java API 或Excel 标记or XML 配置去定义If-Command
	1. 使用Java API
下面是一个 If-Command 的例子, 你可以在 Jxls examples at BitBucket 中找到它.
// ...
// creating 'if' and 'else' areas
XlsArea ifArea = new XlsArea("Template!A18:F18", transformer);
XlsArea elseArea = new XlsArea("Template!A9:F9", transformer);
// creating 'if' command
IfCommand ifCommand = new IfCommand("employee.payment <= 2000", ifArea, elseArea);
	2. Excel 标签
使用Excel标签创建 If Command 你需要用下列句法在command区域的起始单元格的评注中标识.
jx:if(condition="employee.payment <= 2000", lastCell="F9", areas=["A9:F9","A18:F18"])
这里lastCell 属性定义了 If-Command 区域的最后一个单元格.
	3. XML 标签
使用XML 配置创建 If Command 你需要用下列标签
<area ref="Template!A9:F9">
    <if condition="employee.payment &lt;= 2000" ref="Template!A9:F9">
        <area ref="Template!A18:F18"/>
        <area ref="Template!A9:F9"/>
    </if>
</area>
这里ref 属性定义了 If-Command 控制的区域.


## EasyPOI
控制器UserController.download方法
// 下载execl文档
@RequestMapping("/download")
public void download(HttpServletRequest request, HttpServletResponse response) throws Exception {
// 告诉浏览器用什么软件可以打开此文件
response.setHeader("content-Type", "application/vnd.ms-excel");
// 下载文件的默认名称
response.setHeader("Content-Disposition", "attachment;filename=user.xls");
List<User> list = userRepository.findAll();
Workbook workbook = ExcelExportUtil.exportExcel(new ExportParams(), User.class, list);
workbook.write(response.getOutputStream());
}
