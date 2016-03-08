title: 'MFC '
tags:
  - MFC
id: 71
categories:
  - 昔日归档
date: 2008-06-24 10:52:38
---

**MFC**,[微软](http://yangtao.wordpress.com.cn/view/2353.htm)基础类(**Microsoft Foundation Classes**)，同VCL类似，是一种Application Framework，随微软Visual C++ 开发工具发布。目前最新版本为8.0（截止2007年初）。该类库提供一组通用的可重用的类库供开发人员使用。大部分类均从CObject 直接或间接派生，只有少部分类例外。

MFC 应用程序的总体结构通常由 由开发人员从MFC类派生的几个类和一个CWinApp类对象（应用程序对象）组成。MFC 提供了MFC AppWizard 自动生成框架。

Windows 应用程序中，MFC 的主包含文件为"Afxwin.h"。

此外MFC的部分类为MFC/ATL 通用，可以在Win32 应用程序中单独包含并使用这些类。

由于它的易用性，初学者常误认为VC++开发必须使用MFC。这种想法是错误的。作为Application Framework，MFC的使用只能提高某些情况下的开发效率，只起到辅助作用，而不能替代整个Win32 程序设计。
----------------------------------------------------
（下面是原词条）
----------------------------------------------------
**MFC**,微软基础类(**Microsoft Foundation Classes**),实际上是微软提供的,用于在**C++**环境下编写应用程序的一个框架和引擎,**VC++**是**WinOS**下开发人员使用的专业**C++ SDK**(**SDK,Standard SoftWare Develop Kit,专业软件开发平台**),MFC就是挂在它之上的一个辅助软件开发包,MFC作为与VC++血肉相连的部分(注意C++和VC++的区别:C++是一种程序设计语言,是一种大家都承认的软件编制的通用规范,而VC++只是一个编译器,或者说是一种编译器+源程序编辑器的IDE,WS,PlatForm,这跟[Pascal](http://yangtao.wordpress.com.cn/view/9355.htm)和Dephi的关系一个道理,Pascal是Dephi的语言基础,Dephi使用Pascal规范来进行Win下应用程序的开发和编译,却不同于[Basic](http://yangtao.wordpress.com.cn/view/7334.htm)语言和[VB](http://yangtao.wordpress.com.cn/view/3063.htm)的关系,Basic语言在VB开发出来被应用的年代已经成了Basic语言的新规范,VB新加的Basic语言要素,如面向对象程序设计的要素,是一种性质上的飞跃,使VB既是一个IDE,又成长成一个新的程序设计语言),MFC同BC++集成的VCL一样是一个非外挂式的软件包,类库,只不过MFC类是微软为VC++专配的..

**MFC是Win [API](http://yangtao.wordpress.com.cn/view/16068.htm)与C++的结合**,API,即微软提供的WinOS下应用程序的编程语言接口,是一种软件编程的规范,但不是一种程序开发语言本身,可以允许用户使用各种各样的第三方(如我是一方,微软是一方,Borland就是第三方)的编程语言来进行对Win OS下应用程序的开发,使这些被开发出来的应用程序能在WinOS下运行,比如VB,VC++,[Java](http://yangtao.wordpress.com.cn/view/29.htm),Dehpi编程语言函数本质上全部源于API,因此用它们开发出来的应用程序都能工作在WinOS的消息机制和绘图里,遵守WinOS作为一个操作系统的内部实现,这其实也是一种必要,微软如果不提供API,这个世上对Win编程的工作就不会存在,微软的产品就会迅速从时尚变成垃圾,上面说到MFC是微软对API函数的专用C++封装,这种结合一方面让用户使用微软的专业C++ SDK来进行Win下应用程序的开发变得容易,因为MFC是对API的封装,微软做了大量的工作,隐藏了好多程序开发人员在Win下用C++ &amp; MFC编制软件时的大量内节,如应用程序实现消息的处理,设备环境绘图,这种结合是以方便为目的的,必定要付出一定代价(这是微软的一向作风),因此就造成了MFC对类封装中的一定程度的的冗余和迂回,但这是可以接受的..

最后要明白MFC不只是一个功能单纯的界面开发系统,它提供的类绝大部分用来进行界面开发,关联一个窗口的动作,但它提供的类中有好多类不与一个窗口关联,即类的作用不是一个界面类,不实现对一个窗口对象的控制(如创建,销毁),而是一些在WinOS(用MFC编写的程序绝大部分都在WinOS中运行)中实现内部处理的类,如数据库的管理类等,学习中最应花费时间的是消息和设备环境,对C++和MFC的学习中最难的部分是指针,C++面向对像程序设计的其它部分,如数据类型,流程控制都不难,建议学习数据结构C++版..http://home.nuc.edu.cn/~yayu/look.php?id=25
MFC是微软封装了的API。什么意思呢？windows作为一个提供功能强大的应用程序接口编程的操作系统，的确方便了许多程序员，传统的win32开发（直接使用windows的接口函数API）对于程序员来说非常的困难，因为
API函数实在太多了，而且名称很乱，从零构架一个窗口动辄就是上百行的代码。MFC是面向对象程序设计与Application framework的完美结合，他将传统的API进行了分类封装，并且为你创建了程序的一般框架，