---
title: Design Pattern 學習筆記
tags:
  - design pattern
  - note
date: 2020-01-18 17:25:34
# description: ' '
top: true
---

本篇文章為筆者在學習 design pattern 的一些筆記與摘要，並非完全原創，文章內容大多截取自[維基百科](https://en.wikipedia.org/wiki/Design_Patterns)與 [Learning Design Pattern in 30 real-case practices系列](https://ithelp.ithome.com.tw/users/20103220/ironman/1343)（已取得作者同意）<!-- more -->。

[GoF 設計模式](#GoF-設計模式)裡面的各種 pattern 主要會以下列形式介紹：

    Pattern 名稱
    - 情境
        （擷取自 ithome 系列文）
    - 設計
        （擷取自 ithome 系列文、wiki，自己的想法）
    - From wiki
        （擷取自 wiki）
    - wiki 的 diagram
    - Reference 來源

# S.O.L.I.D.

## Single responsibility principle (SRP)

- A class should have only one reason to change.
- __每個物件，不管是類別、函數，負責的功能，都應該只做一件事__。對函數而言，一個函數內，同時做了兩件以上的事情。當發生錯誤時，很難快速定位錯誤的原因。另外，也容易間接導至程式碼的可閱讀性降低。

> Reference:  
> [SOLID 之 單一職責原則（Single responsibility principle）](https://ithelp.ithome.com.tw/articles/10191955)  
> [09. 物件導向設計原則—SOLID](https://ithelp.ithome.com.tw/articles/10191553)

## The open closed principle (OCP)

- Software entities (class, modules, functions, etc.) __should be open for extension, but closed for modification__.
- 優點：降低修改風險；只有新增程式碼，舊有程式因為沒修改，所以理論上問題當然會比較少。
- 潛在問題：擴展的情境並不一定在設計階段就會發現，常常要到了需求調整才會知道

> Reference:  
> [SOLID 之 開關原則（Open-Close principle）](https://ithelp.ithome.com.tw/articles/10192105)

## Liskov Substitution Principle (LSP)

- __Subtypes must be substitutable for their base types__.
- 假設繼承實作並且 override 的時候，必須先思考修改內容的行為方向是否符合 parent class，如果行為不符合就意味著其實一開始就不屬於該 parent class
- Guide：
  - child class 必須完全實作 parent class 的方法
  - child class 可以有屬於自己的屬性和方法
  - 覆寫或實作 parent class 的 method 時，參數要與 parent class 定義的一樣，或是更寬鬆。比方說：parent class 的定義是 List，child class 則可以是 List 或 Collection
  - 覆寫或實作 parent class 的 method 時，回傳結果要跟 parent class 定義的一樣，或是縮小。比方說：parent class 是回傳 List ，child class 則可以回傳 List 或 ArrayList
  - Param type: child > parent
  - Return type: parent > child
- LSP 的目的：提高強健性

> Reference:  
> [SOLID 之 里氏替換原則（Liskov substitution principle）](https://ithelp.ithome.com.tw/articles/10192317)  
> [里氏替換原則 Liskov Substitution Principle (LSP)](https://medium.com/@f40507777/%E9%87%8C%E6%B0%8F%E6%9B%BF%E6%8F%9B%E5%8E%9F%E5%89%87-liskov-substitution-principle-adc1650ada53) 

## Interface Segregation Principle	(ISP)

- Clients should not be forced to depend on methods that they do not use.
> 直譯：「客戶不應該被強迫依賴他們不使用的方法」
- 優點：在需要多型時，會比較容易為 class 實作對應的 method

> Reference:  
> [SOLID 之 介面隔離原則（Interface segregation principle）](https://ithelp.ithome.com.tw/articles/10192464)

## Dependency inversion principle (DIP)

- High-level modules should not depend on low-level modules. Both should depend on abstractions.
- Abstractions should not depend on details. Details should depend on abstractions.

> ![](https://upload.wikimedia.org/wikipedia/commons/9/96/Dependency_inversion.png)
> from [wiki](https://zh.wikipedia.org/wiki/%E4%BE%9D%E8%B5%96%E5%8F%8D%E8%BD%AC%E5%8E%9F%E5%88%99)

> Reference:  
> [SOLID 之 依賴反轉原則（Dependency inversion principle）](https://ithelp.ithome.com.tw/articles/10192844)
 
## SOLID 之外的 Least Knowledge Principle

- Each unit should have only limited knowledge about other units: only units "closely" related to the current unit.

> Reference  
> [不在 SOLID 裡的 最小知識原則（Least Knowledge Principle）(https://ithelp.ithome.com.tw/articles/10193110)

# GoF 設計模式

## Creational design patterns

### Abstract Factory

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10194363)）

> As a 開發人員  
> I want 建立一個 Interface 來讓開發人員建立各資料庫連線物件  
> So that 避免在多個程式碼區塊放入建立資料庫連線的細節，降低耦合度

#### 設計

- 讓工廠類別（Factory Class）去做建立物件的細節，至於使用者只要使用 Factory 去建立需要的物件，不需要知道物件怎麼建立的，或是細節
- 常用的工廠模式：
  - Static factory（兩種使用方式）
    - 藉由參數來選擇要建立哪種連線（例如底下的 Create 方法）（[參考範例](https://github.com/KarateJB/DesignPattern.Sample/tree/master/Python/Samples/Factory)）
    - 直接呼叫對應的方法（例如底下的 CreateDataMart / CreateHistory / CreateOnline 方法）（[參考範例](https://github.com/KarateJB/DesignPattern.Sample/tree/master/Python/Samples/Factory)）
  - Abstract factory
    - 建立一個抽象工廠，再各自建立擴充的工廠來覆寫它
    - ___跟 Strategy 相關 ??___
  - Generic factory

#### From [wiki](https://en.wikipedia.org/wiki/Abstract_factory_pattern)

The abstract factory pattern provides a way to __encapsulate a group of individual factories that have a common theme without specifying their concrete classes__. In normal usage, the client software creates a concrete implementation of the abstract factory and then uses the generic interface of the factory to create the concrete objects that are part of the theme. __The client doesn't know (or care) which concrete objects it gets from each of these internal factories, since it uses only the generic interfaces of their products__. This pattern separates the details of implementation of a set of objects from their general usage and relies on object composition, as __object creation is implemented in methods exposed in the factory interface__.

> ![](https://upload.wikimedia.org/wikipedia/commons/a/aa/W3sDesign_Abstract_Factory_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Abstract_factory_pattern)

> Reference:  
> [DBA說換資料庫的帳號密碼，結果我花了一天改連線資訊$#&@#! (Factory 工廠模式) ](https://ithelp.ithome.com.tw/articles/10194363)

### Builder

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10194814)）

> As a 公司入口網站產品經理  
> I want 各BU在公司入口網站首頁看到屬於部門之資訊  
> So that 讓主管及同仁能迅速掌握資訊，並達到各部門之差異化。

#### 設計

- 建造者模式包含了以下元素：
    - Builder（建造者）：負責建造
    - Director（總監）：請建造者依序執行建造的動作
- 假設入口網站包含了"報表"及"員工請假資訊"，而各 BU 看到的報表類型或哪些員工（介於多少職等）請假要列出來的條件皆不一樣。（[參考範例](https://github.com/KarateJB/DesignPattern.Sample/tree/master/Python/Samples/Builder)）
- 和 Factory 的差別
  - 初看 Builder 會很難抓到使用的時機，因為 Factory 可以解決大部分的 Creational 需求。

#### From [wiki](https://en.wikipedia.org/wiki/Builder_pattern)

The intent of the Builder design pattern is to __separate the construction of a complex object from its representation__. By doing so the same construction process can create different representations.

> ![](https://upload.wikimedia.org/wikipedia/commons/8/87/W3sDesign_Builder_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Builder_pattern)

> Reference:  
> [為什麼裝潢師傅做出來的不是我想要的? 你需要... (Builder 建造者模式)](https://ithelp.ithome.com.tw/articles/10194814)

### Factory Method

#### From [wiki](https://en.wikipedia.org/wiki/Factory_method_pattern)

In class-based programming, the factory method pattern is a creational pattern that uses factory methods to deal with the problem of __creating objects without having to specify the exact class of the object that will be created__. This is done by creating objects by calling a factory method—either specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes—rather than by calling a constructor.

> ![](https://upload.wikimedia.org/wikipedia/commons/4/43/W3sDesign_Factory_Method_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Factory_method_pattern)

> Reference:  
> [參考範例](https://en.wikipedia.org/wiki/Factory_method_pattern#Python)

### Prototype

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10194600)）

> As a 系統使用者  
> I want 降低查詢線上交易報表的回應時間  
> So that 提高作業效率

#### 設計

- 原型模式有更深層的意義在於
  - 儲放原型
  - 方便的調用原型複製（Clone）功能

#### From [wiki](https://en.wikipedia.org/wiki/Prototype_pattern)

The prototype pattern is a creational design pattern in software development. It is used __when the type of objects to create is determined by a prototypical instance__, which is cloned to produce new objects. This pattern is used to:
  - __avoid subclasses of an object creator in the client application__, like the factory method pattern does.
  - __avoid the inherent cost of creating a new object in the standard way__ (e.g., using the 'new' keyword) when it is prohibitively expensive for a given application.

> ![](https://upload.wikimedia.org/wikipedia/commons/c/c4/W3sDesign_Prototype_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Prototype_pattern)

> Reference:  
> [收到一筆要建立複製人軍隊的訂單怎麼辦? (Prototype 原型模式)](https://ithelp.ithome.com.tw/articles/10194600)

### Singleton

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10196899)）
> As a 業務副總  
> I want 在明天的新產品線上預購活動，讓預購客戶取得一個唯一的預購號碼，而且要在產品發表會螢幕上打上線上預購的數目。  
> So that 由這個成功的產品發表會來增加產品曝光率

#### From [wiki](https://en.wikipedia.org/wiki/Singleton_pattern)

In software engineering, the singleton pattern is a software design pattern that __restricts the instantiation of a class to one "single" instance__. This is useful when exactly one object is needed to coordinate actions across the system.

> Reference:  
> [別再因為發號碼牌重複被客訴! (Singleton 單例模式)](https://ithelp.ithome.com.tw/articles/10196899)

## Structural design patterns

### Adapter

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10194158)）

> As a 資料分析者  
> I want 系統可以介接 XX 店家二代卡機傳回來的 EDI 並整理資料後存放在資料庫  
> So that 我們可以在資料庫做進一步客戶分析  

#### 設計

- 通過轉換已經存在類別的接口以適應而不改變它
- Adapter 分成兩種：
  - 繼承（Class way）
  - 組合（Object way）
- __Adapter 就像出國旅行用的萬用轉接頭__，負責將電器的插頭（來源）轉換成插座（Adaptee）可以用的模式。 來源只統一用 Adapter 這個接口，而不管細節

#### From [wiki](https://en.wikipedia.org/wiki/Adapter_pattern)

In software engineering, the adapter pattern is a software design pattern (also known as wrapper, an alternative naming shared with the decorator pattern) that __allows the interface of an existing class to be used as another interface__. It is often used to __make existing classes work with others without modifying their source code__.

> ![](https://upload.wikimedia.org/wikipedia/commons/e/e5/W3sDesign_Adapter_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Adapter_pattern)

> Reference:  
> [江湖走跳，轉接頭很重要! (Adapter 適配器模式)](https://ithelp.ithome.com.tw/articles/10194158)

### Bridge

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10193914)）

> As a 建立訂單的秘書  
> I want 可以在同一介面上依據各供應商、產品和是否急件列印不同格式的訂單  
> So that 秘書可以不必因為上述之差異而到處 KEY 重複的資料

#### 設計

1. 分離 Abstraction 及 Implementor，使兩者可獨立變化
2. 在 run time 設定 Abstraction 裡的 Implementor

- __Strategy 屬於行為模式（Behavioral design patterns）__
- __Bridge 屬於結構型模式（Structural design patterns）__，它將抽象和實做解耦合，使兩者可獨立的變化

#### From [wiki](https://en.wikipedia.org/wiki/Bridge_pattern)

The bridge pattern is a design pattern used in software engineering that is meant to __decouple an abstraction from its implementation so that the two can vary independently__, introduced by the Gang of Four. The bridge uses encapsulation, aggregation, and can use inheritance to separate responsibilities into different classes.

> ![](https://upload.wikimedia.org/wikipedia/commons/f/fd/W3sDesign_Bridge_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Bridge_pattern)

> Reference:  
> [橋來橋去! 以需求大化小，小化無(抽象)為目標! (Bridge 橋接模式)](https://ithelp.ithome.com.tw/articles/10193914)

### Composite

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10195044)）

> As a 人資經理  
> I want 系統可以帶出任一單位的組織圖  
> So that 可以讓老闆容易了解目前組織架構

#### From [wiki](https://en.wikipedia.org/wiki/Composite_pattern)

In software engineering, the composite pattern is a partitioning design pattern. The composite pattern describes a group of objects that are treated the same way as a single instance of the same type of object. __The intent of a composite is to "compose" objects into tree structures to represent part-whole hierarchies__. Implementing the composite pattern lets clients treat individual objects and compositions uniformly.

Composite __should be used when clients ignore the difference between compositions of objects and individual objects__. If programmers find that they are using multiple objects in the same way, and often have nearly identical code to handle each of them, then composite is a good choice; it is less complex in this situation to treat primitives and composites as homogeneous. 

> ![](https://upload.wikimedia.org/wikipedia/commons/6/65/W3sDesign_Composite_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Composite_pattern)

> Reference:  
> [老闆最大的興趣：異動組織! 但是下個月又調回來了... (Composite 組合模式)](https://ithelp.ithome.com.tw/articles/10195044)

### Decorator

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10195207)）

> As a 物流部秘書  
> I want 報價單系統可以在標準運費上加上其他服務費：加點/假日運送/延遲費"並費用最大化  
> So that 配合成本轉嫁客戶之策略，節首公司之支出

#### 設計

- 在不繼承原有類別情況下，對原類別加強或新增功能

#### From [wiki](https://en.wikipedia.org/wiki/Decorator_pattern)

In object-oriented programming, the decorator pattern is a design pattern that __allows behavior to be added to an individual object, dynamically, without affecting the behavior of other objects from the same class__. The decorator pattern is often useful for adhering to the Single Responsibility Principle, as it allows functionality to be divided between classes with unique areas of concern. The decorator pattern is __structurally nearly identical to the chain of responsibility pattern__, the difference being that in a chain of responsibility, exactly one of the classes handles the request, while for the decorator, all classes handle the request. 

> ![](https://upload.wikimedia.org/wikipedia/commons/8/83/W3sDesign_Decorator_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Decorator_pattern)

> Reference:  
> [標準永遠有例外! 但是千萬不要以為自己可以改標準... (Decorator 裝飾者模式)](https://ithelp.ithome.com.tw/articles/10195207)

### Facade

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10193671)）

> As a 資料分析者  
> I want 使用者在執行任一系統功能時，系統可以同時記錄使用記錄在文字檔和資料庫  
> So that 我們可以知道使用者何時使用了該功能和次數

#### 設計

- 封裝商業邏輯並提供簡單介面，以達到易使用、可讀性、減少依賴的目的

#### From [wiki](https://en.wikipedia.org/wiki/Facade_pattern)

The facade pattern (also spelled façade) is a software-design pattern commonly used in object-oriented programming. Analogous to a facade in architecture, a facade is an object that serves as a front-facing interface masking more complex underlying or structural code.

A facade can:
  - improve the readability and usability of a software library by __masking interaction with more complex components behind a single (and often simplified) API__
  - provide a context-specific interface to more generic functionality (complete with context-specific input validation)
  - serve as a launching point for a broader refactor of monolithic or tightly-coupled systems in favor of more loosely-coupled code

__Developers often use the facade design pattern when a system is very complex or difficult to understand__ because the system has a large number of interdependent classes or because its source code is unavailable. __This pattern hides the complexities of the larger system and provides a simpler interface to the client__.

> ![](https://upload.wikimedia.org/wikipedia/commons/9/96/W3sDesign_Facade_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Facade_pattern)

> ![](https://upload.wikimedia.org/wikipedia/en/5/57/Example_of_Facade_design_pattern_in_UML.png)
> from [wiki](https://en.wikipedia.org/wiki/Facade_pattern)

> ReferenceL  
> [不用看書就會，但不一定會唸的... (Facade 外觀模式)](https://ithelp.ithome.com.tw/articles/10193671)

### Flyweight

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10195427)）

> As a 公司官網管理者  
> I want 產品頁面可以更快速的顯示(<=2.0Sec)  
> So that 瀏覽者有好的使用者體驗

#### 設計

- Flyweight 使用的時機如下：
  - __共享對像會頻繁的建立__，而且每次建立需耗費可觀的資源
  - 共享對像適合為獨立且輕量的的小元素，且不會由本身來改變其狀態和資料
  - 提供介面讓外部程式改變其狀態和資料
- 網站的暫存資料很適合將其作為 Flyweight 物件存放並共享給整個網站使用，因為暫存資料一般有以下特性：
  - __變動性小__
  - 因資料共用性，一般習慣將暫存以小範圍管理之方式建立
- 注意 Flyweight 為 Structural design pattern 而非 Creational design pattern，它通常會搭配 Factory，由工廠提供資料，而 Flyweight 提供一個共享的結構。

#### From [wiki](https://en.wikipedia.org/wiki/Flyweight_pattern)

A flyweight is an object that __minimizes memory usage by sharing as much data as possible with other similar objects__; it is a way to use objects in large numbers when a simple repeated representation would use an unacceptable amount of memory. Often some parts of the object state can be shared, and it is common practice to hold them in external data structures and pass them to the objects temporarily when they are used. 

> ![](https://upload.wikimedia.org/wikipedia/commons/4/4e/W3sDesign_Flyweight_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Flyweight_pattern)

> Reference:  
> [程式碼也需要瘦身! (Flyweight 享元模式)](https://ithelp.ithome.com.tw/articles/10195427)

### Proxy

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10195625)）

> As a 物流部秘書  
> I want 報價單系統可以在其他服務費加上更多彈性：
>   - 加點: 若單趟載超過兩個點，第三個點開始每加一點加收總價*20%
>   - 延遲費: 超過兩小時後的時間，改為每小時NTD$1,000
>
> So that 業務可在大單採原來之計價，但小單則採新制

#### 設計

- What problems can the Proxy design pattern solve?
  - The access to an object should be controlled.
  - Additional functionality should be provided when accessing an object.

#### Proxy 和 Adapter 的差異（from [ithome](https://ithelp.ithome.com.tw/articles/10195625)）

- Adapter
  - 特性：
    - 提供不同的介面，而主程式依賴於實體 Adapter 類別
    - 當套用 Adapter 時，__主程式使用的介面會改變__
  - 使用時機：
    - __在不改變原始介面下__，提供不同的介面讓主程式可以使用原介面的功能
    - 目的在於__適應__，不改變原功能的目的
- Proxy
  - 特性：
    - 提供相同的介面，讓主程式依賴於抽象
    - __主程式使用的介面和方式不會改變__
  - 使用時機：
    - 在不改變主程式的行為下，讓代理完成其它實作類別的功能
    - 目的在於__控制__，可__加強或改變原功能的目的__

#### From [wiki](https://en.wikipedia.org/wiki/Proxy_pattern)

A proxy, in its most general form, is a class functioning as an interface to something else. The proxy could interface to anything: a network connection, a large object in memory, a file, or some other resource that is expensive or impossible to duplicate. In short, a proxy is a wrapper or agent object that is being called by the client to access the real serving object behind the scenes. Use of the proxy can simply be forwarding to the real object, or can provide additional logic. In the proxy, extra functionality can be provided, for example caching when operations on the real object are resource intensive, or checking preconditions before operations on the real object are invoked. For the client, usage of a proxy object is similar to using the real object, because both implement the same interface.

> ![](https://upload.wikimedia.org/wikipedia/commons/6/6e/W3sDesign_Proxy_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Proxy_pattern)

> Reference:  
> [老闆說給客戶的報價要有彈性! 但是只能多算不能少算! (Proxy 代理模式)](https://ithelp.ithome.com.tw/articles/10195625)

## Behavioral design patterns

### Chain of responsibility

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10193451)）

> As a 產品經理  
> I want 多國語系介面  
> So that 顯示使用者對應的語系內容

#### 設計

- 根據條件來定義一個有責任的接收者，以處理一個請求或將其轉發給鏈上的下一個接收者（如果有的話）
- chain 上的接收者可以選擇直接丟給下一個適合的接收者，或是選擇做事再判斷適合的接收者後往後丟

#### From [wiki](https://en.wikipedia.org/wiki/Chain-of-responsibility_pattern)

In object-oriented design, the chain-of-responsibility pattern is a design pattern __consisting of a source of command objects and a series of processing objects__. Each processing object contains logic that defines the types of command objects that it can handle; the rest are passed to the next processing object in the chain.

> ![](https://upload.wikimedia.org/wikipedia/commons/6/6a/W3sDesign_Chain_of_Responsibility_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Chain-of-responsibility_pattern)

> Reference:  
> [職場第一條規則：事情不要接了傻傻做，而是要交給負責的人! (Chain of Responsibility 職責鍊模式)](https://ithelp.ithome.com.tw/articles/10193451)

### Command 未完成
### Interpreter

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10193177)）

> As a 資料分析者  
> I want 系統可以介接店家傳回來的 EDI 並整理資料後存放在資料庫  
> So that 我們可以在資料庫做進一步客戶分析

#### 設計

- 定義一個表示法，使用表示法來解釋（翻譯）語言中的句子

#### From [wiki](https://en.wikipedia.org/wiki/Interpreter_pattern)

In computer programming, the interpreter pattern is a design pattern that specifies how to evaluate sentences in a language. __The basic idea is to have a class for each symbol (terminal or nonterminal) in a specialized computer language.__ The syntax tree of a sentence in the language is an instance of the composite pattern and is used to evaluate (interpret) the sentence for a client.

> ![](https://upload.wikimedia.org/wikipedia/commons/3/33/W3sDesign_Interpreter_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Interpreter_pattern)

> 感覺跟 strategy 的概念有點相似，對於同一個介面個別實作細節

> Reference:   
> [雞同鴨講也可以通! (Interpreter 解譯器模式)](https://ithelp.ithome.com.tw/articles/10193177)

### Iterator 未完成
### Mediator 未完成
### Memento 未完成
### Observer 未完成
### State 未完成

### Strategy

#### 情境（from [ithome](https://ithelp.ithome.com.tw/articles/10192935)）

> As a 資料分析者  
> I want 使用者在執行任一系統功能時，系統可以記錄使用記錄在文字檔  
> So that 我們可以知道使用者何時使用了該功能和次數

#### 設計

- 定義多個演算法，各別封裝這些演算法，並讓它們可以互換

#### From [wiki](https://en.wikipedia.org/wiki/Strategy_pattern)

In computer programming, the strategy pattern (also known as the policy pattern) is a behavioral software design pattern that enables __selecting an algorithm at runtime__. Instead of implementing a single algorithm directly.

> ![](https://upload.wikimedia.org/wikipedia/commons/4/45/W3sDesign_Strategy_Design_Pattern_UML.jpg)
> from [wiki](https://en.wikipedia.org/wiki/Strategy_pattern)

> Reference:  
> [謀略設計模式! 學習首重策略! (Strategy 策略模式) ](https://ithelp.ithome.com.tw/articles/10192935)

### Template 未完成
### Visitor 未完成

https://ithelp.ithome.com.tw/articles/10192379
https://github.com/KarateJB/eBooks/tree/master/Design%20Patterns
https://en.wikipedia.org/wiki/Design_Patterns