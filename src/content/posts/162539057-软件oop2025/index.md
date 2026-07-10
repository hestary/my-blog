---
title: "软件oop2025"
published: 2026-07-03
description: ""
tags: ["javascript", "开发语言", "ecmascript"]
category: "当前文章被以下社区和专栏收录："
draft: false
---

- 


**1. 如果一个类不能实例化对象，那么这个类一定是抽象类。✗ 错误。**

反例：如果一个类的所有构造函数都是 `private`，则外部无法实例化对象，但它不一定是抽象类（没有纯虚函数）。例如单例模式的类。另外，抽象类必须有纯虚函数（`=0`），这是"不能实例化"的充分条件，但不是必要条件。

---

**2. 针对 A 类型的对象 s，语句 `s=1;` 一定会出现编译错误。✗ 错误。**

如果类 A 定义了一个非 `explicit` 的单参数构造函数（如 `A(int)`），编译器会自动将整数 `1` 隐式转换为 A 类型的临时对象，再调用赋值运算符。这时 `s=1;` 不会报编译错误。

---

**3. 一个类中如果没有定义虚函数，则该类不需要生成虚表。✗ 错误。**

如果该类继承自一个包含虚函数的基类，即使它自己没有新增虚函数，它仍然继承了基类的虚函数，因此同样需要虚表。另外，虚析构函数也是虚函数。

---

**4. 类的任何数据成员不可以是该类本身的类型。✗ 错误。**

类的非静态数据成员不能是类本身的**实例**（此时类类型不完整，无法确定大小），但**可以**是该类本身的指针（`A*`）或引用（`A&`），也可以有该类的静态数据成员（`static A s;`）。

---

**5. 一个类的对象的大小只和该类的数据成员有关。✗ 错误。**

对象大小还与以下因素有关：

虚函数表指针（vptr，通常 4 或 8 字节）
- 内存对齐（padding）
- 基类子对象的大小（继承而来）
- 空基类优化（EBO）等因素

---

**6. 函数的参数的个数、类型、顺序以及返回类型都是区分函数重载的依据。✗ 错误。**

返回类型**不能**作为函数重载的依据。函数重载只能通过函数名 + 参数列表（个数、类型、顺序）来区分。若仅返回类型不同而参数列表相同，编译器无法区分。

---

**7. 同一类的成员函数 `void f(A s);` 和成员函数 `void f(A s) const;` 是重载函数。✓ 正确。**

`const` 修饰符是成员函数签名的一部分。const 成员函数的 `this` 指针类型为 `const A*`，非 const 成员函数的 `this` 指针类型为 `A*`，二者构成合法的重载。

---

**8. 父类的数据成员可以在其派生类构造函数中进行初始化。✗ 错误。**

父类的数据成员只能由父类自己的构造函数初始化。派生类构造函数可以在初始化列表中调用父类的构造函数来间接初始化父类成员，但不能直接在初始化列表中单独列出父类成员的名字。

`// 错误：派生类不能直接初始化基类成员
B(int x) : base_member(x) {}  // 编译错误
// 正确：通过基类构造函数
B(int x) : A(x) {}
`

---

**9. 一个类中需要深度拷贝构造函数的情况下，析构函数一般也要进行特殊处理。✓ 正确。**

这就是 C++ 的**规则三/五（Rule of Three/Five）**：如果一个类需要自定义析构函数、拷贝构造函数或赋值运算符中的任意一个，通常三者都需要自定义。深度拷贝意味着类管理了动态资源，析构函数必须释放这些资源以防内存泄漏。

---

**10. 一个类的全部构造函数都为 private 属性，则该类既不能实例化也不能被继承。✗ 错误。**

"不能实例化"是错误的：可以通过**静态成员函数**（工厂方法）或**友元函数/类**来创建对象。例如单例模式正是利用私有构造函数 + 静态方法实现实例化。

"不能被继承"基本正确（派生类需要调用基类构造函数），但如果派生类是基类的友元，则仍可以继承。

---


虽然每个类的成员函数代码在编译期就确定了，但**调用哪个类的函数版本只能在运行时根据对象的实际类型来决定**。当通过基类指针/引用调用虚函数时，编译期无法知道该指针指向的到底是基类对象还是某个派生类对象。虚表（vtable）存储了每个类中虚函数的实际地址，通过 vptr → vtable → 函数地址的间接调用机制，实现了**动态绑定（dynamic binding）**，即运行时多态。

---


如果形参不是引用而是**传值**，则调用拷贝构造函数时需要先拷贝实参以创建形参，而这个拷贝过程又会调用拷贝构造函数自身，从而导致**无限递归**。使用引用传递避免了实参的拷贝，直接引用源对象。

---


**不可以。** 以下成员函数不能或不应设为虚函数：

- **构造函数**：构造时对象的类型必须完全确定，虚函数机制在构造期间尚未完全建立（构造时 vptr 指向当前正在构造的类的虚表）
- **静态成员函数**：属于类而非对象，没有 `this` 指针，无法进行动态绑定
- **非成员函数**：虚函数机制仅适用于成员函数
- （补充）**内联函数**技术上可以声明为虚，但通过指针/引用调用时无法内联

---


位置示例作用函数末尾（成员函数）`void f() const;`承诺不修改对象数据成员；可被 const 对象调用参数列表`void f(const int& x)`保证函数内部不修改参数值返回类型`const int& f()`返回的引用指向的对象不可被修改参数中的指针指向`void f(const char* p)`指针指向的内容不可变参数中的指针本身`void f(char* const p)`指针本身不可变
---


将拷贝构造函数和赋值运算符设为 `private`（传统 C++98），或在 C++11 中使用 `= delete`：

`class A {
public:
    A() {}
private:
    A(const A&);              // 私有拷贝构造函数
    A& operator=(const A&);   // 私有赋值运算符
};

// C++11 推荐写法：
class A {
public:
    A() = default;
    A(const A&) = delete;
    A& operator=(const A&) = delete;
};
`

---


`f` 可能是以下三种之一：

- **基类**：`f` 是基类的类名，调用基类的构造函数，如 `class A : public f { ... };`
- **成员对象**：`f` 是类 A 中某个成员对象的名字（其类型有对应参数的构造函数）
- **const/constexpr 成员**（C++11）：初始化 const 或引用成员

最常见的情况是成员对象或基类。

---


对象类型创建时机销毁时机生命周期**全局对象**`main()` 执行前`main()` 结束后整个程序运行期**局部动态对象**（`new`）执行 `new` 时执行 `delete` 时（或永不）由程序员控制**局部静态对象**第一次执行到定义语句时`main()` 结束后从首次构造到程序结束**静态数据成员**`main()` 执行前`main()` 结束后整个程序运行期，所有对象共享
---


维度含义C++ 语法支持**值的动态**程序运行时变量的值可变变量赋值、指针/引用的重新绑定**空间的动态**运行时按需分配/释放内存`new`/`delete`、`malloc`/`free`、STL 容器（`vector` 等自动扩容）**类型的动态**运行时根据实际类型决定行为虚函数 + 继承（多态）、`dynamic_cast`、RTTI（`typeid`）**代码的动态**运行时决定执行哪段代码虚函数（vtable 分发）、函数指针、`std::function` + lambda、函数对象
四种动态层层递进：值的动态 → 空间的动态 → 类型的动态 → 代码的动态，体现了程序从"写死"到"灵活适配"的柔性设计。

---


**`<>` 的用途：**

- **模板**：`template<typename T>`、`vector<int>`、`function<void(int)>`
- **标准库头文件**：`#include <iostream>`
- **比较运算符**：`a < b`、`a > b`
- **模板特化**：`template<> class A<int> { ... };`

**`()` 的用途：**

- 函数调用、表达式分组、类型转换（`int(x)`）、构造函数的初始化列表分隔

**关系：** `<>` 主要用于**编译期**（泛型/模板），`()` 主要用于**运行期**（函数调用）。模板实例化时二者结合：`vector<int>()` — `<>` 指定类型参数，`()` 调用默认构造函数。

---


**可以。** C 语言是图灵完备的，理论上能完成任何计算任务，操作系统内核大多用 C 编写。

**缺点：**

- 不支持 OOP（须用 `struct` + 函数指针模拟，代码复杂、易出错、可读性差）
- 无模板/泛型（须用 `void*` + 宏，类型不安全）
- 无异常处理（须靠返回值 + `goto`/`setjmp`，工程性差）
- 无自动资源管理（RAII），手动管理内存极易泄漏
- 缺乏 STL 等标准抽象，重复造轮子
- 无函数重载/运算符重载，代码冗长

---


此题考察**适配器模式（Adapter Pattern）** 的应用。

`// ========== 目标接口（导弹端）==========
class Missile {
public:
    virtual ~Missile() = default;
    virtual void launch() = 0;              // 发射
    virtual void reportStatus() = 0;        // 数据回传
    virtual string type() const = 0;        // 型号标识
};

class Tomahawk : public Missile { /* 战斧系列 */ };
class Bulava   : public Missile { /* 白杨系列 */ };
class Perseus  : public Missile { /* 比音系列 */ };

// ========== 适配者接口（战斗机端）==========
class Fighter {
public:
    virtual ~Fighter() = default;
    virtual void mount(Missile&) = 0;       // 机械挂载
    virtual void fire() = 0;                // 开火
    virtual string model() const = 0;
};

class F16 : public Fighter { /* ... */ };
class F22 : public Fighter { /* ... */ };
class F35 : public Fighter { /* ... */ };
class Su27 : public Fighter { /* ... */ };
class Su30 : public Fighter { /* ... */ };

// ========== 适配器（核心）==========
class UniversalAdapter {
public:
    // 机械挂载：将任意导弹挂到任意战机上
    virtual bool mountOn(Fighter& f, Missile& m) = 0;

    // 数据监测：读取导弹状态
    virtual void monitor(Missile& m) = 0;

    // 控制功能：发送发射指令
    virtual void controlLaunch(Fighter& f, Missile& m) = 0;

    virtual ~UniversalAdapter() = default;
};

// ========== 具体适配器 ==========
class ConcreteAdapter : public UniversalAdapter {
public:
    bool mountOn(Fighter& f, Missile& m) override {
        f.mount(m);
        return true;
    }
    void monitor(Missile& m) override {
        m.reportStatus();
    }
    void controlLaunch(Fighter& f, Missile& m) override {
        m.launch();
    }
};
`
**设计要点：**

- **可复用**：适配器与具体型号解耦，新增战斗机/导弹型号无需修改适配器
- **可扩展**：可派生新的适配器变体支持不同的对接协议
- **可维护**：接口清晰、职责单一，每类只关注自己的功能

---


**

在软件工程**的进化之路上，**C++** 以其对硬件的高效抽象和面向对象思想，持续为高可靠性系统奠基。今天，**具身人工智能**的感知-推理-行动闭环依赖实时 C++ 推理引擎驱动；**量子技术**的量子纠错和电路模拟同样由 C++ 承载计算；**核聚变**等离子体控制（如 ITER 的 EPICS 框架）用 C++ 实现微秒级反馈环路。更遥远的思辨中，**硅基生命**若诞生，或将运行在 C++ 编译的内核之上，于冯·诺依曼架构与新生计算基板之间架起桥梁。从二进制到智能涌现，**文化**的数字化存储和传播同样依赖软件工程的构造——代码正成为新时代的"活文字"，承载并塑造着文明的形态。

---


`class A{
    int * p;
public:
    A(int k=9){p = new int[k];}
};
void main(){
    A * s = new A;
    delete s;
}
`
**错误：**

- **数组内存泄漏**：构造函数中 `p = new int[k]` 使用 `new[]` 分配数组，但类 A 没有定义析构函数来执行 `delete[] p`。`delete s` 仅释放 A 对象本身，不会释放 p 指向的动态数组。
- **缺少拷贝控制**：根据规则三，存在动态内存的类还需禁用或实现拷贝构造函数和赋值运算符，防止浅拷贝导致的双重释放。

**改正：**

`class A {
    int *p;
public:
    A(int k = 9) : p(new int[k]) {}
    ~A() { delete[] p; }
    A(const A&) = delete;
    A& operator=(const A&) = delete;
};
`

---


`class A{
    int val;
public:
    void display() const {set();}   // 错误！const函数调用非const函数
    void set(){cout<<val<<endl;}
    A(int = 0);
};
`
**错误：** `display()` 是 const 成员函数，其 `this` 类型为 `const A*`，但它调用了非 const 的 `set()`。const 成员函数既不能修改对象状态，也不能调用可能修改对象状态的非 const 函数。

**改正一（推荐）：** 将 `set()` 也声明为 const：

`void set() const { cout << val << endl; }
`
**改正二：** 去掉 `display()` 的 const 修饰符。

---


`class A{
    int vala;
public:
    virtual void set()=0;   // 纯虚函数，A是抽象类
};
class B: public A{
    A s;        // 错误！抽象类A不能实例化对象作为成员
    int valb;
public:
    void set(){cin>>valb;}
};
`
**错误：** A 声明了纯虚函数 `set()=0`，是抽象类，不能实例化。B 中的成员 `A s;` 试图直接创建 A 的对象，这是一个编译错误。抽象类只能作为指针或引用的类型。

**改正：** 将 `A s;` 改为 `A* s;` 或 `A& s;`（均可以指向实际的派生类对象），或者去掉 A 的纯虚函数特性。

---


`class A{
    int x;
public:
    A(int s = 0){ x = s; }
    static void m(){cout<<x<<endl;}  // 错误1
};
class B :public A {
    int y;
public:
    B(int t = 0):A(t),y(t){}
    void n(){cout<<x<<y<<endl;}      // 错误2
};
`
**错误 1：** `static void m()` 是静态成员函数，没有 `this` 指针，不能访问非静态数据成员 `x`。静态函数中只能访问静态成员。

**错误 2：** `B::n()` 试图直接访问 `x`，但 `x` 在类 A 中默认访问权限为 **private**，派生类不能直接访问基类的 private 成员。

**改正：**

`class A {
    int x;
public:
    A(int s = 0) { x = s; }
    static void m() { /* 不能访问 x */ }    // 去掉对x的访问
protected:
    int getX() const { return x; }           // 提供 protected 访问接口
};

// B::n() 改为：
void n() { cout << getX() << y << endl; }
// 或将 class A 中的 x 改为 protected
`

---


`#include <iostream>
#include <vector>
using namespace std;

class Set {
    static int nextId;       // 全局编号生成器
    vector<int> data;        // 存储元素

public:
    const int id;            // 集合编号（只读）

    // 默认构造函数：空集合，自动分配编号
    Set() : id(++nextId) {}

    // 拷贝构造函数：复制全部元素但分配新的唯一 id
    Set(const Set& other) : id(++nextId), data(other.data) {}

    // 添加元素
    void add(int val) {
        data.push_back(val);
    }

    // 集合并：a = a + b（不去重）
    Set operator+(const Set& other) const {
        Set result;
        result.data = this->data;
        result.data.insert(result.data.end(),
                           other.data.begin(), other.data.end());
        return result;
    }

    // 移动赋值（支持 a = a + b 的链式调用）
    Set& operator=(Set&& other) {
        if (this != &other) {
            data = move(other.data);
        }
        return *this;
    }

    // 友元输出运算符
    friend ostream& operator<<(ostream& os, const Set& s) {
        os << "Set#" << s.id << " { ";
        for (int v : s.data)
            os << v << " ";
        os << "}";
        return os;
    }
};

int Set::nextId = 0;
`
**设计说明：**

- `id` 为 `const` 成员，通过静态计数器 `nextId` 自动递增分配，确保与建立顺序相关且不重复
- 拷贝构造调用 `++nextId` 产生新 id，满足 “a 和 b 的 id 不重复”
- `operator+` 返回新 Set 对象，合并两集合全部元素
- 移动赋值支持 `a = a + b` 的写法（+ 返回临时对象，触发移动语义）
- `operator<<` 输出格式为 `Set#id { 元素列表 }`

---


本题使用**组合模式（Composite Pattern）**——将公司（可含子节点）和部门（叶子节点）统一为组织单元，递归遍历。

`#include <iostream>
#include <vector>
#include <string>
using namespace std;

// 抽象组件：统一的组织单元接口
class OrgUnit {
protected:
    string name;
public:
    OrgUnit(const string& n) : name(n) {}
    virtual ~OrgUnit() = default;
    virtual void print(int depth = 0) const = 0;  // 递归打印，depth 控制缩进
    virtual void add(OrgUnit*) {}                  // 叶子节点默认空实现
    string getName() const { return name; }
};

// 叶子节点：职能部门（不再下设子部门）
class Department : public OrgUnit {
public:
    Department(const string& n) : OrgUnit(n) {}
    void print(int depth = 0) const override {
        cout << string(depth * 4, ' ') << "[部门] " << name << endl;
    }
};

// 复合节点：公司/分公司（可下设子公司或部门）
class Company : public OrgUnit {
    vector<OrgUnit*> children;
public:
    Company(const string& n) : OrgUnit(n) {}

    void add(OrgUnit* unit) override {
        children.push_back(unit);
    }

    void print(int depth = 0) const override {
        cout << string(depth * 4, ' ') << "[公司] " << name << endl;
        for (auto* child : children)
            child->print(depth + 1);
    }

    ~Company() {
        for (auto* c : children) delete c;
    }
};
`
**使用示例（仅在答题纸上呈现，试题不要求 `main`）：**

`Company* hq = new Company("总公司");
hq->add(new Department("财务部"));
hq->add(new Department("人力资源部"));

Company* branch = new Company("华东分公司");
branch->add(new Department("销售部"));
hq->add(branch);

hq->print();   // 递归输出全部组织架构
/* 输出：
[公司] 总公司
    [部门] 财务部
    [部门] 人力资源部
    [公司] 华东分公司
        [部门] 销售部
*/
`
**设计思想：**

需求实现方式**可复用**`OrgUnit` 抽象接口统一处理公司和部门，遍历代码一份即可**可扩展**新增组织类型（如"办事处"“项目组”）只需新增派生类**可维护**Composite 模式将树形结构操作集中在 `Company` 中，职责清晰**遍历支持**通过虚函数 `print()` + 递归实现深度优先遍历
---


`A1
A2
B
A3
A4
B
A3
A2
A1
A0
`
**详细分析过程：**

步骤操作count 变化输出①`new B` → 基类 A 构造0→1`A1`②B 的成员 `A a` 默认构造1→2`A2`③B() 构造函数体-`B`④`new A[2]` — 第 1 个元素2→3`A3`⑤`new A[2]` — 第 2 个元素3→4`A4`⑥`delete pa` → 虚析构，先调 ~B()-`B`⑦~B() 中 `delete[] p` 析构 A[0]4→3`A3`⑧~B() 中 `delete[] p` 析构 A[1]3→2`A2`⑨成员 `a` 析构（B 的成员，逆序）2→1`A1`⑩基类 A 部分析构1→0`A0`
**关键规律：**

- 构造顺序：**基类 → 成员 → 自身构造函数体**
- 析构顺序：**自身析构函数体 → 成员 → 基类**（与构造严格相反）
- 虚析构函数：保证 `delete` 基类指针时能正确路由到派生类析构函数

---


**共同 main 函数（表四）：**

`B s;
A& t = s;
s.g();   // 通过 B 对象调用
t.g();   // 通过 A& 引用调用（实际指向 B 对象）
`
**三表输出完全相同：**

`B::f
B::f
`
**分表辨析：**


调用机制输出`s.g()`B 无 `g()`，继承 A::g()。g() 非虚，调 A::g()。g() 内调虚函数 `f()` → 动态绑定到 B::f()`B::f``t.g()`t 静态类型 A&，g() 非虚 → 调 A::g()。g() 内调虚函数 `f()` → 动态类型 B → B::f()`B::f`

调用机制输出`s.g()`B 定义了 g()，隐藏 A::g()。s 静态类型 B → 调 B::g()。其内 f() 虚 → 动态绑定 B::f()`B::f``t.g()`t 静态类型 A&，g() 非虚 → 调 A::g()。其内 f() 虚 → 动态类型 B → B::f()`B::f`

调用机制输出`s.g()`g() 虚，B 重写。s 静态类型 B → B::g()。其内 f() **非虚**，B::f() 隐藏 A::f() → 静态调 B::f()`B::f``t.g()`t 静态类型 A&，g() 虚 → 动态类型 B → B::g()。其内 f() 非虚 → 静态调 B::f()`B::f`
**核心结论：** 三表殊途同归。无论 `g()` 和 `f()` 各自是否为虚函数，无论调用路径是静态绑定还是动态分发，最终都执行了 `B::f()`。这体现了 C++ 名字查找、静态绑定与动态绑定组合时的精妙语义——表三在 B::g() 中 f() 通过名字隐藏而非虚函数机制找到了 B::f()，体现了两种多态实现方式的"交集"。

---

*（卷终）*