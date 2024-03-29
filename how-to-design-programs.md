# 目录

[TOC]

## 3 怎样设计程序

学习编程需要掌握许多概念s。另一方面，编程需要一门语言。尽管编程语言和自然语言有一些相通的地方，比如词汇，语法和成语。编程语言是人造的东西（artificial constructions）。
另一方面，学习如何把一个问题的说明转化为程序是很关键的。我们要学会取舍，找出程序的输入、输出，如何关联。我们必须知道或找出所选语言及其库是否为程序要处理的数据提供某些基本操作。

所有这些听起来都相当复杂，您可能想知道为什么我们不只是迷路，在这里和那里进行实验，当结果看起来不错时，就独自留下足够的空间。 这种编程方法通常被称为“车库编程”，并且在许多场合都成功。 有时它是创业公司的启动平台。 但是，初创公司无法出售“车库工作”的结果，因为只有原始的程序员及其朋友才能使用它们。 一个好的程序附带简短的说明，解释它的功能，期望的输入以及产生的结果。 理想情况下，还可以保证它确实有效。 在最佳情况下，程序与问题陈述的联系显而易见，因此对问题陈述的微小更改很容易转化为对程序的微小更改。 软件工程师将此称为“编程产品”。

所有这些额外的工作都是必要的，因为程序员不会自己创建程序。程序员编写程序供其他程序员阅读，有时，人们会运行这些程序来完成工作。大多数程序都是大型，复杂的协作功能集合，没有人一天可以编写所有这些功能。程序员加入项目，编写代码，离开项目；其他人接管他们的程序并继续努力。另一个困难是，程序员的客户倾向于对他们真正想要解决的问题改变主意。他们通常都说对了，但更多的是，他们弄错了一些细节。更糟糕的是，诸如程序之类的复杂逻辑结构几乎总是遭受人为错误的困扰。简而言之，程序员会犯错误。最终有人发现了这些错误，程序员必须修复它们。他们需要从一个月前，一年前或二十年前重新读取程序并进行更改。

在这里，我们提出了一个设计方案，该方案将分步过程与围绕问题数据组织程序的方式相集成。 对于长时间不喜欢盯着黑屏的读者来说，本设计诀窍提供了一种系统地取得进步的方法。 对于那些教别人设计程序的人来说，食谱是诊断新手困难的一种工具。 对于其他人，我们的食谱可能可以应用于其他领域，例如医学，新闻或工程。 对于那些希望成为真正的程序员的人来说，设计秘诀还提供了一种理解和使用现有程序的方法，尽管并非所有程序员都使用这种设计秘诀来编写程序。 本章的其余部分专门介绍进入设计配方世界的第一步。 以下各章和各部分以一种或另一种方式完善和扩展了配方。

### 3.1 函数设计

#### **信息与数据**

程序的目的是描述消耗一些信息并产生新信息的计算过程。从这个意义上讲，程序就像数学老师给小学学生的指令一样。但是，与学生不同的是，该程序不仅可以处理数字，还可以使用导航信息进行计算，查找人员的地址，打开开关或检查视频游戏的状态。所有这些信息都来自真实世界的一部分（通常称为程序域），而程序的计算结果表示该域中的更多信息。

信息在我们的描述中起着核心作用。将信息视为有关程序领域的事实。对于处理家具目录的程序，信息为“五脚桌子”或“两米两米的方桌”。一个游戏程序处理的是另一种领域，其中“五个”可能是指某个对象从画布的一部分到另一部分在每个时钟滴答中移动的像素数。或者，薪资计划可能会处理“五个抵扣”。

要使程序处理信息，它必须以编程语言将其转换为某种形式的数据。然后处理数据；完成后，它将生成的数据再次转换为信息。交互式程序甚至可以混合这些步骤，根据需要从世界获取更多信息，并在两者之间传递信息。

我们使用BSL和DrRacket，因此您不必担心将信息转换为数据的麻烦。在DrRacket的BSL中，您可以将函数直接应用于数据并观察其产生的结果。结果，我们避免了编写将信息转换为数据，反之亦然的函数的严重问题。对于简单的信息来说，设计这样的程序很简单。对于除简单信息以外的任何内容，例如，您需要了解解析，而这立即需要程序设计方面的大量专业知识。

软件工程师使用标语模型视图控制器（MVC）作为BSL和DrRacket将数据处理从解析信息转换为数据以及将数据转换为信息的方式。的确，尽管大多数入门书籍仍将它们分开，但精心设计的软件系统可以实现这种分离，这已成为公认的智慧。因此，使用BSL和DrRacket可以使您专注于程序核心的设计，并且，如果您有足够的经验，则可以学习设计信息/数据转换部分。

在这里，我们使用两个预装的示教包来演示数据和信息的分离：2htdp / batch-io和2htdp / universe。 从本章开始，我们为批处理程序和交互式程序开发设计配方，以使您了解如何设计完整的程序。 请记住，成熟的编程语言库为完整的程序提供了更多的上下文，并且您将需要适当地调整设计方法。

到目前为止，您已经遇到了四类数据的名称：Number，String，Image和Boolean。 这样，制定新的数据定义仅意味着为现有数据形式引入新名称，例如数字的“温度”。 即使是这种有限的知识也足以解释我们的设计过程的概要。

**设计过程**一旦您了解了如何将输入信息表示为数据并将输出数据解释为信息，则将根据一个简单的过程来进行单个功能的设计：

1. 表达你如何表示信息为数据。

``` racket
; We use numbers to represent centimeters.
```

为您认为对程序成功至关重要的数据类别制定数据定义，例如温度定义。

2. 写下签名，目的声明和函数标头。

函数签名是一种注释，它告诉您的设计读者该函数消耗多少输入，从中提取哪些类以及产生什么样的数据。 这是分别用于功能的三个示例：

``` racket
; String -> Number
```

 消耗一个sring 一个数 一个图形 产生一个图形

``` racket
; String Number Image -> Image
```

停止！ 此函数产生什么？
目的陈述是BSL注释，它在一行中总结了函数的目的。 如果您对目的陈述有疑问，请写下问题的最短答案
该函数计算什么？

程序的每个读者都应该了解函数计算的内容，而不必阅读函数本身。
多功能程序还应附带目的说明。 的确，优秀的程序员编写了两个目的声明：一个供可能需要修改代码的读者使用，另一个供希望使用该程序但不阅读该程序的人士使用。

最后，标头是一种简单的函数定义，也称为存根。 为签名中的每一类输入选择一个变量名； 函数的主体可以是输出类中的任何数据。 这三个函数头与上述三个签名匹配：

``` racket
(define (f a-string) 0)

(define (g n) "a")

(define (h num str img) (empty-scene 100 100))
```

我们的参数名称反映了该参数代表的数据类型。 有时，您可能希望使用暗示参数目的的名称。
在制定目的陈述时，通常使用参数名称来澄清要计算的内容。 例如，

``` racket
; Number String Image -> Image 
; adds s to img,
; y pixels from the top and 10 from the left 
(define (add-image y s img)
  (empty-scene 100 100))
```

 3. 写几个函数的例子.

``` racket
; Number -> Number
; computes the area of a square with side len 
; given: 2, expect: 4
; given: 7, expect: 49
(define (area-of-square len) 0)
```

4. 下一步是进行盘点，以了解给定的值和需要计算的值。对于我们现在正在考虑的简单功能，我们知道它们是通过参数提供数据的。 尽管参数是我们尚不知道的值的占位符，但我们确实知道，函数必须根据未知数据来计算其结果。 为了提醒我们这个事实，我们将模板替换为函数的主体。

5. 现在该进行编码了。 通常，编码是指编程（尽管通常以最狭窄的方式进行编程），即编写可执行表达式和函数定义。

6. 适当设计的最后一步是在您之前制定的示例上测试功能。 目前，测试工作是这样的。
单击运行按钮，然后在交互区域中输入与示例匹配的功能应用程序：

如果确实遇到预期结果与实际值不匹配的情况，我们建议您首先向自己保证，预期结果是正确的。 如果是这样，则假定错误出在函数定义中。 否则，请修复示例，然后再次运行测试。 如果仍然遇到问题，则可能遇到了第三种情况，这种情况有些罕见。

### 3.2 指尖练习：函数

### 3.3 专业领域知识

很自然地想知道要编写函数的主体需要哪些知识。一点点反思告诉您，此步骤需要适当地掌握程序的域。实际上，这种领域知识有两种形式：
来自外部领域的知识，例如数学，音乐，生物学，土木工程，艺术等。因为程序员不能了解计算的所有应用程序领域，所以他们必须准备好理解各种应用程序领域的语言，以便他们可以与领域专家讨论问题。数学是许多（但不是全部）领域的交集。因此，程序员在解决领域专家遇到的问题时必须经常选择新的语言。

有关所选编程语言中库功能的知识。当您要翻译涉及切线函数的数学公式时，您需要知道或猜测您所选择的语言是否带有BSL tan等函数。当您的任务涉及图形时，您将从了解2htdp /图像库的可能性中受益。

由于您永远无法预测您将要使用的领域或必须使用哪种编程语言，因此必须对各种周围和适用的计算机语言的全部可能性有深刻的了解。否则，一些具有半熟的编程知识的领域专家将接管您的工作。
您可以从得出的数据定义中识别出需要领域知识的问题。只要数据定义使用所选编程语言中存在的类，功能主体（和程序）的定义就主要依赖于该领域的专业知识。后来，当我们引入复杂的数据形式时，功能设计需要计算机科学知识。

### 3.4 从函数到程序

并非所有程序都包含单个功能定义。有些需要几个功能；许多人也使用常量定义。无论如何，系统地设计每个功能始终很重要，尽管全局常数和辅助功能会稍微改变设计过程。

定义全局常量后，您的函数可以使用它们来计算结果。为了提醒自己它们的存在，您可能希望将这些常量添加到模板中。毕竟，它们属于可能有助于功能定义的事物清单。

之所以会出现多功能程序，是因为交互式程序自动需要处理按键和鼠标事件的功能，将状态呈现为音乐的功能，甚至可能还要更多。甚至批处理程序也可能需要几个不同的功能，因为它们执行几个单独的任务。有时问题陈述本身就建议了这些任务；有时，您在设计某些功能时会发现需要辅助功能。
由于这些原因，我们建议保留所需功能列表或愿望清单。 愿望清单上的每个条目应由三部分组成：函数的有意义的名称，签名和目的说明。 对于批处理程序的设计，请将主要功能放在愿望清单上并开始进行设计。 对于交互式程序的设计，可以将事件处理程序，stop-when函数和场景渲染函数放在列表中。 只要列表不为空，请选择一个愿望并设计功能。 如果在设计过程中发现需要其他功能，请将其放在列表中。 当列表为空时，您就完成了。

### 3.5 关于测试

## 7小结

在本书的第一部分中，您学习了很多简单但重要的课程。总结如下：

1. **一个好的程序员**设计程序。一个糟糕的程序员会不断修改，直到程序看起来可以运行为止。

2. **设计配方**有两个维度。一个涉及设计过程，即要采取的步骤顺序。另一个解释了所选数据表示如何影响设计过程。

3. 每个设计良好的程序都包含许多常量定义，结构类型定义，数据定义和函数定义。对于**批处理程序**，一个函数是“主要”函数，它通常包含其他几个函数以执行其计算。对于**交互式程序**，大爆炸功能扮演主要功能；它指定程序的初始状态，产生图像的输出函数以及最多三个事件处理程序：一个用于时钟滴答，一个用于鼠标单击，一个用于按键事件。在这两种程序中，功能定义都以“自顶向下”的形式显示，从主功能开始，然后是主功能中提到的功能，依此类推。

4. 像所有编程语言一样，“初学者语言”附带**词汇和语法**。程序员必须能够确定一种语言中每个句子的含义，以便他们能够预测给定输入后程序如何执行其计算。下面的Interezezzo详细解释了这个想法。

5. 包括BSL在内的编程语言都提供了丰富的库，因此程序员不必总是重新发明轮子。程序员应熟悉库提供的功能，尤其是其签名和用途说明。这样做可以简化生活。

6. 程序员必须了解所选编程语言提供的“工具”。这些工具或者是语言的一部分（例如cond或max），或者它们是从库中“导入”的。本着这种精神，请确保您理解以下术语：结构类型定义，函数定义，常量定义，结构实例，数据定义，大爆炸和事件处理函数。


