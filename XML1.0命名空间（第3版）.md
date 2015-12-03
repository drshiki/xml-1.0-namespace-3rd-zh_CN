#XML1.0命名空间（第3版）
##W3C推荐标准 2009年12月8日
此版本：
[http://www.w3.org/TR/2009/REC-xml-names-20091208/](http://www.w3.org/TR/2009/REC-xml-names-20091208/)

最新版本：
[http://www.w3.org/TR/xml-names/](http://www.w3.org/TR/xml-names/)

以前的版本：
[http://www.w3.org/TR/2006/REC-xml-names-20060816/](http://www.w3.org/TR/2009/PER-xml-names-20090806/)

请参考此文档的[勘误表](http://www.w3.org/XML/2009/xml-names-errata)，勘误表上可能包含了规范的修正。

另请参阅[译版](http://www.w3.org/2003/03/Translations/byTechnology?technology=xml-names)。

此文档的非规范格式：[XML版本](http://www.w3.org/TR/2009/REC-xml-names-20091208/xml-names-10-3e.xml)和[高亮相对第二版更新部分的HTML版本](http://www.w3.org/TR/2009/REC-xml-names-20091208/xml-names-10-3e-diff.html)。

<hr>

##摘要
XML命名空间提供了一种简单的方式将以URI引用标识的命名空间应用于可扩展标记文档中使用的标记和属性以达到限制的效果。

##此文档状态
这一节描述了此文档出版时的状态，其他文档可能会替代此文档，w3c的出版列表以及这份技术报告的最新版本能够在http://www.w3.org/TR/ 的 [W3C技术报告索引](http://www.w3.org/TR/)上找到。

此文档作为[W3C核心工作组](http://www.w3.org/XML/Core/)的[W3C XML 活动](http://www.w3.org/XML/Activity.html)的一部分，英语版本是唯一的规范版本，其他的译版请参阅[http://www.w3.org/2003/03/Translations/byTechnology?technology=xml-names](http://www.w3.org/2003/03/Translations/byTechnology?technology=xml-names)。

已知的实现被详细记录在[命名空间1.1实现报告](http://www.w3.org/XML/2002/12/xml-names11-implementation.html)中（所有已知的命名空间1.1实现都支持命名空间1.0)，在[XML测试套件页面](http://www.w3.org/XML/Test/)可获得一个XML测试套件。

第三版包含了截至出版日期所有已知的勘误，并取代了之前的2006年8月16日版。

此版本已被广泛接受，是2009年8月6日的提议规范经过小幅修改后的版本。

请将此文档的错误发送至xml-names-editor@w3.org；[文档归案](http://lists.w3.org/Archives/Public/xml-names-editor/)可以在此获取，在[http://www.w3.org/XML/2009/xml-names-errata](http://www.w3.org/XML/2009/xml-names-errata)上可以查阅此文档的勘误表。

W3C成员，软件开发者，以及其他w3c工作组和感兴趣的团体已复查评审了此文档，并且董事会批准此文档作为W3C推荐规范，这是一份长期不变的文档并且可以作为其他文档的参考材料或者引用，W3C扮演着引起各方关注规范以及促进规范的广泛使用角色，旨在增强万维网的功能和互操作性。

W3C维护一个与工作组交付物相关的[公开专利信息列表](http://www.w3.org/2002/08/xmlcore-IPR-statements)，实际对专利[基本要求](http://www.w3.org/Consortium/Patent-Policy-20040205/#def-essential)事项知情的个人必须和[W3C专利政策第6节](http://www.w3.org/Consortium/Patent-Policy-20040205/#sec-Disclosure)保持一致公开信息。

##目录
1 目的和概要

1.1 符号与使用

2 XML命名空间

2.1 基本概念

2.2 使用URI作为命名空间名字

2.3 比较URI引用

3 声明命名空间

4 受限名

5 使用受限名

6 在元素与属性中应用命名空间

6.1 命名空间作用域

6.2 默认命名空间

6.3 属性的唯一性

7 文档一致性

8 处理程序一致性

##附录
A 规范引用

B 其他引用（非规范）

C XML命名空间内部结构（非规范）

D 自1.0版本后的修改（非规范）

E 鸣谢（非规范）

F 独立产品（非规范）

##1 目的和概要
我们预想到在XML的应用当中，一个XML文档中可能包含为多个软件模块定义的和使用的元素和属性（此处指“标记词汇”），此目标之一是确保模块化：重用那些在软件中易于理解和使用的词汇比重新起用新词更好。

对于那些包含多个词汇表而导致识别和冲突问题的文档。软件模块需要具备在其它软件包使用了相同元素名和属性名而导致“冲突”的情况下识别那些被设计成应该被处理的元素和属性的能力。

这些考虑要求文档构造机制需要具有名字构造机制以避免多个标记词汇表之间的命名冲突，这份规范描述了一种给元素和属性名指定拓展名来解决这些问题的机制——XML命名空间。

###1.1 符号和使用

在本文档强调时，使用关键字，必须，不允许，必需，应该，不应该，可以将按照[[Keywords]](http://www.w3.org/TR/REC-xml-names/#keywords)中的定义去解释。

注意许多产生式中的非终结符定义在XML规范中[[XML]](http://www.w3.org/TR/REC-xml-names/#XML)而不是在此文档中，当此文档中定义的非终结符具有和XML规范中定义的非终结符具有同样的名字时，在任何情况下此文档中的产生式将匹配XML规范中相应产生式匹配字符串的子集。

在此文档的产生式中，NSC是指一个“命名空间约束”，是遵守此规范的文档必须遵守的规则之一。

##2 XML命名空间

###2.1 基本概念

[定义：一个命名空间以一个URI引用标识，运用此文档所描述的机制，元素和属性的名字可以放置于xml命名空间内]

[定义：一个拓展名由命名空间名字和本地名字组成][定义：例如名字N在一个以I标识的命名空间内，那么I就是命名空间名字；例如N不在任一个命名空间内，那么就说命名空间名字为空][定义：以上两种情况中的N都是本地名字]统一管理URI和本地名字可以高效的避免名字冲突。

URI引用可能包含不允许在名字中使用的字符，并且很长造成使用不便，所以拓展名并不在xml文档的元素和属性命名中直接使用，而是使用受限命.[定义：受限名是一个被解释为命名空间的名字]在遵守此规范的文档中，元素和属性名使用受限名，在句法构成上或以带前缀或无前缀的方式出现。提供了一种基于属性声明的方式去将一个前缀和命名空间名字进行绑定，和将无前缀的元素名字和默认命名空间进行绑定，这些声明作用于他们出现的元素上，所以文档中的各个部分可能使用不同的绑定。遵守此文档的处理器必须识别和解释这些声明和前缀。

###2.2使用URI作为命名空间名字

尽管空字符串是一个合法的URI引用，但是不可以作为一个命名空间名字。

在命名空间声明中反对使用相对URI，包括同文档引用。

**注：**

反对使用相对URI是经过w3cXML全体投票决定的，这也说明了之后一些说明书例如DOM,xPath等等都不会对它们进行解释。

###2.3 比较URI引用

URI引用标识名将在判断一个名字是否属于所指定的命名空间或者比较两个名字是否属于同一个命名空间的时候发生比较。

[定义：两个URI将会被作为字符串对待，当且仅当它们表示的字符串是相同的时候它们表示同一个事物，也就是，它们是同样的字符序列]比较过程是大小写敏感的，且没有转义字符会被转换。

这个结论也就是说，它们表示不同的事物但可能指向相同的资源，它们和URI引用的差异仅仅发生在它们包含大小写，转义字符，或者基于一些具有不同基URI外部实体的情况下。（注：相对URI引用是被反对在命名空间命名中使用的）

在一个命名空间声明中，URI引用是属性的规范化值，所以XML字符替换和实体引用将在任何比较之前完成。

例如：

以下URI分别标识不同的命名空间，因为他们大小写不同

ttp://www.example.org/wine

http://www.Example.org/wine

http://www.example.org/Wine

以下URI也分别标识不同的命名空间

http://www.example.org/~wilbur

http://www.example.org/%7ewilbur

http://www.example.org/%7Ewilbur

为了避免和上述URI解引用时指向同样的资源的情况混淆，强烈反对在命名空间命名中使用%转义字符。

##3 声明命名空间

[定义：命名空间（或者更准确的说是命名空间绑定）是通过使用一族保留的属性去声明的，这些属性的名字必须是xmlns或者是以xmlns:的字符串，和其他属性一样，可以直接指定或者使用默认值]

命名空间声明中的属性命名规则

	[1]   	NSAttName	   ::=   	PrefixedAttName
									| DefaultAttName
	[2]   	PrefixedAttName	   ::=   	'xmlns:' NCName	[NSC: 保留的前缀和命名空间名字]
	[3]   	DefaultAttName	   ::=   	'xmlns'
	[4]   	NCName	   ::=   	Name - (Char* ':' Char*)	/* 不带“:”的XML名字 */

此属性的规范化的值必须为任意一个URI引用-命名空间名字标识一个命名空间-或一个空字符串，命名空间应该具备唯一性和永久性使得它可以保证预期工作效果。它的目的不是直接用于检索模式（如果存在的话），统一资源命名是被设计成这种目的的一个语法例子，然而，原始URL可以通过这种方法管理去实现同样的目的。


[定义：如果属性名匹配PrefixedAttName，那么NCName部分将提供命名空间前缀，用于将命名空间声明所在的元素的作用域内的元素，属性名和命名空间声明中属性的规范值关联起来]

[定义：如果属性名匹配DefaultAttName，那么命名空间声明中属性的规范值就是自声明所在元素作用域内的默认命名空间]默认命名空间和覆盖声明将在6.在元素与属性中应用命名空间中讨论。

命名空间声明的一个例子，将前缀edi和命名空间名字 http://ecommerce.example.org/schema相关联：

	<x xmlns:edi='http://ecommerce.example.org/schema'>
	  <!-- "edi" 前缀和http://ecommerce.example.org/schema绑定
	       ”x“元素的内容 -->
	</x>

**命名空间约束：保留的前缀和命名空间名字**

xml前缀定义性地与命名空间名字http://www.w3.org/XML/1998/namespace绑定，它可以，但不需要被声明，且不允许绑定到任何其他命名空间名字，其它前缀也不允许绑定到这个命名空间名字，且它不可以被声明用作默认命名空间。

前缀xmlns定义性地仅被声明用作与命名空间名字 http://www.w3.org/2000/xmlns/绑定，它不允许被声明，其他的前缀不允许和这个命名空间名字绑定，且它不允许被声明用作默认命名空间，元素名中不允许包含此前缀。

任何以X，M，L（不区分大小写）这三个字母顺序开头的是保留名，这意味着，

用户不应该使用它们，除非以后的说明书中有相关定义。

处理器不应该把它们当做致命错误。

##4 受限名

在遵守此规范的文档中，一些名字（和非终结符名相对应）必须以以下定义的受限名的形式出现：

受限名

	[7]   	QName	   ::=   	PrefixedName
								| UnprefixedName
	[8]   	PrefixedName	   ::=   	Prefix ':' LocalPart
	[9]   	UnprefixedName	   ::=   	LocalPart
	[10]   	Prefix	   ::=   	NCName
	[11]   	LocalPart	   ::=   	NCName

prefix提供了受限名的命名空间前缀部分，且必须和某个命名空间中使用的URI引用相关联。[定义：localpart提供了受限名的本地部分]

要注意的是前缀的作用仅是作为命名空间名字的占位符，应用程序在构造那些超出包含那些受限名的文档的作用范围的情况下使用的应该是命名空间名字而不是前缀。

##5 使用受限名

在遵守此规范的文档中，元素名必须以以下定义的受限名的形式出现：

元素名

	[12]   	STag	   ::=   	'<' QName (S Attribute)* S? '>' 	[NSC: Prefix Declared]
	[13]   	ETag	   ::=   	'</' QName S? '>'	[NSC: Prefix Declared]
	[14]   	EmptyElemTag	   ::=   	'<' QName (S Attribute)* S? '/>'	[NSC: Prefix Declared]

一个使用受限名用作元素名的例子：
	
	  <!-- the 'price' element's namespace is http://ecommerce.example.org/schema -->
	  <edi:price xmlns:edi='http://ecommerce.example.org/schema' units='Euro'>32.18</edi:price>

属性或以命名空间声明形式，或以以下定义的受限名出现：

属性
	
	[15]   	Attribute	   ::=   	NSAttName Eq AttValue
				| QName Eq AttValue	[NSC: Prefix Declared]
					[NSC: No Prefix Undeclaring]
					[NSC: Attributes Unique]、

一个使用受限名用作属性名的例子：

	<x xmlns:edi='http://ecommerce.example.org/schema'>
	  <!-- the 'taxClass' attribute's namespace is http://ecommerce.example.org/schema -->
	  <lineItem edi:taxClass="exempt">Baby food</lineItem>
	</x>

命名空间约束：前缀声明

命名空间前缀除了是xml或者xmlns的情况下，必须在使用该前缀的开始标签处的或者祖先元素的命名空间属性中已被声明。

命名空间约束：无前缀声明

命名空间前缀（例如NSAttName匹配PrefixedAttName的时候）的属性值必须不能为空。

这个约束可能是由外部实体声明的属性提供而不是直接在xml文档实体中提供的命名空间属性的而导致操作上的困难，这种声明可能对于基于未验证的XML处理程序的软件是不可读的。主要的xml应用程序，可能包括那些对命名空间敏感的，

元素名和属性名在DTD的声明中也可以以受限名的形式出现。

声明中的受限名

	[16]   	doctypedecl	   ::=   	'<!DOCTYPE' S QName (S ExternalID)? S? ('[' (markupdecl | PEReference | S)* ']' S?)? '>'
	[17]   	elementdecl	   ::=   	'<!ELEMENT' S QName S contentspec S? '>'
	[18]   	cp	   ::=   	(QName | choice | seq) ('?' | '*' | '+')?
	[19]   	Mixed	   ::=   	'(' S? '#PCDATA' (S? '|' S? QName)* S? ')*'
				| '(' S? '#PCDATA' S? ')'
	[20]   	AttlistDecl	   ::=   	'<!ATTLIST' S QName AttDef* S? '>'
	[21]   	AttDef	   ::=   	S (QName | NSAttName) S AttType S DefaultDecl

注意基于DTD的验证在以下情况下不是命名空间敏感的：一个DTD文档包含了可能以未解释的形式而不是以（命名空间名字，本地名字）组合出现在一个文档中元素和属性，

##6.在元素与属性中应用命名空间

###6.1命名空间作用域

一个声明前缀的命名空间声明的作用域从它出现的开始标签起直到对应的结束标签，不包括任何内部的相同的NSAttName声明的作用域，在空标签的情况下，作用域就是他自身。

命名空间将作用于作用域内匹配它所声明的前缀的元素和和属性名。

带前缀的元素和属性名相对应的拓展名把前缀绑定的URI作为命名空间名字，本地部分作为本地名字。

	<?xml version="1.0"?>
	
	<html:html xmlns:html='http://www.w3.org/1999/xhtml'>
	
	  <html:head><html:title>Frobnostication</html:title></html:head>
	  <html:body><html:p>Moved to 
	    <html:a href='http://frob.example.com'>here.</html:a></html:p></html:body>
	</html:html>

同一个元素可以声明多个命名空间前缀，如下例：

<?xml version="1.0"?>
<!-- both namespace prefixes are available throughout -->
<bk:book xmlns:bk='urn:loc.gov:books'
         xmlns:isbn='urn:ISBN:0-395-36341-6'>
    <bk:title>Cheaper by the Dozen</bk:title>
    <isbn:number>1568491379</isbn:number>
</bk:book>

###6.2默认命名空间

默认命名空间的作用域从它出现的开始标签起直到对应的结束标签，不包括任何内部的相同的NSAttName声明的作用域，在空标签的情况下，作用域就是他自身。

默认命名空间将作用于作用域内所有不带前缀的元素名，默认命名空间不直接作用于属性名，不带前缀的属性名的解析将由他们出现所在的元素所决定。

处于默认命名空间作用域时，不带前缀的元素名相对应的拓展名把前缀绑定的URI作为命名空间名字，本地部分作为本地名字。如果处于一个没有默认命名空间的作用域内时，那么命名空间名字值为空，无前缀的属性名的命名空间名字值总是为空，在所有情况下，本地名字就是本地部分（也就是和无前缀名字自身）。

	<?xml version="1.0"?>
	<!-- elements are in the HTML namespace, in this case by default -->
	<html xmlns='http://www.w3.org/1999/xhtml'>
	  <head><title>Frobnostication</title></head>
	  <body><p>Moved to 
	    <a href='http://frob.example.com'>here</a>.</p></body>
	</html>
	
	<?xml version="1.0"?>
	<!-- unprefixed element types are from "books" -->
	<book xmlns='urn:loc.gov:books'
	      xmlns:isbn='urn:ISBN:0-395-36341-6'>
	    <title>Cheaper by the Dozen</title>
	    <isbn:number>1568491379</isbn:number>
	</book>

一个较复杂的命名空间作用域例子：

	<?xml version="1.0"?>
	<!-- initially, the default namespace is "books" -->
	<book xmlns='urn:loc.gov:books'
	      xmlns:isbn='urn:ISBN:0-395-36341-6'>
	    <title>Cheaper by the Dozen</title>
	    <isbn:number>1568491379</isbn:number>
	    <notes>
	      <!-- make HTML the default namespace for some commentary -->
	      <p xmlns='http://www.w3.org/1999/xhtml'>
	          This is a <i>funny</i> book!
	      </p>
	    </notes>
	</book>

默认命名空间声明中的属性值可以为空，这样具有相同的效果，在它的作用域内没用默认命名空间。

	<?xml version='1.0'?>
	<Beers>
	  <!-- the default namespace inside tables is that of HTML -->
	  <table xmlns='http://www.w3.org/1999/xhtml'>
	   <th><td>Name</td><td>Origin</td><td>Description</td></th>
	   <tr> 
	     <!-- no default namespace inside table cells -->
	     <td><brandName xmlns="">Huntsman</brandName></td>
	     <td><origin xmlns="">Bath, UK</origin></td>
	     <td>
	       <details xmlns=""><class>Bitter</class><hop>Fuggles</hop>
	         <pro>Wonderful hop, light alcohol, good summer beer</pro>
	         <con>Fragile; excessive variance pub to pub</con>
	         </details>
	        </td>
	      </tr>
	    </table>
	  </Beers>

###6.3属性的唯一性

命名空间约束：属性唯一

在遵守此规范的文档内，所有标签不可以包含两个属性：

1.具有相同的名字，或者

2.具有受限名的相同的本地部分以及绑定到相同命名空间名字的前缀。

这个约束等同于要求所有元素不可以具有两个相同扩展名的属性。

如下，例子中全部空标签bad都是非法的

	<!-- http://www.w3.org is bound to n1 and n2 -->
	<x xmlns:n1="http://www.w3.org" 
	   xmlns:n2="http://www.w3.org" >
	  <bad a="1"     a="2" />
	  <bad n1:a="1"  n2:a="2" />
	</x>

然而，下面的却全是合法的，第二个是因为默认命名空间并没有作用于属性名。

	<!-- http://www.w3.org is bound to n1 and is the default -->
	<x xmlns:n1="http://www.w3.org" 
	   xmlns="http://www.w3.org" >
	  <good a="1"     b="2" />
	  <good a="1"     n1:a="2" />
	</x>

##7.文档一致性

这份规范应用于xml1.0文档，一个符合此规范的文档必须是xml1.0中所定义的格式良好的文档。

在遵守此规范的文档中，元素和属性名必须匹配Qname的产生式且满足所有命名空间约束，

[定义：一个文档遵守此规范，那么这个文档就是命名空间格式良好的]

命名空间有效的文档遵守以下：

所有元素或者属性名包含0个或1个冒号

没有任何实体名字，处理指令的目标，或者标识名字包含冒号。

此外，一个命名空间格式良好的文档也可以是命名空间有效的文档

##8.处理程序一致性

一个遵守此规范的处理程序必须报告违反命名空间良构性的行为，不包括必须检查命名空间名字是不是一个URI引用[RFC3986]。

[定义：一个合法的遵守此规范的xml处理程序如果额外提供了命名空间合法性报告，那么此程序是具备命名空阿验证的]。

##附录A：正式引用

关键字：
RFC 2119: Key words for use in RFCs to Indicate Requirement Levels, S. Bradner, ed. IETF (Internet Engineering Task Force), March 1997. Available at http://www.rfc-editor.org/rfc/rfc2119.txt 

RFC2141
    RFC 2141: URN Syntax, R. Moats, ed. IETF (Internet Engineering Task Force), May 1997. Available at http://www.rfc-editor.org/rfc/rfc2141.txt. 

RFC3986
    RFC 3986: Uniform Resource Identifier (URI): Generic Syntax, T. Berners-Lee, R. Fielding, and L. Masinter, eds. IETF (Internet Engineering Task Force), January 2005. Available at http://www.rfc-editor.org/rfc/rfc3986.txt 

RFC3629
    RFC 3629: UTF-8, a transformation format of ISO 10646, F. Yergeau, ed. IETF (Internet Engineering Task Force), November 2003. Available at http://www.rfc-editor.org/rfc/rfc3629.txt 

XML
    Extensible Markup Language (XML) 1.0, Tim Bray, Jean Paoli, C. M. Sperberg-McQueen, Eve Maler, and François Yergeau eds. W3C (World Wide Web Consortium). Available at http://www.w3.org/TR/REC-xml/. 

##B 其他非正式应用(非正式)

1.0 Errata
    Namespaces in XML Errata. W3C (World Wide Web Consortium). Available at http://www.w3.org/XML/xml-names-19990114-errata. 

1.0 2e Errata
    Namespaces in XML (Second Edition) Errata. W3C (World Wide Web Consortium). Available at http://www.w3.org/XML/2006/xml-names-errata. 

Relative URI deprecation
    Results of W3C XML Plenary Ballot on relative URI References In namespace declarations 3-17 July 2000, Dave Hollander and C. M. Sperberg-McQueen, 6 September 2000. Available at http://www.w3.org/2000/09/xppa. 

##C xml命名空间内部结构(非正式)

此附录已删除

##D自版本1.0以来的改变（非正式）

此版本包含了直至2009年七月20日的勘误表内容[1.0 Errata] [1.0 2e Errata]. 

#E致谢（非正式）

此工作反映了大量的人员的贡献，特别是w3c的xml工作组团体的参与以及特别兴趣小组和w3c元数据活动的参与，来自微软的Charles Frankston的贡献也是非常有价值的。

##F独立作品（非正式）

以下两个产品是现在这份规范的已修改后的最初两个版本，他们不再使用，放在此处以便此规范相互参考未标明日期的版本。

因为xml1.0的字母表最初使用的NCNameStartChar自xml1.0第四版后已经不再使用，NCNameStartChar在所有版本的xml规范中都被改作NCName.

	[5]   	NCNameChar	   ::=   	NameChar - ':' /* An XML NameChar, minus the ":" */
	[6]   	NCNameStartChar	   ::=   	NCName - ( Char Char Char* ) /* The first letter of an NCName */

 