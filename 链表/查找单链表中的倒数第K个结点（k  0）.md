### 查找单链表中的倒数第K个结点（k > 0）

#### 思路

1.使用两个指针（```first```，```second```）分别指向头节点；

2.```first```指针先走到正向的第k个节点；

3.```first```，```second```同时开始向前走；

4.当```first```走到最后一个节点时，```second```走到倒数第k个节点。

#### 代码实现（以走到倒数第三个节点为例）

#### C++代码

```c++
Node* reGetKthNodePointer(Node *h, int k)
{
    if(k == 0 || !h) return ;
    Node *first = h;
    Node *second = h;
    whlie(k --) first = first->next;
    while(first)
    {
        first = first->next;
        second = second->next;
    }
    return second;
}
```

#### 完整代码

```c++
#include <iostream>

using namespace std;

struct Node
{
    int data;
    Node *next;
    Node(int data)
    {
        this->data = data;
        this->next = NULL;
    }
};

class LinkList
{
public:
    Node *head;
    Node* CreateList();
    void PrintfList(Node *h);
    Node* reGetKthPointer(Node *h, int k);
};

Node* LinkList::CreateList()
{
    Node *p1 = new Node(1);
    Node *p2 = new Node(4);
    Node *p3 = new Node(2);
    Node *p4 = new Node(3);
    Node *p5 = new Node(5);
    Node *p6 = new Node(6);
    p1->next = p2;
    p2->next = p3;
    p3->next = p4;
    p4->next = p5;
    p5->next = p6;
    head = p1;
    return p1;
}

void LinkList::PrintfList(Node *h)
{
    Node *p = h;
    while(p)
    {
        cout << p->data << " ";
        p = p->next;
    }
}

Node* LinkList::reGetKthPointer(Node *h, int k)
{
    if(k == 0 || !h) return ;
    Node *first = h;
    Node *second = h;
    while(k --) first = first->next;
    while(first)
    {
        first = first->next;
        second = second->next;
    }
    return second;
}

int main()
{
    LinkList l;
    l.CreateList();
    l.PrintfList(l.head);
    cout << endl;
    cout << "倒数第三个结点的值为：";
    cout << l.reGetKthPointer(l.head, 3)->data;
}
```

