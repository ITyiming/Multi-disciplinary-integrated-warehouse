# 第一章 语言基础

## 第一节：C++基础格式与版本选择

- '\n'输出比endl更快，但是不会清除缓存

## 第二节：输入输出

- 万能开头：`#include<bits/stdc++.h>`
- 取消同步流（可以加快cin和cout速度）：`ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);`

## 第三节：string的使用

### （1）注意

如果不使用万能头文件#include<bits/stdc++.h>，则需要在开头写上#include<string>（最好也写上#include<string.h>），如果要输入带有空格的字符串可以选择用`getline(cin,字符串名称)`，或者用for循环输入。

### （2）string的声明和初始化

1. `string s=”（里面是你想填的东西）”;`
2. `string s1=s;`（使用另一个string对象来初始化）
3. `string s2=s.substr(起始位置,长度);`（截取部分字符串进行初始化）
4. `const char* arr=”（里面是你想填的东西）”; string s3(arr);`（使用字符数组初始化字符串）
5. `string s4(5,’A’);`（使用重复的字符进行初始化）5是重复的字符的个数，’A’是重复的字符

### （3）string的各种基本操作

1. 获取字符串长度: `string s=”Hello world”; int length=s.length();`（或者是`int length=s.size();`）
2. 拼接字符串: 
    ```cpp
    string s1=”Hello”,s2=”world”,s;
    s=s1+” “+s2; // 或者是s=s1.append(“ ”).append.(s2);

3. 字符串查找:
    ```cpp
    string s=”Hello world”;
    int pos=s.find(“world”);
    if(pos!=string::npos)
        cout<<”位置是：”<<pos<<’\n’;
    else
        cout<<”不存在”<<’\n’;
    ```
    `string::npos`返回值是-1，`s.find(“world”)`，如果有找到”world”，那么返回值应该是”w”的位置，如果没有找到那么返回值应该是-1。
4. 字符串的替换:
    ```cpp
    string s=”Hello world”;
    s.replace(起始位置,长度，用于替换的字符串); 
    ```
5. 提取子字符串:
    ```cpp
    string s=”Hello world”;
    string s1=s.substr(起始位置,长度);
    ```
6. 字符串的比较:
    ```cpp
    string s1=”abcd”;
    string s2=”das”;
    // 可以直接用>、<、=判断，因为string是重载了不等号的
    // 也可以用s1.compare(s2)或strcmp(s1,s2)进行判断，二者判断方式相同
    ```

### （4）遍历string字符串的方法

1. for循环枚举下标:
    ```cpp
    string s=”Hello world”;
    int length=s.length();
    for(int i=0;i<length;i++)
    {
        cout<<s[i]<<’\n’;
    }
    ```

2. auto枚举:
    ```cpp
    string s=”Hello world”;
    for(auto i:s)
    {
        cout<<i;
        // i=’a’; // 此时i是复制了字符串s的字符，如果对i进行更改是改不了
    }
    for(auto &i:s)
    {
        cout<<i;
        // i=’a’; // 有了&,此时i是字符串s里的字符串，可以对i进行更改
    }
    ```

### 例题：

#### 题目描述

实现一个算法来实现反转字符数组的功能。反转的要求如下：
1. 将字符数组的字符进行反转，例如［' b ','',' a ','］变成［ r ',' a ','',' b '］。
2. 将字符数组替换为反转后的数组。

#### 输入描述

读入一行字符串，长度不超过100，字符串可能含有空格。

#### 输出描述

输出一行字符串，该字符串为读入字符串的反转字符串。

#### 示例：

输入：`b ar`

输出：`ra b`

#### 程序：

```cpp
#include<bits/stdc++.h>
using namespace std;
int main()
{
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    string s;
    getline(cin,s);
    int length=s.length();
    // 法一(倒序输出)：
    for(int i=length;i>=0;i--)
        cout<<s[i];
    cout<<’\n’;
    return 0;
}
// 个人感觉练习的时候还是别用，但是如果比赛允许可以直接用

// 法二：
reverse(s.begin(),s.end());
cout<<s;
return 0;
}

// 法三：
for(int i=0;i<length/2;i++)
    swap(s[i],s[length-1-i])

// 法四：
char temp;
for(int i=0;i<length/2;i++)
{
    temp=s[i];
    s[i]=s[length-1-i];
    s[length-1-i]=temp;
}
return 0;
```
# 第二章 竞赛常用库函数

## 第一节 排序

### （1）sort简介

需要在头文件里写上 `#include<algorithm>` 或者使用万能头文件。
默认从小到大排序。

### （2）sort用法

1. `sort(起始地址,结束地址,)`（个人觉得最好用的一个）
    - 举个例子：
    ```cpp
    int a[]={2,3,45,1,9,4,6};
    int size=sizeof(a)/sizeof(a[0]);
    // 法一：
    sort(a,a+size);
    // 法二：（这个适合于从头到尾，不能选择到第几个）
    sort(a.begin(),a.end());
    ```
   
2. `sort(起始地址，结束地址，比较函数（布尔型）)`
    - 举个例子：
    ```cpp
    bool cmp(const int &u,const int&v);
    int a[]={2,3,45,1,9,4,6};
    int size=sizeof(a)/sizeof(a[0]);
    // 法一：
    sort(a,a+size,cmp);
    // 法二：（这个适合于vector数列且从头到尾，不能选择到第几个，如果要选择第几个则把a.end()改为a.begin()+n）
    sort(a.begin(),a.end(),cmp);
    ```

3. `sort(起始地址，结束地址，lambda表达式（匿名函数）)`
    - 举个例子：
    ```cpp
    int a[]={2,3,45,1,9,4,6};
    int size=sizeof(a)/sizeof(a[0]);
    sort(a,a+size,[](const int &u,const int &v) {
        return u>v;
    });
    ```

4. 运算符重载函数（这个会比较快一点）
    - 举个例子：
    ```cpp
    struct node {
        int u,v;
        bool operator <(const node &m)const {
            return u==m.u?v<m.v:u<m.u;
        }
    };
    ```

## 第二节 最值查找

### 1、min和max函数

- min和max都能传入两个数或者一个列表，时间复杂度是O(1)。
- 举个例子：
    ```cpp
    min(3,4)=3;
    min({1,2,3,4})=1;
    max(3,4)=4;
    max({1,2,3,4})=4;
    ```

### 2、min_element和max_element函数

- 用法：`min_element(st,ed)`返回地址[st,ed)中最小值的下标或迭代器，传入两个地址或迭代器；`max_element(st,ed)`返回地址[st,ed)中最大值的下标或迭代器，传入两个地址或迭代器。

### 3、nth_element函数

- 用法：`nth_element(st,k,ed)`用于对一个数列进行部分排序，返回值是void()。

### 例题：

```cpp
#include<algorithm>
using namespace std;
int main()
{
    int data[200],x;
    for(int i=0;i<200;i++) data[i]=4*i+6;
    cin>>x;
    lower_bound(data,data+200,x);
    cout<<(lower_bound(data,data+200,x)-data)<<endl;
    return 0;
}
```

# 第二章 竞赛常用库函数

## 第一节 排序

### （1）sort简介

需要在头文件里写上 `#include<algorithm>` 或者使用万能头文件。
默认从小到大排序。

### （2）sort用法

1. `sort(起始地址,结束地址,)`（个人觉得最好用的一个）
    - 举个例子：
    ```cpp
    int a[]={2,3,45,1,9,4,6};
    int size=sizeof(a)/sizeof(a[0]);
    // 法一：
    sort(a,a+size);
    // 法二：（这个适合于从头到尾，不能选择到第几个）
    sort(a.begin(),a.end());
    ```
   
2. `sort(起始地址，结束地址，比较函数（布尔型）)`
    - 举个例子：
    ```cpp
    bool cmp(const int &u,const int&v);
    int a[]={2,3,45,1,9,4,6};
    int size=sizeof(a)/sizeof(a[0]);
    // 法一：
    sort(a,a+size,cmp);
    // 法二：（这个适合于vector数列且从头到尾，不能选择到第几个，如果要选择第几个则把a.end()改为a.begin()+n）
    sort(a.begin(),a.end(),cmp);
    ```

3. `sort(起始地址，结束地址，lambda表达式（匿名函数）)`
    - 举个例子：
    ```cpp
    int a[]={2,3,45,1,9,4,6};
    int size=sizeof(a)/sizeof(a[0]);
    sort(a,a+size,[](const int &u,const int &v) {
        return u>v;
    });
    ```

4. 运算符重载函数（这个会比较快一点）
    - 举个例子：
    ```cpp
    struct node {
        int u,v;
        bool operator <(const node &m)const {
            return u==m.u?v<m.v:u<m.u;
        }
    };
    ```

## 第二节 最值查找

### 1、min和max函数

- min和max都能传入两个数或者一个列表，时间复杂度是O(1)。
- 举个例子：
    ```cpp
    min(3,4)=3;
    min({1,2,3,4})=1;
    max(3,4)=4;
    max({1,2,3,4})=4;
    ```

### 2、min_element和max_element函数

- 用法：`min_element(st,ed)`返回地址[st,ed)中最小值的下标或迭代器，传入两个地址或迭代器；`max_element(st,ed)`返回地址[st,ed)中最大值的下标或迭代器，传入两个地址或迭代器。

### 3、nth_element函数

- 用法：`nth_element(st,k,ed)`用于对一个数列进行部分排序，返回值是void()。

### 例题：

```cpp
#include<algorithm>
using namespace std;
int main()
{
    int data[200],x;
    for(int i=0;i<200;i++) data[i]=4*i+6;
    cin>>x;
    lower_bound(data,data+200,x);
    cout<<(lower_bound(data,data+200,x)-data)<<endl;
    return 0;
}
```

## 第三节 二分查找

### 1、二分查找的前提

- 需要引入头文件 `#include<algorithm>`。
- 只能对数组进行查找。
- 数组的元素必须是单调不减或单调不增的。

### 2、binary_search函数

- 用法：`binary_search(起始地址，结束地址，目标值)`。

### 3、lower_bound和upper_bound函数

- 功能：获取找到的元素的位置。

1. 例题：略

## 第四节 大小写转换

### 1、islower和isupper函数

- 用法：`islower(ch)`和`isupper(ch)`。

### 2、tolower和toupper函数

- 用法：`tolower(ch)`和`toupper(ch)`。

### 3、ASCII码

## 第五节 全排列

### 1、next_permutation函数

- 功能：用于生成当前序列的下一个序列，按照字典序进行排列。

### 2、pre_permutation函数

- 功能：用于生成当前序列的上一个序列，按照字典序排序。

## 第六节 其他库函数

### 1、memset()函数

- 功能：用于设置内存块的值。

### 2、swap()函数

- 功能：用于交换变量的值。

### 3、reverse()函数

- 功能：用于反转容器或者数组中元素的顺序。

### 4、unique()函数

- 功能：用于去除容器中相邻重复的元素。



# 第三章 STL

## vector

### 1、vector的定义和特性

（1）在c++中vector是动态（指大小是动态的）数组容器，可以储存相同类型的元素，如果元素的类型不同则无法存储在同一个vector容器中，需要添加头文件#include<vector>或者使用万能头文件#include<bits/stdc++.h>

vector声明语法：`vector<数据类型>向量名称`，如: `vector<int> nums`、`vector<double> a`等等

为了方便表示，以下的说明均以`vector<int> nums`为例

（2）元素访问：可以通过索引来访问vector中的元素，索引从0开始，最后一个元素的索引最好用`(int) nums.size() - 1`，不要使用`nums.size() - 1`因为`size()`返回的是`unsigned int`类型，如果vector是空的那么`size()`返回的值会很大容易出问题。

如果要用for循环遍历vector那么可以写成 `for(int i=0; i<nums.size(); i++)`

可以使用`[ ]`或者`at()`函数来访问vector中的元素，如：`nums[0]`、`nums[1]`或者`nums.at(0)`、`nums.at(1)`

（3）元素的添加、删除、插入：可以用

- `push_back()`函数在vector的末尾添加元素，例如：`push_back(1)`就会在末尾添加1
- `pop_back()`删除vector末尾的元素，用法：`nums.pop_back()`即可（一定要在vector非空时使用）
- `insert()`函数在vector中的指定位置插入元素，用法：指定位置：`nums.insert(nums.begin()+i, a)`在第i+1个元素前面插入a；
- `erase()`函数删除vector中指定位置或者指定区间的元素，删除指定位置：`nums.erase(nums.begin()+i)`删除第i+1个元素，删除指定区间：`nums.erase(nums.begin()+i, nums.begin()+j (或者 nums.end()))`删除[i,j-1)间的元素

（4）容器大小管理：可以用

- `size()`函数来获取vector中元素的数量 用法：`nums.size()`;
- `empty()`函数来检查vector是否为空，如果是空的则返回true，否则返回false 用法：`nums.empty()`;
- `resize()`函数来调整vector的大小 用法：`resize(你所要设置的vector的size()大小)`，如果设置的size()比原来大，那么vector会自动补上0使得vector变为调整的大小，也可以设置补上的元素，例如：`resize(你所要设置的vector的size()大小, 10)`，此时补上的元素就会变成10。

（5）迭代器：vector提供了迭代器，可用于遍历数组vector中的元素，可以使用`begin()`来获取vector的第一个元素的迭代器，使用`end()`来获取vector中最后一个元素的下一个位置的迭代器（nums.begin()到nums.end()是一个左闭右开的区间，也就是说nums.begin()取得到，nums.end()取不到，还有一点就是迭代器之间是不能比较大小的，只有相等和不等。

用于遍历的话可以是：

```cpp
vector<int>::iterator it;
for(it=nums.begin(); it!=nums.end(); it++) {
    cout << *it << " ";
}
```

或者是

```cpp
for(auto it=nums.begin(); it!=nums.end(); it++) {
    cout << *it << " ";
}
```

### 2、vector的排序去重

（1）去重思路：先用sort函数排序，让重复的元素相邻，然后用unique函数将vector重复的元素移到后面，并用last接收unique的返回值（因为unique返回的是重复元素的中第一个），然后用erase函数将重复元素去除。

（2）示例代码：

```cpp
sort(nums.begin(), nums.end());
auto last = unique(nums.begin(), nums.end());
erase(last, nums.end());
```

### 3、代码示例：

```cpp
#include<iostream>
#include<vector>
#include<algorithm>
#include<utility>
using namespace std;

int main() {
    vector<int> nums;
    nums.push_back(5);
    nums.push_back(2);
    nums.push_back(8);
    nums.push_back(5);
    nums.push_back(1);
    nums.push_back(2);
    nums.push_back(9);
    nums.push_back(8);

    //打印原始向量中的元素
    cout << "原始向量中的元素是：";
    for(int &i : nums) {
        cout << i << " ";
    }
    cout << '\n';

    //排序向量并打印 
    sort(nums.begin(), nums.end());
    cout << "排序后的向量：";
    for(int i : nums) {
        cout << i << " ";
    }
    cout << '\n';

    //对向量去重并打印 
    auto last = unique(nums.begin(), nums.end());
    nums.erase(last, nums.end());
    cout << "去重后的向量：";
    for(auto &i : nums) {
        cout << i << " ";
    }
    cout << '\n';

    //对向量插入一个元素并打印 
    nums.insert(nums.begin()+2, 3);
    cout << "插入元素后的向量：";
    for(auto &i : nums) {
        cout << i << " ";
    }
    cout << '\n';

    //删除向量中的某个元素并打印 
    nums.erase(nums.begin()+2);
    cout << "删除元素后的向量：";
    for(auto &i : nums) {
        cout << i << " ";
    }
    cout << '\n';

    if(nums.empty()) {
        cout << "该向量是空的" << '\n';
    }
    else {
        cout << "该向量不是空的" << '\n';  
    }

    int size = nums.size();
    //获取向量的大小并打印 
    cout << "该向量大小是：" << size <<

 '\n';

    //清空向量并检查 
    nums.clear();
    if(nums.empty()) {
        cout << "该向量是空的" << '\n';
    }
    else {
        cout << "该向量不是空的" << '\n';  
    }

    return 0;
}
```

## pair

### 1、pair的定义和结构

（1）pair是模板类，用于表示一对值的组合，需要添加头文件`#include<utility>`或者万能头文件`#include<bits/stdc++.h>`

（2）pair的结构

pair类有两个成员变量：`first`和`second`，分别表示第一个值和第二个值，`first`和`second`可以是整型、浮点型，也可以是结构体、类等等

（3）pair用法：示例：

```cpp
pair<int, double> p1(1, 3.14);
```

### 2、pair的嵌套

pair进行嵌套，也就是说可以将一个pair对象作为另一个pair对象的成员

代码示例：

```cpp
pair<int, pair<char, double>> p1(1, make_pair('p', 3.14));
```

### 3、pair自带的排序规则

pair自带的排序规则是按照`first`成员进行升序排序，如果`first`成员大小相等则按照`second`成员大小进行排序，也就是说，如果你用sort进行排序，那么会优先对`first`成员进行升序排序。

例如：

```cpp
#include<iostream>
#include<utility>
#include<algorithm>
#include<vector>
using namespace std;

int main() {
    vector<pair<int, int>> v;
    v.push_back(make_pair(3, 4));
    v.push_back(make_pair(5, 1));
    v.push_back(make_pair(1, 7));
    sort(v.begin(), v.end());
    for(auto &i : v) {
        cout << i.first << "," << i.second << '\n';
    }
    return 0;
}
```
输出结果：
```
1,7
3,4
5,1
```
如果想要按照其他排序规则对pair进行排序可以通过自定义比较函数或者使用lambda表达式来实现（用法见sort）

### 4、代码示例

```cpp
#include<iostream>
#include<vector>
#include<algorithm>
#include<string>
using namespace std;

struct Person {
    string name;
    int age;
};

int main() {
    vector<Person> p;
    p.push_back({"张三", 18});
    p.push_back({"李四", 22});
    p.push_back({"王五", 24});
    vector<pair<Person, int>> score;
    score.push_back({p[0], 90});
    score.push_back({p[1], 80});
    score.push_back({p[2], 70});
    for(auto i : score) {
        cout << "Name: " << i.first.name << " ";
        cout << "Age: " << i.first.age << " ";
        cout << "Score: " << i.second << '\n';
    }
    return 0;
}
```
输出结果：
```
Name: 张三 Age: 18 Score: 90
Name: 李四 Age: 22 Score: 80
Name: 王五 Age: 24 Score: 70
```

## list

### 1、list的定义和结构

需要包含头文件`#include<list>`或者使用万能头文件`#include<bits/stdc++.h>`

（1）T：指定容器中存储的元素类型
Allocater（可选）：指定用于分配内存的分配器类型，一般默认为：Allocater<T>

特点：
（2）双向性：每个节点都包含指向前一个和后一个节点的指针，因此可以在常数时间内在链表中的任意位置进行插入、访问、删除操作，一般插入和删除操作的时间复杂度是O(1)，而访问操作的时间复杂度是O(n)，n是数组大小，因此如果要进行随机访问的操作最好使用支持随机访问的容器，例如vector或者deque
（3）动态大小：链表可以根据大小动态扩展或收缩，无需预先指定容器大小
（4）不连续存储：链表中的节点在内存中是在任意位置分布的，因此删除或插入不会导致链表中的元素移动

list提供了一系列成员函数和迭代器来操作和访问链表中的元素，包括插入、访问、删除、反转等操作

### 2、list常用函数

（1）`push_back`：将元素插入到链表的末尾
（2）`push_front`：将元素插入到链表的开头
（3）`pop_back`：将链表末尾的元素删除
（4）`pop_front`：将链表开头的元素删除
（5）`size()`：返回链表元素个数
（6）`empty()`：检查链表是否为空，若是空则返回1，否则返回0
（7）`clear()`：清空链表
（8）`front()`：返回链表第一个元素的引用
（9）`back()`：返回链表最后一个元素的引用
（10）`begin()`：指向链表第一个元素的迭代器
（11）`end()`：指向链表最后一个元素下一个位置的迭代器
（12）`insert()`：在链表中插入一个或多个元素
（13）`erase()`：删除指定位置或指定区间的元素

### 3、代码示例

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <utility>
#include <list>
using namespace std;

int main() {
    //创建一个list链表
    list<int> my_list;
    //向list尾部添加元素
    for(int i=1; i<6; i++) {
        my_list.push_back(i);
    }
    //输出list中的元素
    for(int &i : my_list) {
        cout << i << " ";
    }
    cout << '\n';
    //将list中的元素反转并输出 
    reverse(my_list.begin(), my_list.end());
    for(int &i : my_list) {
        cout << i << " ";
    }
    cout << '\n';
    //在第一个元素的后一个位置添上0并输出 
    my_list.insert(++my_list.begin(), 0);
    for(int &i : my_list) {
        cout << i << " ";
    }
    cout << '\n';
    //删除第第二个元素并输出 
    my_list.erase(++my_list.begin(), --my_list.end());
    for(int &i : my_list) {
        cout << i << " ";
    }
    cout << '\n';
    //输出list的大小
    cout << my_list.size(); 
    
    return 0;
}
```


## Stack

### 1、**定义和结构**

Stack 是一种先进后出的数据结构，需要包含头文件 `#include<stack>` 或者万能头文件 `#include<bits/stdc+.h>`，Stack 提供了一组函数来访问和操作元素。

**定义和结构如下：**

- `T`: 表示存储在 Stack 中元素的类型。
- `Container`: 表示底层容器的类型，默认为 `deque`，也可以使用其他容器来访问，如 `vector` 或者 `list`。

Stack 实现了使用底层容器来存储元素，并且只能通过特定的函数来访问和操作元素。

### 2、**常用函数**

- `push(x)`: 在栈顶推入元素 `x`，时间复杂度：O(1)。
- `pop()`: 弹出栈顶元素，时间复杂度：O(1)。
- `top()`: 返回栈顶元素，时间复杂度 O(1)。
- `empty()`: 检查栈是否为空，时间复杂度 O(1)。
- `size()`: 返回栈的元素个数，时间复杂度 O(1)。

**小 Tip**：如果将一个数组的元素一次放入栈中再依次取出，则可以将数组反转（但一般不用，可以直接用 `reverse` 函数）。

- 只能对栈顶的元素进行操作。

### 3、**代码实例**

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <utility>
#include <list>
#include <stack>
using namespace std;

int main() {
    // 创建一个栈
    stack<int> myStack;
    // 向栈中推入元素并输出
    for (int i = 10; i <= 40; i += 10) {
        myStack.push(i);
    }
    // 获取栈顶元素
    cout << "栈顶元素是：" << myStack.top() << '\n';
    // 弹出栈顶元素
    myStack.pop();
    // 再次获取栈顶元素
    cout << "栈顶元素是：" << myStack.top() << '\n';
    // 检查栈是否为空
    if (myStack.empty())
        cout << "栈为空" << '\n';
    else
        cout << "栈不为空" << '\n';
    // 获取栈的大小
    cout << "栈的大小为：" << myStack.size();
    
    return 0;
}
```

---

## Queue

### 1、**队列**

- Queue 是一种先进先出的数据结构。
- 提供了一组函数来访问和操作元素。

**定义和结构如下：**

```cpp
template<class T, class Container=deque<T>>
class queue;
```

    - `T`: 表示存储在队列中的元素的类型。
    - `Container`: 表示底层容器的类型，默认为 `deque`，也可以使用其他类型的容器，如 `list`。
    
    Queue 实现了使用底层容器来存储元素，并且只能通过特定的函数来访问和操作元素。

### 2、**常用函数**

- `push(x)`: 在队尾插入元素 `x`，时间复杂度为 O(1)。
- `pop()`: 弹出顶部的元素，时间复杂度为 O(1)。
- `front(()`: 返回顶部的元素，时间复杂度为 O(1)。
- `back()`: 返回队尾的元素，时间复杂度为 O(1)。
- `empty()`: 检查队列是否为空，时间复杂度为 O(1)。
- `size()`: 检查队列中的元素个数，时间复杂度为 O(1)。

### 3、代码实例

```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
    queue<string> V;
    queue<string> N;
    int times;
    cin >> times;
    while (times--) {
        string op;
        cin >> op;
        if (op == "IN") {
            string name, type;
            cin >> name >> type;
            if (type == "V")
                V.push(name);
            else
                N.push(name);
        } else {
            string type2;
            cin >> type2;
            if (type2 == "V")
                V.pop();
            else
                N.pop();
        }
    }
    while (V.size()) {
        cout << V.front() << '\n';
        V.pop();
    }
    while (N.size()) {
        cout << N.front() << '\n';
        N.pop();
    }
    return 0;
}
```

---

## Set

### 1、**集合**

- Set 是一种容器，用于存储一组唯一的元素，默认情况下，set 中的元素按照升序排序，使用的比较运算符是 `<`。
- Set 内部实现了使用红黑树来存储元素，并保持元素的有序性，因此，set 中查找、删除和插入元素的时间复杂度都是 O(logN)。

### 2、**常用操作**

- `insert(x)`: 向 set 中插入 `x`，时间复杂度是 O(logN)。
- `erase(x)`: 删除集合中的所有 `x` 元素，时间复杂度是 O(logN)。
- `find(x)`: 查找集合中的元素是否存在，时间复杂度为 O(1)。
- `lower_bound(x)`: 返回第一个不小于 `x` 的迭代器，时间复杂度是 O(logN)。
- `upper_bound(x)`: 返回第一个大于 `x` 的迭代器，时间复杂度是 O(logN)。
- `size()`: 返回集合中的元素数量，时间复杂度是 O(1)。
- `empty()`: 检查集合是否为空，时间复杂度是 O(1)。


 - `clear()`: 清空集合，时间复杂度是 O(1)。
    - `begin()`: 返回集合起始位置的迭代器，时间复杂度是 O(1)。
    - `end()`: 返回集合末尾的下一个位置的迭代器，时间复杂度是 O(1)。
    - `rbegin()`: 返回集合末尾位置的迭代器，时间复杂度是 O(1)。
    - `rend()`: 返回集合其实位置的迭代器，时间复杂度是 O(1)。

### 3、**代码示例**

```cpp
#include<iostream>
#include<set>
using namespace std;

int main() {
    set<int> mySet;
    // 插入元素
    mySet.insert(5);
    mySet.insert(2);
    mySet.insert(8);
    mySet.insert(2);
    // 遍历集合
    for (auto &i : mySet)
        cout << i << " ";
    cout << '\n';
    // 查找元素
    int SearchValue = 5;
    auto it = mySet.find(SearchValue);
    if (it != mySet.end())
        cout << SearchValue << " is found in the set" << '\n';
    else
        cout << SearchValue << " is not found in the set" << '\n';
    // 移除元素
    int removeValue = 2;
    mySet.erase(removeValue);
    // 再次遍历 set
    for (auto &i : mySet)
        cout << i << " ";
    cout << '\n';
    // 清空集合
    mySet.clear();
    // 判断集合是否为空
    if (mySet.empty())
        cout << "the set is empty";
    else
        cout << "the set is not empty";
    cout << '\n';
    return 0;
}
```

### 4、**Multiset 代码示例**

```cpp
#include<iostream>
#include<set>
using namespace std;

int main() {
    multiset<int> mySet;
    // 插入元素
    mySet.insert(5);
    mySet.insert(2);
    mySet.insert(8);
    mySet.insert(2);
    // 遍历集合
    for (auto &i : mySet)
        cout << i << " ";
    cout << '\n';
    // 查找元素
    int SearchValue = 5;
    auto it = mySet.find(SearchValue);
    if (it != mySet.end())
        cout << SearchValue << " is found in the set" << '\n';
    else
        cout << SearchValue << " is not found in the set" << '\n';
    // 移除元素
    int removeValue = 2;
    mySet.erase(mySet.find(removeValue));
    // 再次遍历 set
    for (auto &i : mySet)
        cout << i << " ";
    cout << '\n';
    // 清空集合
    mySet.clear();
    // 判断集合是否为空
    if (mySet.empty())
        cout << "the set is empty";
    else
        cout << "the set is not empty";
    cout << '\n';
    return 0;
}
```


## Map

### 1、**定义和结构**

- Map 是一种关联容器，用于存储一对键值对，每个键都是唯一的。
- Map 容器根据键来自动进行升序排序，并且可以通过键来快速查找对应的值。
- Map 容器使用红黑树数据结构来实现，具有较快的查找、删除、插入操作，时间复杂度为 O(logN)。

### 2、**常用函数**

- `insert`: 插入元素。
- `erase`: 删除元素。
- `find`: 查找元素。
- `count(key)`: 统计元素个数，比如说 key 为 1 有 2 个，则 `count(1)==2`，但是 map 中的 key 是唯一的，所以 count 在 map 可以用于判断这个 key 是否存在，在 multimap 则可以统计 key 所对应的值有多少个。
- `size`: 返回元素个数。
- `begin()`: 返回指向容器起始位置的迭代器。
- `end()`: 返回指向容器末尾位置的迭代器。
- `clear()`: 清空容器。
- `empty()`: 判断容器是否为空。
- `lower_bound`: 返回指向第一个大于等于指定键的元素位置。
- `upper_bound`: 返回指向第一个大于指定键的元素位置。

### 3、**代码示例**

```cpp
#include<iostream>
#include<map>
using namespace std;

int main() {
    // 创建一个 map 并初始化
    map<int,string> mp = {{1,"apple"}, {3,"orange"}, {2,"banana"}};
    // 插入一个元素
    mp.insert(make_pair(4,"grape"));
    // 访问和查找元素
    cout << "value at key 2: " << mp[2] << '\n';
    // 遍历并打印元素
    for(auto &i : mp)
        cout << "key: " << i.first << " value: " << i.second << '\n'; 
    // 移除元素并判断其是否存在
    mp.erase(3);
    if(mp.count(3) == 0)
        cout << "is not found in the set" << '\n';
    // 清空元素
    mp.clear();
    // 判断集合是否为空
    if(mp.empty())
        cout << "set is empty";
    else
        cout << "empty is not empty";
    cout << '\n'; 
    return 0;
}
```

# 第四章 基础算法

## 时空复杂度

### 时间复杂度

1. 时间复杂度是衡量算法执行时间随输入规模增长的增长率。
2. 通过分析算法中基本操作的执行次数来确定时间复杂度。
3. 常见的时间复杂度：常数时间O(1)、线性时间O(n)、对数时间O(logn)、平方时间O(n^2)。
4. 计算的时候应该关注时间复杂度的数量级，而非表达式。
5. 一般关注最坏的时间复杂度，用O(f(n))表示，大多数时候仅需估算。
6. 一般来说评测机1s跑1e8次，所以尽可能把程序运算规模的数量级控制在1e8以内。

### 空间复杂度

1. 空间复杂度是衡量算法执行过程中所需的存储空间随输入规模增长的增长率。
2. 通过分析算法中所使用的额外存储空间大小来确定空间复杂度。
3. 常见的空间复杂度：常数空间O(1)、线性空间O(n)、对数空间O(logn)、平方空间O(n^2)。
4. 一般关注最坏的空间复杂度，用O(f(n))表示，大多数情况下可以根据开出的数组精确算出，但也存在需要估算的情况。

### 分析技巧

1. 理解基本操作：基本操作（时间复杂度是O(1)，也被称为“原子操作”因为已经不能再继续分解下去了）可以是算数运算、位移操作、赋值操作等等。
2. 关注循环结构：循环是算法中的常见结构，其执行次数对于时间复杂度的计算至关重要。
3. 递归算法：递归算法的时间和空间复杂度的分析较为复杂，需要确定递归的深度以及每个递归的调用的时间和空间开销。
4. 最坏情况分析：对于时间复杂度的分析，通常考虑最坏情况下的执行时间，要考虑输入数据使得算法执行时间达到最大值的情况。
5. 善用结论：某些常见算法的时间和空间复杂度已被广泛研究和证明，可利用这些已知结论来分析算法的复杂度。

### 代码示例

1. 这里再分析一下空间复杂度：这段代码没有开数组或者vector其他的容器，因此额外空间就只有那些常数，那些常数的空间复杂度是O(1)，虽然总共有4个，但是空间复杂度也是算O(1),即使是100个也算O(1)，常数空间是不随输入规模变化的。
2. 时间复杂度的分析：i循环了n次，j循环了n/i次，i每循环一次，j就循环n/i次，而i要循环n次，所以时间复杂度就是n/i向下取整，然后i从1到n求和，而n是可以拿到外面的，然后就拿到外边，则另一个就变成那样，也叫做“调和级数”，这个约等于logn，因此就得到了时间复杂度：O(nlogn)。
3. 总共有2^n个节点，则递归就要执行2^n次，时间复杂度就变成了2^n；斐波那契数列的递归函数主体（就是第一个if）的时间复杂度是O(1)，而因为第二个return要递归下去，所以时间复杂度为O(2^n)。

## 枚举

### 枚举算法介绍

1. 将问题的解空间当中的每个可能的解枚举出来并进行验证和比较，找到满足问题的最优解或者所有解。
2. 适用于规模较小、解空间可枚举的情况。
   - 优点：简单直观、易于实现。
   - 缺点：问题规模较大时，时间复杂度可能会很大，效率很低。

### 解空间

- 可以是一个范围内的所有数字（或字符串、二元组等数据）、或者满足某个条件的所有数字，也可以是解空间树（一般分为子集树和排列树，针对解空间树需要用回溯法进行枚举）。

### 循环枚举解空间

1. 首先确定解空间的维度，即问题中需要枚举的变量个数。
2. 对于每个变量，确定其可能的取值范围。这些范围可以根据问题的性质和约束条件来确定，这步往往是优化时间复杂度的关键。
3. 在循环体内，针对每个可能解进行处理，可以进行验证、计算、输出等操作。

## 模拟

### 模拟算法

模拟算法通过模拟实际情况来解决问题，一般容易理解但实现起来较复杂，需要注意许多细节和特殊情况。模拟题一般由许多简单但不易处理的部分组成，考察选手的细心程度和整体逻辑思维。

通常为了使模拟题写得更清晰，经常会编写许多小函数来辅助解题，例如整数和字符串类型的相互转换、回文串的判断、日期的转换、各种特殊条件的判断等等。

## 递归

#### 1. 递归的介绍

- **递归的概念：** 递归是指函数直接或间接调用自身的过程。
- **递归的两个关键要素：**
  - 基本情况（递归终止条件）：递归中的一个条件，当满足该条件时，递归终止，避免无限递归。它解决了极小规模问题的方法。
  - 递归表达式（递归调用）：递归函数中的语句，用于解决规模更小的子问题，再将子问题的答案合并成当前问题的答案。

#### 2. 递归的实现

- **递归函数的基本结构：**
  ```cpp
  返回类型 函数名(参数列表) {
      // 基本情况（递归终止条件）
      if (满足终止条件) {
          返回终止条件下的结果
      }
      // 递归表达式（递归调用）
      else {
          // 将问题分解为规模更小的子问题
          // 使用递归调用解决更小的子问题
          // 返回子问题的结果
      }
  }

1. **递归函数的基本结构**：

- **设计时需要注意的细节：**
  - 确保递归能找到出口，避免无限递归。
  - 考虑边界条件，有时候递归出口不止一个。
  - 避免不必要的重复计算，尽可能优化递归函数的性能（例如使用记忆化，或进行剪枝）。

## 进制转换

1. **进制本质：**
   - 对于一个十进制数字来说，例如153，其本质是每一个数位上的数字乘上该位的权重。
   - 二进制只不过是把10换成了2。

2. **将任意进制数转换为十进制数：**
   
3. **将十进制数转换为任意进制数：**

## 快速幂

快速幂是高效求次方的算法，可以迅速计算大数的幂运算。

#### 示例代码：
```cpp
// 模板1
int ksm(int a, int b) {
    int res = 1;
    while (b) {
        if (b & 1) res *= a;
        a *= a;
        b >>= 1;
    }
}
// 模板2
int ksm(int x, int k) {
    if (k == 0) return 1;
    if (k == 1) return x;
    if (k & 1)  return ksm(x * x, k / 2) * x;
    return ksm(x * x, k / 2);
}
```

## 前缀和

#### 1. 前缀和的原理和特点

前缀和是一种预处理算法，用于快速计算数组的一段区间的和或所有数的和。

#### 2. 实现前缀和

## 差分

#### 1. 差分的原理和特点

差分数组是原数组相邻元素之差构成的数组，可用于快速区间修改和区间查询。

以下是您提供的内容的Markdown格式：

## 离散化

**1、离散化简介**

离散化是一种将数组的值域压缩的算法，其目的是将无限空间中的有限个体映射到有限的空间中，从而提高算法的时空效率。当原数组中的数字很大、负数、小数时（大多数情况下是数字很大），难以将“元素值”表示为“数组下标”，一些依靠下标实现的数据结构和算法无法实现时，我们就可以考虑将其离散化。

例如，假设原数组的元素大小范围是\[1,1e9\]，而数组大小仅为1e5（长度），那么说明元素值的“种类数”最多也就1e5种，因此可以利用一个数组（即离散化数组）来表示某个元素的排名（即第几小），实现值域的压缩，将原数组的元素值作为下标来处理。

离散化数组要求内部是有序的（一般是去重的，当然也存在不去重的方法，但比较少见），可以通过离散化下标得到值，当然也可以通过值得到离散化下标（通过二分实现）。

**2、离散化的实现方法**

离散化实现的方法多样，这里使用`vector`来实现：

```cpp
#include<iostream>
#include<vector>
#include<algorithm>

using namespace std;
const int N = 1e5 + 9;
int a[N]; //原数组
vector<int> L; //离散化数组

//获取值的离散化下标
int getidx(int n) {
    return lower_bound(L.begin(), L.end(), n) - L.begin();
}

int main() {
    int n; cin >> n;
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
        L.push_back(a[i]);
    }

    //排序去重
    sort(L.begin(),L.end());
    L.erase(unique(L.begin(), L.end()), L.end());

    //查找值的离散化下标
    int x; cin >> x;
    cout << getidx(x);
    return 0;
}
```

离散化不会单独考察，一般会结合其他算法或数据结构进行考察，如树状数组、线段树、二维平面的计算几何等。多写几遍离散化过程就当作例题了。

## 贪心

### **1、贪心算法介绍**

贪心算法的基本原理是每一步都选择局部最优解，而尽量不考虑对后续的影响，最终达到全局最优解。贪心算法的局限性在于不能保证获得全局最优解，但在某些问题上具有高效性。

贪心算法的特征包括贪心选择性质和最优子结构性质。贪心选择性质指每次选择的操作都是局部最优的，而最优子结构性质则指问题的最优解可以通过子问题的最优解得到。

### **2、贪心算法实现步骤**

- 确定问题的最优子结构
- 构建贪心选择的策略
- 通过贪心逐步求解问题，直到得到最终解

### **3、例题**

#### 例1

```cpp
#include <bits/stdc++.h>

using namespace std;
using ll=long long;
const int N=1e5+9;
ll diff[N]={0};
ll all[N]={0};

int main()
{
    int n;cin>>n;
    for(int i=1;i<=n;i++)
        cin>>all[i];
    
    sort(all+1,all+1+n);

    for(int i=1;i<=n-1;i++)
        diff[i]=all[i+1]-all[i];

    sort(diff+1,diff+n);

    cout<<diff[1];
    return 0;
}
```

####  例2：

题解：

```cpp
#include<bits/stdc++.h>

using namespace std;
const int N=3e5+9;
int a[N];

int main()
{
    int w;cin>>w;
    
    int n;cin>>n;
    for(int i=0;i<n;i++)
    cin>>a[i];

    sort(a,a+n);

    int l=0,r=n-1,ans=0;
    while(l<=r)
    {
        ans++;
        if(l==r)
        {
            break;
        }
        if(a[l]+a[r]<=w)
        {
            l++;
            r--;
        }
        else
        r--;
    }
    cout<<ans;
    return 0;
}
```

#### 例3：

分类讨论：
第一种情况：所有糖果都一样，也就是说只有一种糖果，那么均分下去就ok了，但是还要看n是否能整除x，如果可以就没事了，如果不行就要多输出，一个才能使字符串最大
第二种情况：s[0]=s[x-1]。如果是这样，那么就将s[x-1]连同剩下的一起输出，这样子才能使开心程度差距尽量小并且字典序最大
第三种情况：s[0]!=s[x-1]。因为字符串已经排序过了，所以字典序一定是从小到大排列的，而字典序的排序是这样的：aa<aaa或者aaa<b，因为s[x-1]和s[0]不一样并且字符串是按照字典序升序排列的，所以直接输出s[x-1]把剩下的扔给s[0]就OK了

最大卡牌价值

```cpp
#include<bits/stdc++.h>

using namespace std;
using ll = long long;
const int N = 1e6 + 9;
pair<ll, pair<ll, ll>>p[N];
vector<ll>v;
int diff[N];

int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int n; cin >> n;
    int k; cin >> k;

    for (int i = 0; i < n; i++)
        cin >> p[i].second.first;
    
    if(n==1)
    {
        cout<<p[0].second.first;
        return 0;
    }

    for (int i = 0; i < n; i++)
        cin >> p[i].second.second;

    for (int i = 0; i < n; i++)
    {
        diff[i] = p[i].second.first - p[i].second.second;
        p[i].first = diff[i];
    }

    sort(p, p + n);

    int i = 0;
    while (k--)
    {
        if (p[i].first >= 0)
            v.push_back(p[i].second.first);
        else 
            v.push_back(p[i].second.second);
        i++;
    }

    for (i; i < n; i++)
        v.push_back(p[i].second.first);

    ll ans = 0;
    for (auto& x : v)
        ans += x;

    cout << ans;

    return 0;
}
```

珠宝的最大交替和

```cpp
#include<iostream>
#include<queue>

using namespace std;
using ll = long long;
const int N = 1e6 + 9;
priority_queue<ll, vector<ll>, greater<ll>>a;
priority_queue<ll, vector<ll>> b;
ll s[N]={0};

int main()
{
    int n; cin >> n;
    
    if(n==1)
    {
        cin>>s[1];
        cout<<abs(s[1]);
        return 

0;
    }

    for (int i = 1; i <= n; i++)
    {
        cin >> s[i];
        if (i & 1)
            a.push(abs(s[i]));
        else
            b.push(abs(s[i]));
    }

    if (a.top() < b.top())
    {
        ll x = a.top(); a.pop();
        ll y = b.top(); b.pop();
        a.push(y);
        b.push(x);
    }

    ll sum = 0;
    while (a.size())
    {
        sum += a.top();
        a.pop();
    }

    while (b.size())
    {
        sum -= b.top();
        b.pop();
    }

    cout << sum;

    return 0;
}
```

小蓝的礼物

```cpp
#include<iostream>
#include<algorithm>

using namespace std;
using ll = long long;
const int N = 1e5 + 9;
ll a[N] = { 0 };

int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int n; cin >> n;
    ll k; cin >> k;
    if(k==0)
    {
        cout<<0;
        return 0;
    }

    if (n == 1)
    {
        cin >> a[1];
        if(a[1]&1)
        {
            if((a[1]/2)+1>k)
            cout<<0;
            else
            cout<<1;
        }
        else
        {
            if(a[1]/2>k)
            cout<<0;
            else
            cout<<1;
        }
        return 0;
    }

    for (int i = 1; i <= n; i++)
    {
        cin >> a[i];
    }

    sort(a + 1, a + 1 + n);

    int i = 1;
    int ans = 0;
    while (k - a[i] >= 0)
    {
        if(i==n)
            break;

        k -= a[i];
        i++;
        ans++;
    }

    if (i == n)
        cout << n;
    else if (k == 0)
    {
        if (i == n)
            cout << n;
        else
            cout << ans;
    }
    else if (k > 0)
    {
        ++i;
        if (k >= a[i] / 2)
            cout << ++ans;
        else
        {
            cout << ans;
        }
    }
    else
        cout << ans;
    return 0;
}
```

四个瓷瓶的神秘游戏

鸡哥的购物挑战

```cpp
#include<iostream>
#include<algorithm>

using namespace std;
using ll = long long;
const int N = 1e5 + 9;
ll a[N];

int main()
{
    int n; cin >> n;
    for (int i = 0; i < n; i++)
        cin >> a[i];

    sort(a, a + n);

    int i = n - 1;
    int cnt = 0;
    ll ans = 0;

    while (a[i] >= 0)
    {
        if (i == 1)
            break;

        ans += a[i];
        i--;
        cnt++;
    }

    if (i == 0)
    {
        if (cnt & 1)
        {
            ans -= a[0];
            cout << ans;
        }
        else
            cout << ans;
        return 0;
    }

    if (cnt & 1)
    {
        if (a[i + 1] + a[i] < 0)
            ans -= a[i+1];
        else
            ans += a[i];
        cout << ans;
    }
    else
        cout << ans;

    return 0;
}
```

冒险者工会

```cpp
#include<iostream>
#include<vector>
#include<algorithm>

using namespace std;
const int N = 1e3 + 9;
vector<int>a;
int b[N][N] = { 0 };
vector<int>v, y;
vector<int>ans;

int main()
{
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int m, n; cin >> m >> n;

    for (int i = 0; i < m; i++)
    {
        int x; cin >> x;
        a.push_back(x);
    }
    sort(a.begin(), a.end());

    int t = 0;
    int tempn = n;
    int xmx = 0;
    while (tempn--)
    {
        
        int k; cin >> k;
        if (k > m)
        {
            cout << -1;
            return 0;
        }
        xmx = max(xmx, k);

        for (int j = 0; j < k; j++)
        {
            int x; cin >> x;
            v.push_back(x);
        }

        sort(v.begin(), v.end(), [](const int& a, const int& b) {
            return a > b;
            });

        for (int j = 0; j < k; j++)
            b[t][j] = v[j];

        v.clear();
        t++;
    }

    for (int i = 0; i < xmx; i++)
    {
        int ymx = 0;

        for (int j = 0; j < n; j++)
            ymx = max(ymx, b[j][i]);

        y.push_back(ymx);
    }

    for (int i = 0; i < y.size(); i++)
    {
        int aidex = lower_bound(a.begin(), a.end(), y[i]) - a.begin();
        if (lower_bound(a.begin(), a.end(), y[i]) == a.end())
        {
            cout << -1;
            return 0;
        }
        else
        {
            int temp = *lower_bound(a.begin(), a.end(), y[i]);
            ans.push_back(temp);
            a.erase(a.begin() + aidex);
        }
    }

    int sum = 0;
    for (int i = 0; i < ans.size(); i++)
        sum += ans[i];

    cout << sum;

    return 0;
}
```
