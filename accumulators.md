# Accumulators

当您要求ISL +将某些函数f应用于参数a时，通常会得到一些值v。如果再次求值（f a），则会再次得到v。事实上，无论您请求（f a）的评估频率如何，都将得到v。函数应用程序也可能永远循环或发出错误信号，但我们忽略了这些可能性。我们也忽略了随机性，这是该规则的真正例外。该功能是首次应用还是第100次应用，无论应用程序位于DrRacket的交互区域还是功能本身内部，都没有关系。该功能根据其用途说明运行，这就是您所需要知道的。

上下文无关的原理在递归函数的设计中起着至关重要的作用。在设计时，您可以自由地假设该函数计算了用途声明所承诺的内容，即使该函数尚未定义。特别是，您通常可以在其cond子句之一中自由使用递归调用的结果来创建某些函数的代码。结构和生成递归函数的设计配方的模板和编码步骤都依赖于此思想。

尽管上下文无关性促进了功能的设计，但它引起了两个问题。通常，上下文无关会导致递归评估中知识的丢失；函数不会“知道”是在完整列表中还是在该列表的一部分上调用了它。对于结构递归程序，这种知识的丢失意味着它们可能不得不多次遍历数据，从而导致性能损失。对于使用生成递归的函数，丢失意味着该函数可能根本无法计算结果。上一部分使用图遍历函数说明了第二个问题，该遍历函数无法为圆形图找到两个节点之间的路径。

本部分介绍了设计方案的变体，以解决此“上下文丢失”问题。由于我们希望保留（f a）无论返回的频率如何或在何处都返回相同结果的原理，因此唯一的解决方案是添加一个表示函数调用上下文的参数。我们将此附加参数称为累加器。在数据遍历期间，递归调用继续接收常规参数，而累加器相对于那些参数和上下文而变化。

显然，与上一章中的任何一种设计方法相比，正确地使用累加器设计功能要复杂得多。关键是要了解适当的论点和累加器之间的关系。以下各章说明如何使用累加器设计功能以及它们如何工作。

## 31 The Loss of Knowledge 

尽管结构方式不同，但根据结构配方设计的函数和生成功能都遭受了知识的损失。 本章通过两个示例（每个类别一个示例）说明缺少上下文知识如何影响功能的性能。 虽然第一部分是关于结构递归的，但第二部分是关于生成领域的关注。

### 31.1 A Problem with Structural Processing

**示例问题**您正在为一个几何团队工作，该团队将测量路段的长度。 团队要求您设计一个程序，将一系列道路点之间的相对距离转换为到某个起点的绝对距离。

### 31.2 A Problem with Generative Recursion

Let’s revisit the problem of “traveling” along a path in a graph:
**Sample Problem** Design an algorithm that checks whether two nodes are connected in a simple graph. In such a graph, each node has exactly one, directional connection to another, and possibly itself.

## 32 Designing Accumulator-Style Functions

上一章通过两个示例说明了积累额外知识的必要性。 在一种情况下，累加可以使函数易于理解，并且产生的功能要比原始版本快得多。 在其他情况下，必须积累功能才能正常工作。 但是，在这两种情况下，只有在适当设计的功能存在时，才需要积累。

从上一章的总结可以看出，累加器功能的设计有两个主要方面：
认识到函数受益于累加器； 和

对累加器代表什么的理解。

前两个部分讨论了这两个问题。 由于第二个主题很困难，因此第三部分将通过一系列示例将常规函数转换为累加函数来说明这一点。

## 34 小结

最后一部分是关于使用累加器进行设计的，累加器是一种在数据结构遍历期间收集知识的机制。添加累加器可以修复性能缺陷并消除端接问题。您将从本部分中学到的两个半设计课程：
第一步是认识到引入蓄能器的必要性。遍历从一个参数移到另一个参数时会“忘记”参数的各个部分。如果您发现这些知识可以简化功能的设计，请考虑引入一个累加器。第一步是切换到累加器模板。

关键步骤是制定累加器语句。后者必须表示累加器收集什么样的知识作为什么样的数据。在大多数情况下，accumulator语句描述原始参数与当前参数之间的差异。

第三步是次要步骤，是从累加器语句中得出：（a）累加器的初始值是什么；（b）在遍历步骤中如何保持其初始值；以及（c）如何利用其知识。

积累知识的想法无处不在，并且以许多不同的形式和形式出现。它在诸如ISL +之类的所谓功能语言中得到了广泛使用。使用命令式语言的程序员遇到累加器的方式有所不同，主要是通过原始循环构造中的赋值语句，因为后者无法返回值。设计这样的命令式累加器程序的过程与这里的累加器功能的设计一样，但是详细信息超出了本书有关系统程序设计的范围。

# 尾声：继续前进

正如我们在这里所说的，您已经到达了计算和编程或程序设计的本导论的结尾。 尽管还有更多关于这两个主题的知识，但这是停止，总结和展望未来的好方法。

## 电脑运算

在小学，您学会了用数字进行计算。首先，您使用数字来计算真实事物：三个苹果，五个朋友，十二个百吉饼。稍后，您遇到了加法，减法，乘法甚至除法；然后是分数。最终，您发现了有关变量和函数的信息，您的老师称其为代数。变量表示数字，而函数表示数字与数字的关系。

由于您在整个过程中都使用数字，因此您不会过多地使用数字来表示有关现实世界的信息。是的，您从三只熊，五只狼和十二匹马开始。但是到了高中，没有人让你想起这种关系。

当您从数学计算转移到计算时，从信息到数据再到返回的步骤变得至关重要。如今，程序可以处理音乐，视频，分子，化合物，业务案例研究，电气图和蓝图的表示。幸运的是，您不需要使用数字对所有这些信息进行编码，更糟糕的是，您只需使用0和1即可；如果必须的话，生活将是令人难以想象的乏味。取而代之的是，计算将算术和代数概括化，以便在编程时，您可以使用字符串，布尔值，字符，结构，列表，函数以及更多类型的数据进行编码，并且程序可以进行计算。

数据类别及其功能附带方程式定律，这些方程式解释了它们的含义，就像数字定律及其功能一样。尽管这些方程式定律很简单，例如“（+ 1 + 1）计算为2”和“（非#true）等于#false”，但是您可以使用它们来预测整个程序的行为。当您运行程序时，实际上只是应用了它的众多功能之一，您可以使用在《 Intermezzo 1：入门学生语言》中首先提到的beta规则来解释这一行为。将变量替换为值后，数据定律将接管，直到您只有一个值或另一个函数应用程序为止。但是，是的，这就是计算的全部。

## 程序设计

一个典型的软件开发项目需要许多程序员的协作，其结果包含数千个功能。在这样一个项目的生命周期中，程序员来来往往。因此，程序的设计结构实际上是跨时间程序员之间进行交流的一种手段。当您使用别人之前写的代码时，该程序应该表达其目的及其与其他部分的关系，因为其他人可能已经不在了。

在这样一个动态的环境中，如果程序员希望工作合理的小时数或生产高质量的产品，则必须以有纪律的方式创建程序。遵循系统的设计方法可以保证程序的组织性是可理解的。其他人则可以轻松地理解各个部分和整体，然后修复错误或添加新的功能。

本书的设计过程就是其中一种方法，每当您创建自己可能关心的程序时，都应该遵循它。您首先要分析信息世界，并描述代表信息的数据。然后，您制定一个计划，并列出所需的功能。如果此列表很大，则以迭代方式优化流程。您从功能的子集开始，这些功能可以快速产生客户可以与之交互的产品。当您观察到这些交互时，您将快速确定工作清单中的哪些元素接下来要解决。

设计程序或仅是功能，需要对其计算内容有严格的了解。除非可以用简洁的语句描述一段代码的目的，否则您将无法产生任何对将来的程序员有用的东西。编造并完成示例。将这些示例转换为一组测试。当涉及程序的未来修改时，此测试套件甚至更加重要。更改代码的任何人都可以重新运行这些测试，并再次确认该程序仍可用于基本示例。

最终，您的程序也会失败。其他程序员可能会以意外方式使用它。实际用户可能会发现预期行为与实际行为之间存在差异。因为您已经系统地设计了代码，所以您会知道该怎么做。您将为程序的主要功能制定一个失败的测试用例。从这个测试中，您将为主要功能提到的每个功能得出一个测试用例。通过新测试的那些功能不会导致失败。其中之一做到了；有时，一些人可能合谋制造一个错误。如果损坏的功能由其他功能组成，请恢复测试的创建；否则，您已找到问题的根源。当整个程序通过所有测试时，您将知道已经解决了问题。

无论您多么努力，功能或程序都不会在首次通过测试套件时完成。您必须花时间检查它是否存在设计缺陷和设计重复。如果找到任何设计模式，请形成新的抽象或使用现有的抽象来消除这些模式。

如果您遵守这些准则，则将尽力制作可靠的软件。之所以有效，是因为您了解其原因和工作方式。其他必须修改或增强您的软件的人会很快理解它，因为代码可以传达其过程和用途。通过本书的学习，您可以入门。现在，您必须练习，练习，练习。与第一本书相比，您将不得不学到更多有关程序设计和计算的知识。

## 以后，开发人员和计算机科学家

现在，您可能想知道接下来要学习什么。答案是更多的编程和更多的计算。

作为程序设计的学生，您的下一个任务是学习设计过程如何应用成熟的编程语言。这些语言中的一些像教学语言一样，过渡会很容易。其他人则需要不同的思维方式，因为他们提供了拼写数据定义（类和对象）和制定签名的方式，以便在程序运行之前对其进行交叉检查（类型）。学习Racket，这是本书教学语言背后的语言。有关可能的介绍，请参见“球拍领域”。此外，您还必须学习如何将设计过程扩展到所谓的框架（“堆栈”）和组件的使用和生产。粗略地说，框架抽象了许多软件系统所共有的功能，例如图形用户界面，数据库连接和Web连接。您需要学习实例化这些抽象，然后您的程序将组成这些实例以创建一致的系统。同样，学习创建新的系统组件也本质上是扩展技能的一部分。

作为计算专业的学生，​​您还必须扩大对计算过程的了解。本书着重于描述过程本身的法律。为了发挥真正的软件工程师的作用，您需要在理论和实践上都了解过程的成本。更深入地研究big-O的概念是朝这个方向迈出的第一步。学习衡量和分析程序性能是真正的目标，因为您将需要定期作为开发人员使用此技能。除了这些基本概念之外，您还将需要有关各种学科的硬件，网络，软件分层和专用算法的知识。

## Onward, Accountants, Journalists, Surgeons, and Everyone Else

Some of you wanted to see what computing and programming are all about. You now know that computing is merely a generalization of calculating, and you may sense how useful program design is to you. Even if you never develop programs again, you know what distinguishes a garage programmer from a serious software developer. When you interact with developers as a professional, you know that systematic design matters because it affects your quality of life and the bottom line of your business.

In reality, though, you are likely to “program” again, on a regular basis; you may just fail to see your activities in this light. Imagine a journalist for a moment. His story starts with the collection of information and data, laying it out, organizing it, and adding anecdotes. If you squint, you’ll see that this is only step one of the design process. Let’s turn to a family doctor who, after checking up on your symptoms, formulates a hypothesis of what might affect you. Do you see step two? Or, think of a lawyer who illustrates the point of an argument with a number of examples—an instance of step three. Finally, a civil engineer cross-checks the bridge as it is built to make sure it lives up to the blueprint and the underlying static calculations. Cross-checking is a form of testing—step six of the process; it compares actual measurements with expected values from the predictive calculations. Each of these professionals develops a system to work effectively and efficiently; and deep down, this system is likely to resemble the design process employed in this book.

Now, once you accept that many activities are a form of programming, you can transfer additional ideas from the design process to your own life. For example, if you recognize patterns, you may take the little additional time it takes to create an “abstraction”—a single point of control—to simplify your future work. So, regardless of whether you become an accountant or a doctor or something else, remember the design processes wherever you go and whatever you do.

## 从那时起，会计师，新闻工作者，外科医生以及其他所有人

你们中有些人想了解计算和编程的全部内容。您现在知道计算只是计算的概括，并且您可能会感觉到程序设计对您有多有用。即使不再开发程序，您也知道车库车库程序员与认真的软件开发人员的区别所在。当您作为专业人士与开发人员互动时，您会知道系统设计很重要，因为它会影响您的生活质量和业务底线。

但实际上，您很可能会定期再次“编程”；您可能因此无法看到自己的活动。想象一下记者。他的故事始于信息和数据的收集，布局，组织和添加轶事。着眼睛，您会发现这只是设计过程的第一步。让我们找一位家庭医生，他会在检查了您的症状之后，提出可能影响您的假设。您看到第二步了吗？或者，想像一个律师用许多例子来说明争论的要点，例如第三步。最终，一名土木工程师对桥梁的建造进行了交叉检查，以确保桥梁符合图纸和基础的静态计算。交叉检查是测试的一种形式-过程的第六步；它将实际测量结果与预测计算的期望值进行比较。这些专业人员中的每一个都开发出有效而高效地工作的系统；从根本上讲，该系统很可能类似于本书中采用的设计过程。

现在，一旦您接受许多活动是一种编程形式，就可以将其他想法从设计过程转移到您自己的生活中。例如，如果您识别出模式，则可能花费很少的额外时间来创建“抽象”（一个控制点）以简化未来的工作。因此，无论您是会计师还是医生，都无论身在何处，无论做什么都记住设计过程。
