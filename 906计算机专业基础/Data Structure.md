#### 数据结构 90 分

（1）掌握相关的基本概念，如数据结构、逻辑结构、存储结构、数据类型、抽象数据类型等；
（2）掌握算法设计的原则，掌握计算语句频度和估算算法时间复杂度和空间复杂度的方法；
（3）了解使用类C语言描述算法的方法。

## 线性表

（1）掌握线性表的逻辑结构和存储结构；
（2）掌握线性表在顺序结构和链式结构上实现基本操作的方法
（3）理解线性表两种存储结构的不同特点及其适用场合，会针对需求选用合适的存储结构解决实际问题
（4）了解一元多项式的表示方法和基本运算的实现方法。

### 定义

线性表是具有相同数据类型的n个数据元素的有限序列，n=0时，该线性表位空表。

线性表特点如下：

表中元素个数**有限**；

表中元素具有逻辑上的**顺序**性，在序列中各元素排序有其先后次序；

表中元素都是数据元素，每个元素都是单个元素；

表中元素的数据类型都**相同**，占有相同大小的存储空间；

表中元素具有**抽象性**，仅讨论元素间的逻辑关系，而不考虑元素究竟表示什么内容。

### 线性表的基本操作

InitList(&L)：初始化空表。

Length(L)：求表长。

LocateElem(L,e)：按值查找。

GetElem(L,i)：按位查找。

ListInsert(&L,i,e):在表的第i个位置插入元素e。

ListDelete(&L,i,&e):删除表的第i个位置的元素，并返回其值。

PrintList(L):输出表L。

Empty(L):判空。

DestroyList(&L)：销毁表。

### 顺序表

线性表的顺序存储称作顺序表

#### 顺序表的特点：

表中元素的逻辑顺序与其物理顺序相同；

随机访问（最主要的特点），即通过首地址和元素序号可在时间O(1)内找到指定的元素；

存储密度高，每个结点只存储数据元素；

##### 静态分配

```cpp
#define MaxSize 50
typedef struct{
    ElemType data[MaxSize];
    int length;
}SqList;
```

##### 动态分配

```cpp
#define InitSize 100
typedef struct{
    ElemType *data;
    int MaxSize,length;
}
```

C的初始动态分配

```c
L.data=(ElemType*)malloc(sizeof(ElemType)*InitSize);
```

C++的初始动态分配

```cpp
L.data=new ElemType[InitSize];
```

##### 顺序表的基本操作实现

###### 插入操作

```c
bool ListInsert(SqList &L,int i,ElemType e){
    if(i<1 || i>MaxSize+1 || L.length>=MaxSize) return false;
    for(int j=L.length;j>=i;j--)
        L.data[j]=L.data[[j-1];
    L.data[i-1]=e;
    L.length++;
    return true;
}
```

###### 删除操作

```cpp
bool ListDelete(SqList &L,int i,ElemType &e){
    if(i<1 || i>L.length) return false;
    e = L.data[i-1];
    for(j=i-1;j<length-1;j++)
        L.data[j]=L.data[j+1];
    L.length--;
    return true;
}
```

###### 按位查找

```cpp
int ListFind(SqList L, ElemType e) {
    for (int i = 0; i < L.length; i++) {
        if (L.data[i] == e) {
            return i + 1;
        }
    }
    return 0;
}
```

###### 按值查找

```cpp
int ListFind(SqList L, ElemType e) {
    for (int i = 0; i < L.length; i++) {
        if (L.data[i] == e) {
            return i + 1;
        }
    }
    return 0;
}
```

### 链表

#### 单链表

##### 单链表结点

```c
typedef struct LNode{
    ElemType data;
    struct Lnode *next;
}LNode, *LinkList;
```

利用单链表可以解决顺序表需要大量连续存储空间的缺点，但单链表附加指针域，也存在浪费存储空间的缺点。

单链表是非随机存取的存储结构，即不能直接找到表中某个特定的结点。

引入头节点的优点：

1.由于开始结点的位置被存放在头节点的指针域中，所以在链表的第一个位置上的操作和在表的其他位置上的操作一致，无须进行特殊处理。

2.无论链表是否为空，其头指针都指向头结点的非空指针，因此空表和非空表的处理得到同意。

##### 单链表的基本操作

建立单链表：

```c
//头插法建立单链表（带头结点）
void CreateList(LinkList &L) {
    ElemType e;
    LNode *p;
    InitList(L);
    cout << "请输入数据：" << endl;
    cin >> e;
    L->next = new LNode;
    L->next->data = e;
    p = L->next;
    while (cin >> e) {
        p->next = new LNode;
        p->next->data = e;
        p = p->next;
    }
    p->next = NULL;
}
//尾插法建立单链表（带头结点）
void CreateList2(LinkList &L) {
    ElemType e;
    LNode *p,*q;
    InitList(L);
    cout << "请输入数据：" << endl;
    cin >> e;
    L->next = new LNode;
    L->next->data = e;
    p = L->next;
    while (cin >> e) {
        q = new LNode;
        q->data = e;
        p->next = q;
        p = q;
    }
    p->next = NULL;
}
```

按序查找结点值：

```c
// 按序查找结点值
LNode *GetElem(LinkList L,int i) {
    if(i<0) return NULL;
    LNode *p = L->next; 
    int j = 1; //当前p指向的是第几个结点
    if(i == 0) return L;
    while (p != NULL && j < i) {//循环找到第i个结点
        p = p->next;
        j++;
    }
    return p;
}
```

按值查找表结点

```c
// 按值查找
LNode *LocateElem(LinkList L,ElemType e) {
    LNode *p = L->next;
    while (p != NULL && p->data != e) {
        p = p->next;
    }
    return p;
}
```

插入结点

```c
// 插入结点
bool ListInsert(LinkList &L,int i,ElemType e) {
    if(i<1) return false;
    LNode *p = L; //让p指向第0个结点
    int j = 1;
    while (p != NULL && j < i) {
        p = p->next;
        j++;
    }
    //LNode *p = GetElem(L,i-1); 让p指向第i-1个结点
    if(p == NULL) {
        return false;
    }
    LNode *q = new LNode;
    q->data = e;
    q->next = p->next;
    p->next = q;
    return true;
}
```

删除结点

```c
// 删除结点
bool ListDelete(LinkList &L,int i,ElemType &e) {
    if(i<1) return false;
    LNode *p = L;
    int j = 0;
    while (p != NULL && j < i-1) { //循环找到第i-1个结点
        p = p->next;
        j++;
    }
    if(p == NULL) {
        return false;
    }
    if(p->next == NULL) {
        return false;
    }
    LNode *q = p->next;
    p->next = q->next;
    e = q->data;
    delete q;
    return true;
}
```

#### 双链表

```c
typedef struct DNode{
    ElemType data;
    struct DNode *prior,*next;
}DNode,*DLinkList;
//初始化双链表（带头结点）
void InitList(DLinkList &L) {
    L = new DNode;
    L->prior = NULL;
    L->next = NULL;
}
//判断双链表是否为空
bool ListEmpty(DLinkList L) {
    return L->next == NULL;
}
//在p结点之后插入s结点
bool ListInsert(DNode *p,DNode *s) {
    if(p==NULL || s==NULL) {
        printf("error: p or s is NULL\n");
        return false;
    }
    s->next = p->next;
    if(p->next != NULL) {//如果p结点不是最后一个结点
        p->next->prior = s;
    }
    s->prior = p;
    p->next = s;
    return true;
}
// 双链表的删除操作
bool ListDelete(DNode *p) {
    if(p==NULL || p->next==NULL) {
        printf("error: p is NULL or p->next is NULL\n");
        return false;
    }
    DNode *q = p->next;
    p->next = q->next;
    if(q->next != NULL) {  //q不是最后一个结点
        q->next->prior = p;
    }
    delete q;
    return true;
}
// 双链表的遍历
void ListTraverse(DLinkList L) {
    DNode *p = L->next;
    while(p != NULL) {
        // 处理
        p = p->next;
    }
}
```

#### 循环链表

#### 静态链表

分配一整片连续内存空间，把结点集中安置，用数组的方式实现的链表

优点：增、删操作不需要移动大量元素

缺点：不能随机存取，只能从头结点开始依次往后查询

适用于 ①不支持指针的低级语言（如Basic）② 数据元素数量固定不变（如操作系统的FAT）

### 一元多项式的表示方法和基本运算

> 2018年算法填空：求两个一元多项式的和

## 栈和队列(StackAndQueue)

（1）了解栈和队列的特点；
（2）掌握在两种存储结构上栈的基本操作的实现；
（3）掌握栈的各种应用，理解递归算法执行过程中栈状态的变化过程；
（4）掌握循环队列和链队列的基本运算；
（5）会应用队列结构解决实际问题。

### 栈

栈(Stack) ：只允许在一端进行插入或删除操作的线性表。

操作特性：后进先出（Last In First Out)

#### 栈的顺序存储结构

```c
#define MaxSize 50           //定义栈中元素的最大个数
typedef struct{
    Elemtype data[MaxSiz];//存放栈中元素
    int top;              //栈顶指针         
} SqStack;
```

#### 顺序栈的基本操作

```c
// 初始化栈顶指针
void InitStack(SqStack &S){
    S.top=-1; 
}
//判栈空
bool StackEmpty(SqStack S){
    return S.top=-1;
}
//入栈
bool Pop(SqStack &S,ElemType x){
    if(S.top==MaxSize-1)//栈满，报错
        return false;
    S.data[++S.top]=x;  //指针加1，入栈
    return true;
}
//出栈
bool Push(SqStack &S,ElemType &x){
    if(S.top=-1) //栈空，报错
        return false;
    x = S.data[S.top--]; //出栈，指针减1
    return true;
}
//读取栈顶元素
bool GetTop(SqStack S,ElemType &x){
    if(S.top=-1)//栈空，报错
        return falsel;
    x = S.data[S.top];
    return true;
}
//如果初始化为S.top=0，那么入栈操作变为S.data[S.top++]=x;出栈操作变为x=S.data[--S.top]。
```

#### 栈的链式存储结构

优点：便于多个栈共享存储空间和提高效率，且不存在栈满上溢的情况。规定所有操作都是在单链表的表头进行的

```c
typedef int ElemType;
typedef struct Linknode{
    ElemType data;
    struct Linknode *next;
} *LiStack;

// 初始化链栈
LiStack InitStack() {
    Linknode* top = new Linknode;
    top->next = NULL;
    return top;
}
// 判空
bool StackEmpty(LiStack top) {
    return top->next == NULL;
}
// 入栈
bool Push(LiStack &top,ElemType x) {
    Linknode* p = new Linknode;
    if(p == NULL)
        return false;
    else{
        p->data = x;
        p->next = top->next;
        top->next = p;
        return true;
    }
}
// 出栈
bool Pop(LiStack &top,ElemType x) {
    if(StackEmpty(top))
        return false;
    else{
        Linknode* p = top->next;
        x = p->data;
        top->next = p->next;
        return true;
    }
}
```

##### 卡特兰数

##### 共享栈

### 队列

只允许在表尾入队，在表头出队，先进先出（First In First Out,FIFO）

#### 队列的顺序存储结构

```c
#define MaxSize 50 //队列中元素的最大个数
typedef struct{
    ElemType data[MaxSize];
    int front,rear;
}SqQueue;
```

#### 队列的基本操作

初始：Q.front=Q.rear=0

队首指针进1：Q.front=(Q.front+1)%MaxSize

队尾指针进1：Q.rear=(Q.rear+1)%MaxSize

队列长度：(Q.rear-Q.front+MaxSize)%MaxSize

```c
//初始化
void InitQueue(SqQueue &Q){
    Q.rear=Q.front=0;    //队头队尾指针都指向0
}
//判队空
bool isEmpty(SqQueue Q){
    return Q.rear==Q.front;
}
//入队
bool EnQueue(SqQueue &Q,ElemType x){
    if((Q.rear+1)%MaxSize==Q.front)    //队满，报错
        return false;
    Q.data[Q.rear] = x;
    Q.rear=(Q.rear+1)%MaxSize;
    return true;
}
//出队
bool DeQueue(SqQueue &Q,ElemType &x){
    if(Q.rear==Q.front)                 //队空，报错
        return false;
    x = Q.data[Q.front];
    Q.front=(Q.front+1)%MaxSize;
    return true;
}
// 牺牲一个存储空间
// 队空条件：Q.front == Q.rear
// 队满条件：(Q.rear+1)%Maxsize == Q.front
// 队列元素个数：(Q.rear-Q.front+Q.Maxsize)%Maxsize
```

以上是牺牲一个单元来区分队空与队满

队满：(Q.rear+1)%MaxSize==Q.front

队空：Q.rear==Q.front

元素个数：(Q.rear-Q.front+MaxSize)%MaxSize

##### 还有两种方法来区分

1.类型中增设元素个数 int size ，每次入队size++ ，出队size--

队空：Q.size==0

队满：Q.size==MaxSize

2.类型中增设tag，只有出队会导致队空，只有入队会导致队满

则每次出队时将tag设为0，入队时将tag设为1

队空：tag == 0

队满：tag == 1

#### 队列的链式存储结构

```c
typedef struct{
    ElemType data;
    struct LinkNode *next;
}LinkNode;
typedef struct{
    LinkNode *front,*rear;
}LinkQueue;
```

#### 链式队列的基本操作

优点：适用于数据元素变动比较大的情形，不存在队列满且产生溢出的问题

```c
////带头结点的
//初始化
void InitQueue(LinkQueue &Q){
    Q.front = Q.rear = new LinkNode*;
    //Q.front=Q.rear=(LinkNode*)malloc(sizeof(LinkNode));
    Q.front->next=NULL; // 2021年算法填空：初始化条件
}
//判队空
bool IsEmpty(LinkQueue Q){
    return Q.front==Q.rear;
}
//入队
void EnQueue(LinkQueue &Q,ElemType x){
    //链式存储一般不需要判满，除非内存不足
    LinkNode *s = new LinkNode;
    s->data = x;
    s->next = NULL;
    Q.rear->next=s;
    Q.rear=s;
}
//出队
bool DeQueue(LinkQueue &Q,ElemType &x){
    if(Q.front==Q.rear) //队空，报错
        return false;
    LinkNode *p = Q.front->next;
    x=p->data;
    Q.front->next=p->next;
    if(Q.rear==p)
        Q.rear=Q.front;
    delete p;
    return true;
}
// 2021年算法填空：出队入队操作
////不带头结点
//初始化
void InitQueue(LinkQueue &Q){
    Q.front = NULL;
    Q.rear = NULL;
}
//判队空
bool IsEmpty(LinkQueue Q){
    return Q.front = NULL;
}
//入队
void EnQueue(LinkQueue &Q,ElemType x){
    LinkNode *s=(LinkNode *)malloc(sizeof(LinkNode));
    s->data=x;
    s->next=NULL;
    if(Q.front=NULL){
        Q.front = s;
        Q.rear = s;
    }else{
        Q.rear->next = s;
        Q.rear = s;
    }
}
//出队
bool DeQueue(LinkQueue &Q,ElemType &x){
    if(Q.front==NULL)   //队空，报错
        return false;
    LinkNode *p = Q.front;
    x=p->data;
    Q.front=p->next;
    if(Q.rear==p){
        Q.front = NULL;
        Q.rear = NULL;
    }
    free(p);
    return true;
}
```

#### 双端队列

允许两端都可以进行入队和出队操作

分类：

输出受限的双端队列∶允许在一端进行插入和删除，但在另一端只允许插入的双端队列

输入受限的双端队列∶允许在一端进行插入和删除，但在另一端只允许删除的双端队列

### 栈和队列的应用

#### 栈在括号匹配中的应用

给定一个只包括 `(`，`)`，`{`，`}`，`[`，`]` 的字符串，判断字符串是否有效。
有效字符串需满足：
1、左括号必须用相同类型的右括号闭合。
2、左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

算法：

1.初始化空栈，顺序将字符串压入栈中

2.若是左括号，直接压栈

3.若是右括号，直接与栈顶元素配对；若匹配，栈顶元素弹出栈，若栈空，false

4.若栈空，true

```c++
bool bracketCheck(char str[],int length){
    SqStack S;
    InitStack S;
    for(int i=0;i<length;i++){
        if(str[i]=='('||str[i]=='['||str[i]=='{')
            Push(S,str[i]);
        else{
            if(StackEmpty(S))
                return false;
            char topElem;
            Pop(S,topElem);
            if(str[i]=='('&&topElem!=')')
                return false;
            if(str[i]=='['&&topElem!=']')
                return false;
            if(str[i]=='{'&&topElem!='}')
                return false;
        }
    }
    return StackEmpty(S);
}
```

考试时用顺序栈即可，开发时为防止栈满使用链栈。

#### 栈在表达式求值中的应用

##### 中缀表达式转后缀表达式:

初始化一个栈，用于保存暂时还不能确定运算顺序的运算符。从左到右处理各个元素，直到末尾。可能遇到三种情况:
①遇到操作数。直接加入后缀表达式。
②遇到界限符。遇到“(”直接入栈;遇到“)”则依次弹出栈内运算符并加入后缀表达式，直到弹出“(”为止。注意:“(”不加入后缀表达式。
③遇到运算符。依次弹出栈中优先级高于或等于当前运算符的所有运算符，并加入后缀表达式若碰到“(”或栈空则停止。之后再把当前运算符入栈。
按上述方法处理完所有字符后，将栈中剩余运算符依次弹出，并加入后缀表达式。

##### 后缀表达式的计算:

①从左往右扫描下一个元素，直到处理完所有元素②若扫描到操作数则压入栈，并回到①;否则执行③
③若扫描到运算符，则弹出两个栈顶元素，执行相应运算，运算结果压回栈顶，回到①

##### 中缀表达式的计算:（上述两个算法的合并）

初始化两个栈，操作数栈和运算符栈若扫描到操作数，压入操作数栈
若扫描到运算符或界限符，则按照“中缀转后缀”相同的逻辑压入运算符栈（期间也会弹出运算符每当弹出一个运算符时，就需要再弹出两个操作数栈的栈顶元素并执行相应运算，运算结果再压回操作数栈)

###### 前缀表达式同理

## 串

（1）掌握串的基本运算的定义，了解利用基本运算来实现串的其它运算的方法；
（2）了解在顺序存储结构和在堆存储结构以及块链存储结构上实现串的各种操作的方法；
（3）理解KMP算法，掌握NEXT函数和改进NEXT函数的定义和计算。

#### 串的基本运算

简单模式匹配算法

```c
int Index(SString S,SString T, int pos){
    int i = pos, j = 1;
    while (i<=S.length && j<=T.length){
        if(S.ch[i] == T.ch[j]){
            ++i;++j;
        }
        else{
            i = i-j+2;j = 1; 
        }
    }
    if(j>T.length) return i-T.length;
    else return 0;
}
```

#### 串的操作

#### KMP算法

```c
#define MAXLEN 255
// 静态数组实现串的顺序存储
typedef struct{
    char ch[MAXLEN];
    int length;
}SString;
// 动态数组实现
typedef struct{
    char *ch;
    int length;
}HString;

// 求子串
bool SubString(SString &Sub, SString S, int pos, int len){
    if(pos<1 || len<1 || pos+len-1>S.length)
        return false;
    for(int i=0; i<pos+len; i++)
        Sub.ch[i-pos+1] = S.ch[i];
    Sub.length = len;
    return true;
}
// 比较操作
int StrCompare(SString S, SString T){
    for(int i=1; i<=S.length && i<=T.length; i++)
        if(S.ch[i] != T.ch[i])
            return S.ch[i]-T.ch[i];
    return S.length-T.length;
}
// 定位操作(朴素模式匹配算法)
int Index(SString S, SString T) {
    int i = 1;
    SString sub;
    while(i<=S.length-T.length+1){
        SubString(sub,S,i,T.length);
        if(StrCompare(sub,T)==0)
            return i;
        i++;
    }
    return 0;
}
// 朴素模式匹配算法
int Index1(SString S, SString T) {
    int i=1,j=1;
    while(i<=S.length && j<=T.length){
        if(S.ch[i]==T.ch[i]){
            ++i; ++j;
        }
        else{
            i = i-j+2;
            j = 1;
        }
    }
    if(j>T.length)
        return i-T.length;
    else
        return 0;
}
// KMP算法
// getnext
void GetNext(SString T, int next[]){
    int i=1,j=0;
    next[1] = 0;
    while(i<T.length){
        if(j==0||T.ch[i]==T.ch[j]){
            next[++i] = ++j;
        }
        else {
            j = next[j];
        }
    }
}
// 利用next数组求得nextval
void GetNextval(SString T, int nextval[]) {
    nextval[1] = 0;
    int next[T.length+1];
    GetNext(T,next);
    for(int j = 2; j<=T.length;j++){
        if(T.ch[next[j]] == T.ch[j])
            nextval[j] = nextval[next[j]];
        else
            nextval[j] = next[j];
    }
}
// 纯粹的nextval函数
void get_nextval(SString T, int nextval[]){
    int i = 1, j = 0;
    nextval[1] = 0;
    while(i<T.length){
        if(j == 0||T.ch[i]==T.ch[j]){
            ++i;++j;
            if(T.ch[i]!=T.ch[j])
                nextval[i] = j;
            else
                nextval[i] = nextval[j];
        }
        else{
            j = nextval[j];
        }
    }
}
int Index_KMP(SString S, SString T) {
    int i=1,j=1;
    int *next = new int[T.length+1];
    get_nextval(T,next);
    while(i<=S.length && j<=T.length){
        if(j==0 || S.ch[i]==T.ch[j]){
            ++i; ++j;
        }
        else{
            j = next[j];
        }
    }
    if(j>T.length)
        return i-T.length;
    else
        return 0;
}
```

#### 数组

（1）掌握数组在以行为主和以列为主的存储结构中的地址计算方法；

#### 特殊矩阵的压缩存储

（2）掌握矩阵压缩存储时的下标变换方法，了解以三元组表示稀疏矩阵的方法；

#### 广义表

（3）理解广义表的定义及其存储结构，理解广义表的头尾和子表两种分析方法。

## 树与二叉树

（1）熟练掌握二叉树的结构特点和性质，掌握二叉树各种存储结构及构建方法；
（2）掌握按先序、中序、后序和层次次序遍历二叉树的算法，理解二叉树的线索化实质和方法；
（3）利用二叉树的遍历求解实际问题；
（3）掌握树的各种存储结构及其特点，掌握树的各种运算的实现算法；
（4）掌握建立最优二叉树和哈夫曼编码的方法。

### 树

##### 基本性质

1）树中的结点数等于所有结点的度数加1

2）度为m的树中第i层上至多有$m^{i-1}$个结点$(i>=1)$ 

3）高度为h的m叉树至多有$\frac{m^h-1}{m-1}$个结点

4）具有n个结点的m叉树的最小高度为$[log_m(n(m-1)+1)]$

##### 树的存储结构

双亲表示法

```c
#define MAX_TREE_SIZE 100
typedef struct{
    ElemType data;
    int parnet;
}PTNode;
typedef struct{
    PTNode nodes[MAX_TREE_SIZE];
    int n;
}PTree
```

孩子表示法

```c
typedef struct{
    ElemType data;
    CTNode firstchild;
}CTBox;
typedef struct CTNode{
    int child;
    struct CTNode *next;
}*CTNode;
typdef struct{
    CTBox nodes[MAX_TREE_SIZE];
    int r,n;
}CTree
```

孩子兄弟表示法

```c
typedef struct CSNode{
    TElemtype data;
    struct CSNode *firstchild, *rightsib;
} CSNode, *CSTree;
```

### 二叉树

#### 顺序存储结构

直接用数组存储

#### 链式存储结构

```c
typedef struct BiTNode{
    ElemType data;
    struct BitNode *lchild,*rchild;
}BiNode,*BiTree;
```

### 遍历二叉树

##### 先序遍历

```c
void PreOrder(BiTree T){
    if(T!=NULL){
        visit(T);
        PreOrder(T->lchild);
        PreOrder(T->rchild);
    }
}
```

##### 先序遍历的非递归算法

```c
void PreOrder2(BiTree T){
    InitStack(S);    //初始化栈S
    BiTree p = T;    //p是遍历指针
    while(p || !IsEmpty(S)){    //栈不空或p不空时循环
        if(p){
            visit(p);    //访问出栈结点
            Push(S, p);    //当前节点入栈
            p = p->lchild;    //左孩子不空，一直向左走
        }else{
            Pop(S, p);    //栈顶元素出栈
            p = p->rchild;    //向右子树走，p赋值为当前结点的右孩子
        }
    }
}
```

##### 中序遍历

```c
void InOrder(BiTree T){
    if(T!=NULL){
        InOrder(T->lchild);
        visit(T);
        InOrder(T->rchild);
    }
}
```

##### 中序遍历的非递归算法

```c
void InOrder2(BiTree T){
    InitStack(S);    //初始化栈S
    BiTree p = T;    //p是遍历指针
    while(p || !IsEmpty(S)){    //栈不空或p不空时循环
        if(p){
            Push(S, p);    //当前节点入栈
            p = p->lchild;    //左孩子不空，一直向左走
        }else{
            Pop(S, p);    //栈顶元素出栈
            visit(p);    //访问出栈结点
            p = p->rchild;    //向右子树走，p赋值为当前结点的右孩子
        }
    }
}
```

##### 后序遍历

```c
void PostOrder(BiTree T){
    if(T!=NULL){
        PostOrder(T->lchild);
        PostOrder(T->rchild);
        visit(T);
    }
}
```

##### 后序遍历的非递归算法

```c
void PostOrder2(BiTree T){
    InitStack(S);
    p = T;
    r = NULL;
    while(p || !IsEmpty(S)){
        if(p){    //走到最左边
            push(S, p);
            p = p->lchild;
        }else{    //向右
            GetTop(S, p);    //读栈顶元素（非出栈）
            //若右子树存在，且未被访问过
            if(p->rchild && p->rchild != r){
                p = p->rchild;    //转向右
                push(S, p);    //压入栈
                p = p->lchild;    //再走到最左
            }else{    //否则，弹出结点并访问
                pop(S, p);    //将结点弹出
                visit(p->data);    //访问该结点
                r = p;    //记录最近访问过的结点
                p = NULL;
            }
        }
    }
}
```

##### 层次遍历

```c
void LevelOrder(BiTree T){
    InitQueue(Q);                     //初始化辅助队列
    BiTree p;
    EnQueue(Q, T);                    //将根节点入队
    while(!IsEmpty(Q)){               //队列不空则循环
        DeQueue(Q, p);                //队头结点出队
        visit(p);                     //访问出队结点
        if(p->lchild != NULL){
            EnQueue(Q, p->lchild);    //左子树不空，则左子树根节点入队
        }
        if(p->rchild != NULL){
            EnQueue(Q, p->rchild);    //右子树不空，则右子树根节点入队
        }
    }
}
```

任意序列+中序序列都可以唯一确定一个二叉树

### 线索二叉树

```c
typedef struct ThreadNode{
    ElemType data;    //数据元素
    struct ThreadNode *lchild, *rchild;    //左、右孩子指针
    int ltag, rtag;    //左、右线索标志
}ThreadNode, *ThreadTree;
```

通过中序遍历对二叉树线索化的递归算法如下:

```c
void InThread(ThreadTree p, ThreadTree pre){
    if(p != NULL){
        InThread(p->lchild, pre);    //递归，线索化左子树
        if(p->lchild == NULL){    //左子树为空，建立前驱线索
            p->lchild = pre;
            p->ltag = 1;
        }
        if(pre != NULL && pre->rchild == NULL){
            pre->rchild = p;    //建立前驱结点的后继线索
            pre->rtag = 1;
        }
        pre = p;    //标记当前结点成为刚刚访问过的结点
        InThread(p->rchild, pre);    //递归，线索化右子树
    }
}
```

通过中序遍历建立中序线索二叉树的主过程算法如下:

```c
void CreateInThread(ThreadTree T){
    ThreadTree pre = NULL;
    if(T != NULL){
        InThread(T, pre);    //线索化二叉树
        pre->rchild = NULL;    //处理遍历的最后一个结点
        pre->rtag = 1;
    }
}
```

在线索二叉树中找前驱后继

```c
//找到以P为根的子树中，第一个被中序遍历的结点
ThreadNode *Firstnode( ThreadNode *p){
    //循环找到最左下结点(不一定是叶结点)
    while(p->ltag==0) 
    p=p->lchild;
    return p;
}
//在中序线索二叉树中找到结点p的后继结点
ThreadNode *Nextnode( ThreadNode *p){
    //右子树中最左下结点
    if(p->rtag==0) return Firstnode(p->rchild);
    else return p->rchild; //rtag==1直接返回后继线索
}

```

### 最优二叉树和哈夫曼编码

在含有n个带权叶结点的二叉树中，其中带权路径长度最小的二叉树为最优二叉树也叫哈夫曼树

### 算法总结

1、计算二叉树结点个数

```c
int NodeNum(BTNode * root)
{
    if(root== NULL) // 递归出口
        return 0;
    return NodeNum(root->lchild) + NodeNum(root->rchild) + 1;
}
```

2、计算二叉树中叶子结点个数（2020年代码阅读）

递归解法：  
（1）如果二叉树为空，返回0  
（2）如果二叉树不为空且左右子树为空，返回1  
（3）如果二叉树不为空，且左右子树不同时为空，返回左子树中叶子节点个数加上右子树中叶子节点个数

```c
int GetLeafNodeNum(BTNode * root)
{
    if(root== NULL)
        return 0;
    if(root->lchild== NULL && root->rchild== NULL)
        return 1;
    return GetLeafNodeNum(root->lchild) + GetLeafNodeNum(root->rchild);
}
```

3、计算二叉树中所有双分支的结点个数

```c
int Double(BTNode *b)
{
    if(b==NULL)
        return 0; //返回的树的高度为0
    if(b->lchild != NULL && b->rchild != NULL)
        return Double(b->lchild) + Double(b->rchild)+1;
    else
        return Double(b->lchild) + Double(b->rchild);
}
```

4、计算二叉树的深度（2015年算法填空）

```c
int GetDepth(BTNode * root)
{
    if(root== NULL) // 递归出口
        return 0;
    int depthLeft = GetDepth(root->lchild);
    int depthRight = GetDepth(root->rchild);
    return depthLeft > depthRight ? (depthLeft + 1) : (depthRight + 1); 
}

```

5、(a-(b+c))*(d/e) 存储在二叉树，遍历求值
6、找出二叉树中最大值点
7、判断两个二叉树是否相似
8、把二叉树所有节点左右子树交换
9、查找二叉树中data域等于key的结点是否存在，q指向它，否则q->nullptr
10、输出先序遍历第k个结点的值

```c
int i=0;
int PreNode(BTNode *T,int k){
	
	if(T == NULL){
		return 0;
	}
	i++;
	if(i==k){
		//visit(T);  
		return T->data;
	}
	int ch = PreNode(T->lchild,k);
	if(ch != 0)
		return ch;
	ch = PreNode(T->rchild,k);
		return ch;
}
```

11、求二叉树值为x的层号

```c
int  L = 1;
//L是全局变量，初值为1,用来记录当前所访问的结点层号
void leno(BTNode *p, char x){
	if(p == NULL)
		return;
	if (p->data==x){ //当第一次来到这个结点时，对其data域进行检查，看是否等于x,如果相等，则打印出其层号L
		printf("层号：%d",L);
	}
	++L;	//打印完层号之后，指针p将要进入下一层结点，因此L要自增1,代表下一层的层号
	leno(p->1child,x) ;
	leno(p->rchild,x);
	--L;	//p指针将要由下一层返回上一层，因此L要自减1,代表
}
```

12、树种元素为x的结点，删除以它为根的子树
13、利用结点的右孩子指针将一个二叉树的叶子结点从左向右连接成单链表
14、输出根节点到每个叶子结点的路径

```c
void allpath(BTNode *p, char pathstack[], int top)
{
    if (p != NULL)
    {
    pathstack[top] = p->data;
    if (!p->lchild && !p->rchild)
        for (int i = 0; i <= top; ++i)
        cout << pathstack[i] << " ";
    cout << endl;
    allpath(p->lchild, pathstack, top + 1);
    allpath(p->rchild, pathstack, top + 1);
    }
}
```

15、满二叉树先序序列存在于数组中，转化为后序序列
16、先序与中序遍历存在A、B两个一维数组中，建立二叉链表
17、二叉树以顺序方式存在于数组A，建立二叉链表
18、增加一个指向双亲结点的parent指针，输出所有结点到根节点的路径
19、先序非递归遍历二叉树
20、中序非递归遍历二叉树
21、后序非递归遍历二叉树
22、二叉树中 查找值为x的结点，打印出它的所有祖先
23、找到p和q最近公共祖先结点r
24、
25、给出自下而上从左到右的层次遍历
26、求解二叉树的宽度
27、用层次遍历求解二叉树高度
28、判断二叉树是否为完全二叉树
29、计算二叉树的带权路径长度（叶子）（2016年算法设计）
30、将给定的二叉树转化为等价的中缀表达式
31、建立中序线索二叉树
32、中序遍历线索二叉树（考过两次，课本源代码）

```c
typedef enum PointerTag{Link, Thread}; //Link == 0：指针，Thread ==1:线索
typedef struct BiThrNode{
    TElemType data;
    struct BiThrNode *lchild, *rchild;
    PointerTag LTag,RTag;
}BiThrNode, *BiThrTree;
Status InOrderTraverse_Thr(BiThrTree T, Status(*Visit)(TElemType e)) {
    //中序遍历二叉线索树的非递归算法，对每个数据元素调用函数Visit
    p = T->lchild;
    while(p != T){
        //当ltag==0时循环到中序序列第一个结点
        while(p->LTag == LInk) p = p->lchild;
        if(!Visit(p->data)) return ERROR;
        while(p->RTag == Thread && p->rchild!=T){
            p = p->rchild; Visit(p->data);
        }
        p = p->rchild;
    }
    return OK;
}// InOrderTraverse_Thr
```

33、先序建立二叉搜索树并先序遍历
34、寻找中序线索二叉树的前驱节点
35、孩子兄弟表示法求树所有叶子结点个数（2007年算法设计，要求递归）
36、孩子兄弟表示法求树的高度
37、已知一棵树的层次序列和每个结点的度，构造此树的孩子兄弟链表

## 图

（1）熟练掌握图的基本概念，会构建各种图的存储结构；
（2）掌握深度优先搜索遍历图和广度优先搜索遍历图的算法；
（3）灵活运用图的遍历算法求解各种路径问题，包括最小生成树﹑最短路径﹑拓扑排序﹑关键路径等。

### 图的存储结构

#### 邻接矩阵

```c
#define MaxVerTexNum 100                     //顶点数目最大值
#define INFINITY
typedef struct{
    char Vex[MaxVertexNum];                   //顶点表
    int Edge[MaxVertexNum][MaxVertexNum];    //邻接矩阵，边表
    int vexnum,arcnum;                        //图当前顶点数和边数
}MGraph;
```

空间复杂度：$O(|V|^2)$，只和顶点数有关，和实际边数无关。

适合用于存储稠密图。无向图可以压缩存储。

设图G的邻接矩阵为$A$（矩阵元素为0/1），$A^n$的元素$A^n[i][j]$为从顶点i到顶点j的长度为n的路径的数目

#### 邻接表

```c
#define MaxVertexNum 100  //顶点数目最大值
typedef char VertexType;  //顶点的数据类型
typedef struct ArcNode{   //边结点
    int adjvex;              //该弧所指向的结点的位置
    struct ArcNode *next; //指向下一条弧的指针
    //InfoType info;       //网的边权值
}ArcNode;
typedef struct Vnode{      //顶点结点
    VertexType data;       //顶点信息
    ArcNode *first;          //指向第一条依附该顶点的弧的指针
}Vnode,AdjList[MaxvertexNum]
typedef struct{
    AdjList vertices;      //邻接表
    int vexnum,arcnum;    //图的顶点数和边数
}ALGraph;
```

#### 十字链表

十字链表只用于存储有向图

```c
#define MaxVertexNum 100             //顶点数目最大值
typedef char VertexType;            //顶点的数据类型
typedef struct  ArcNode{            //边结点
    int tailvex,headvex;            //边尾顶点编号
    //InfoType info;                //网的边权值
    ArcNode *hlink,*tlink;            //边头相同、边尾相同的下一条边
}ArcNode;
typedef struct VNode{                //顶点结点
    VertexType data;
    ArcNode *firstin,*firstout;        //该顶点作为边头、边尾的第一条边
}VNode；
typedef struct{
    Vnode xlist[MaxVertexNum];
    int vexnum,arcnum;
}GLGraph
```

#### 邻接多重表

邻接多重表只用于存储无向图

```c
#define MaxVertexNum 100            //顶点数目最大值
typedef char VertexTypel;            //顶点的数据类型
typedef struct ArcNode{
     int i,j;
    ArcNode *iLink,*jLink;
    //InfoType info;
}ArcNode;
typedef struct Vnode{
    char data;
    ArcNode *firstedge;
}Vnode;
typedef struct{
    Vnode adj[MaxVertexNum];
    int vexnum,arcnum;
}AMLGraph;
```

#### 图的基本操作

`Adjacent(G,x,y)`，判断图是否存在边(x,y)或<x,y>。

`Neighbors`，列出图中与 x 邻接的边。

`InsertVertex(G,x)`，在图中插入顶点 x。

`DeleteVertex(G,x)`，在图中删除顶点 x。

`AddEdge(G,x,y)`，如果(x,y)或<x,y>不存在，则添加。

`RemoveEdge(G,x,y)`，如果(x,y)或<x,y>存在，则删除。

`FirstNeighbor(G,x)`，求图中顶点 x 的第一个邻接点。存在返回顶点号，不存在返回-1。

`NextNeighbor(G,x,y)`，返回除x的的下一个邻接点，不存在返回-1；

`GetEdgeValue(G,x,y)`，获得(x,y)或<x,y>的权值。

`SetEdgeValue(G,x,y)`，设置(x,y)或<x,y>的权值。

### 图的遍历

#### 广度优先遍历（BFS）

```c
bool visited[MAX_VERTEX_NUM];        //访问标记数组
void BFSTraverse(Graph G){            //对图G广度优先遍历
    for(int i=0;i<G.vexnum;++i){
        visited[i]=false;            //访问标记数组初始化
    }
    InitQueue Q;                    //作辅助队列
    for(int i=0;i<G.vexnum;++i){    //从0号顶点开始遍历
        if(!visited[i])                //对每个连通分量调用一次BFS
            BFS(G,i);        
    }
}
void BFS(Graph G,int v){            //从顶点v出发开始遍历图G
    visit(v);                        //访问v顶点
    visited(v)=true;                //对v作已访问标记
    EnQueue(Q,v);                    //顶点v入队
    while(!isEmpty(Q)){                
        DeQueue(Q,v);                //顶点v出队
        for(w=FirstNeighbor(G,v);w>=0;w=NextNeighbor(G,v.w)){
            if(!visited[w]){
                visit(w);
                visited[w]=true;
                EnQueue(Q,w);
            }
        }
    }          
}
```

##### 性能分析

邻接矩阵：时间复杂度为为$O(|V|^2)$，，空间复杂度为$O(|V|)$

邻接表：时间复杂度为$O(|V|+|E|)$，，空间复杂度为$O(|V|)$

#### 深度优先遍历（DFS）

```c
bool visited[MAX_VERTEX_NUM];        //访问标记数组
void DFSTraverse(Graph G){
    for(int i=0;i<G.vexnum;++i){
        visited[i]=false;
    }
    for(int i=0;i<G.vexnum;++i){
        if(!visited[i])
            DFS(G,i);
    }
}
void DFS(Graph G,int v){
    visit(v);
    visited[v]=true;
    for(w=FirstNeighbor(G,v);w>=0;w=NextNeighbor(G,v,w)){
        if(!visited[w]){
            DFS(G,w);
        }
    }
}
```

##### 性能分析

邻接矩阵：时间复杂度为$O(|V|^2)$，空间复杂度 为$O(|V|)$ 

邻接表：时间复杂度为$O(|V|+|E|)$，空间复杂度为$O(|V|)$ 

### 图的应用

#### 最小生成树：

2016年算法填空

##### Prim算法

从某一个顶点开始构建生成树；每次将代价最小的顶点纳入生成树，直到所有顶点都被纳入为止

时间复杂度：$O(|V|^2)$  ,适用于边稠密图

##### Kruskal算法

每次选择一条权值最小的边，使这条边的两头连通，直到所有结点都连通

时间复杂度：$O(|E|log_2|E|)$ ，适用于边稀疏图

#### 最短路径：

##### Dijkstra算法

##### Floyd算法

#### 拓扑排序：AOV网

（2006年算法填空）

#### 关键路径：AOE网

> 2018年算法设计：把图的邻接矩阵存储结构转变为邻接表存储结构，求出每个顶点的度并存入邻接表的顶点数组中



1、已知无向连通图G由顶点集V和边集E组成，|E|>0,当G中度为奇数的顶点个数为不大于2的偶数时，G存在包含所有边且长度为|E|的路径。
设图G为邻接矩阵存储，判断途中是否存在EL路径
2、图的BFS
3、BFS求无向图的最短路径
4、图的DFS
5、邻接表的图，判断i和j结点之间是否由路径
6、判断无向图是否是树
7、求无向连通图距顶点V最远的一个结点
8、DFS的非递归
9、输出无向图点u到点v的所有路径
10、求无向图的连通分量个数
11、邻接表转化为邻接矩阵
12、判断无向图是否存在环（并查集）
13、邻接矩阵转化为邻接表（2018年算法设计）

## 查找

（1）熟练掌握各种静态查找和动态查找算法，会计算查找成功时和失败时的平均查找长度；
（2）掌握二叉排序树的建立、插入和删除过程，掌握二叉平衡树的建立和旋转平衡方法；
（3）掌握B-树的建立、插入和删除结点的过程；
（4）熟练掌握哈希表的构造方法和处理冲突的方法。

### 顺序查找和折半查找

### B树和B+树

### 散列表

散列函数：一个把查找表中的关键字映射成该关键字对应的地址的函数

散列表：根据关键字而直接进行访问的数据结构

**一般哈希表都是用来快速判断一个元素是否出现集合里**

###### 处理冲突的方法

1、顺序表递增，最少时间内查找值为x的元素。若找到将其于后继元素位置交换，否则递增插入顺序表
2、找到单链表中值为key的元素，将其于前一个结点互换位置
3、顺序表中二分查找值为key的元素
4、判断二叉树是否使二叉搜索排序树
5、寻找二叉排序树中最大值和最小值
6、设求出指定结点在给定二叉排序树的层次
7、输出二叉搜索树中所有值大于key的结点
8、判断一个二叉树是否为平衡二叉树

## 排序

排序算法的稳定性：排序后使得关键字相同的元素保持原顺序中的相对位置不变

#### 插入排序

每次将一个待排序的记录按其关键字大小插入到前面已排好序的子序列中，直到全部记录插入完成

##### 直接插入

```c
void InsertSort(vector<int>& a){
    int i,j,temp;
    for(i = 1; i<=n-1;i++){
        temp = a[i];
        for(j = i-1;j>=0&&a[j]>temp;j--)
            a[j+1] = a[j];
        a[j+1] = temp;
    }
}
```

> 练习：在链式存储结构上设计直接插入排序
> 
> ```c
> void linksort(Linklist &head){
>     if(head->next == NULL) return;
>     LNode *sorted = head->next; // 已排序链表
>     LNode *curr = sorted->next; // 待插入元素curr
>     while(curr != NULL){
>         if(sorted->data <= curr->data){
>             sorted = sorted->next;    
>         }else{
>             LNode *prev = head;
>             while(prev->next->data <= curr->data){
>                 prev = prev->next;
>             }
>             sorted->next = curr->next;//插入
>             curr->next = prev->next;
>             prev->next = curr;
>         }
>         curr = sorted->next;
>     }
> }
> ```

##### 折半插入

```c
void InsertSort(vector<int>& a){
    int i,j,low,high,mid;
    for(i = 2;i<=n;i++){
        a[0]=a[i];
        low=1;high=i-1;
        while(low<=high){
            mid = (low+high)/2;
            if(a[mid]>a[0];) high = mid-1;
            else low = mid+1;
        }
        for(j=i-1;j>high;j--){
            a[j+1]=a[j];
        }
        a[high+1]=a[0];
    }
}
```

空间复杂度：$O(1)$  时间复杂度： $O(n^2)$  

> 2013年算法填空题

##### 希尔排序

```c
void ShellSort(vector<int>& a){
    int i,j,temp,d=a.size()/2;
    while(d>0){
        for(i=d;i<a.size();i++){
            temp=a[i];
            for(j=i-d;j>=0&&a[j]>temp;j-=d){
                a[j+d]=a[j];
            }
            a[j+d]=temp;
        }
    }
}
```

> 2015年算法填空题
> 
> 2021年算法填空题

#### 交换排序

##### 冒泡排序

```c
void bubbleSort(vector<int>& a){
    int i,j,temp;
    for(i = 0; i<a.size(); i++){
        for(j = 0; j<a.size()-i-1; j++){
            if(a[j]>a[j+1]){
                temp = a[j];
                a[j] = a[j+1];
                a[j+1] = temp;
            }
        }
    }
}
```

##### 快速排序

快速排序被认为是目前基于比较的内部排序方法中最好的方法。

快速排序属于不稳定算法，适用于顺序存储

选取枢纽元素Key,这里选择子表表头元素

空间复杂度

    最好情况 $O(nlog_2n)$ 最坏情况 $O(nlog_2n)$ 平均情况$O(n^2)$ 

时间复杂度 $O(log_2n)$ 

```c
#include<iostream>
using namespace std;
#define MAXSIZE 200
typedef int ElemType;
typedef struct {
    ElemType data[MAXSIZE+1];
    int length;
} SqList;

void quickSort(SqList &a,int low,int high){
    int i,j,temp,key;
    if(low<high){
        i=low;
        j=high;
        key=a.data[low]; // 用子表的第一个记录作枢纽记录
        while(i<j){      // 从表的两端交替向中间扫描
            while(i<j&&a.data[j]>=key) j--;
            a.data[i]=a.data[j];  // 将比枢纽记录小的移到低端
            while(i<j&&a.data[i]<=key) i++; // 将比枢纽记录大的记录移到高端
            a.data[j]=a.data[i];
        }
        a.data[i]=key;                  //枢纽归位
        quickSort(a,low,i-1);           //对低子表递归排序
        quickSort(a,i+1,high);          //对高子表递归排序
    }
}
void QSort(SqList &L){
    // 对顺序表L作快速排序
    quickSort(L, 1, L.length);
}
```

```cpp
void quickSort(vector<int>& a,int low,int high){
    int i,j,temp,key;
    if(low<high){
        i=low;
        j=high;
        key=a[low];
        while(i<j){
            while(i<j&&a[j]>=key) j--;
            a[i]=a[j];
            while(i<j&&a[i]<=key) i++;
            a[j]=a[i];
        }
        a[i]=key;
        quickSort(a,low,i-1);
        quickSort(a,i+1,high);
    }
}
```

> 2014年算法实现快速排序，进行数据结构定义
> 
> 2018年算法应用写出由大到小排序时每一趟的运算结果

#### 选择排序

##### 简单选择排序

属于不稳定排序算法，适合顺序存储、链式存储

将表分为有序部分和无序部分，每次从无序部分中选取最小的元素，然后放入有序部分中

```c
// 简单选择排序
void selectSort(vector<int>& a){
    int i,j,temp,min;
    for(i=0;i<a.size()-1;i++){
        min=i;
        for(j=i+1;j<a.size();j++){
            if(a[j]<a[min]){
                min=j;
            }
        }
        temp=a[i];
        a[i]=a[min];
        a[min]=temp;
    }
}
```

空间复杂度：$O(1)$  时间复杂度$O(n^2)$ 

> 练习：在链式结构上实现简单选择排序
> 
> ```c
> void SimpleSelectSortLinklist(Linklist *&head)
> {
>     Linklist *p,*q,*s;
>     int min.t;
>     if(head == 0 || head->next == 0) return;
>     for(q=head; q!=0; q=q->next)
>     {
>         min = q->data;
>         s=q;
>         for(p=q->next; p!=0; p=p->next)
>         {
>             if(min>p->data) 
>                 {
>                     min=p->data;
>                     s=p;
>                 }
>         }
>         if(s!=q)
>         {
>             t=s->data;
>             s->data=q->data;
>             q->data=t;
>         }
>     }
> }
> ```

##### 堆排序

堆排序是不稳定的算法

基于大根堆的堆排序得到”递增序列“，基于小根堆的堆排序得到“递减序列”

```c
typedef SqList HeapType;
void HeadAdjust(HeapType &H,int k, int len){
    rc = H.r[s];                  //暂存子树的根节点
    for(int i=2*k; i<=len; i*=2){ // 沿key较大的子结点向下筛选
        if(i<len && H.r[i]<H.r[i+1])  
            ++i;                // 取key较大的子结点的下标
        if(rc>=H.r[i]) break;     //筛选结束
        H.r[k] = H.r[i];
        k = i;
    }
    H.r[k] = rc;
}
void HeapSort(HeapType &H, int H.length){
    // 建立初始大根堆
    for(int i=H.length/2;i>0;--i) //从后往前调整所有非终端结点
        HeadAdjust(H,i,H.length);
    for(int i=H.length; i>1; --i){
        swap(H.r[i],H.r[1]);
        HeapAdjust(H,1,i-1);
    }
}
```

> 2007年算法填空题
> 
> 2013年算法应用题
> 
> 2014年算法填空
> 
> 2016年算法应用题
> 
> 2019年算法设计题：写出堆排序的算法
> 
> 2020年代码阅读：堆排序

建堆的时间复杂度$O(n)$ 而排序的时间复杂度为$O(nlog_2n)$ ，空间复杂度为$O(1)$ 

堆排序不稳定（存在一个结点的左右孩子相等时）

#### 归并排序与基数排序

##### 归并排序

把两个或多个有序的子序列合并为一个，一般用2路归并

```cpp
// 归并操作
void merge(vector<int>& a,int low,int mid,int high){
    int i,j,k;
    vector<int> b(high-low+1);
    for (k = 0; k<high-low+1; k++)
        b[k] = a[k+low];
    for( i = 0, j = mid+1-low, k = low; i <= mid-low && j<=high-low; k++){
        if(b[i]<=b[j])
            a[k] = b[i++];
        else
            a[k] = b[j++];
    }02
    while(i <= mid-low) a[k++] = b[i++];
    while(j <= high-low) a[k++] = b[j++];
}
// 归并排序
void mergeSort(vector<int>& a,int low,int high){
    int mid;
    if (low < high){
        mid = (low+high)/2;
        mergeSort(a,low,mid);
        mergeSort(a,mid+1,high);
        merge(a,low,mid,high);
    }
}
```

空间复杂度为$O(n)$

时间复杂度为$O(log_2n)$ 

> 练习：设计链式存储结构上的归并排序

##### 基数排序

将关键字拆分为d位，按照权重递增做分配喝手机

空间复杂度$O(r)$ r为关键字位可能取到的值的个数

时间复杂度$O(d(n+r))$ 

基数排序属于稳定算法

适用于元素个数很大但关键字可以拆分为d组，关键字的取值为r，d,r都较小

#### 内部排序算法的比较

###### 总结

1.若n较小，可采用直接插入排序或简单选择排序
2.当记录本身信息量较大时,用简单选择排序较好
3.若文件的初始状态已按关键字基本有序，则选用直接插入或冒泡排序为宜
4.快速排序被认为是目前基于比较的内部排序方法中最好的方法，待排序的关键字随机分布时,快速排序的平均时间最短
5.若n较大,则应采用时间复杂度为$O(nlog2n)$  的排序方法:快速排序、 堆排序或归并排序
6.要求排序稳定且时间复杂度为$O(nlog2n)$ 则可选用归并排序
7.若n很大,记录的关键字位数较少且可以分解时,采用基数排序较好
8.当记录本身信息量较大时,为避免耗费大量时间移动记录,可用链表作为存储结构

#### 外部排序
