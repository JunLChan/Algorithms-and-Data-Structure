### 给出一单链表头指针pHead和一节点指针pToBeDeleted，O(1)时间复杂度删除节点pToBeDeleted: delete

参考LeetCode

#### 思路

将要被删除的节点伪装成下一个节点，然后把下一个节点删除。

特判：

1.如果删除的是最后一个节点，且链表中只有一个节点。直接把节点置为NULL即可；

2.如果不是第1种情况，则需先找到倒数第二个节点。使倒数第二个节点指向NULL即可。

#### 图例

![avatar](C:\Users\S1-02\Desktop\LeetCode\删除链表节点.png)

#### C++代码实现

```c++
void deleteNode(Node *h, Node *toBeDelete)
{
	if(!toBeDelete) return ;
    if(toBeDelete->next)
    {
        toBeDelete->data = toBeDelete->next->data;
        toBeDelete->next = toBeDelete->next->next;
    }
    else
    {
        if(h == toBeDelete) h = NULL;
        else
        {
            Node *n = h;
            while(n->next != toBeDelete) n = n->next;
            n->next = NULL;
        }
    }
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
    void PrintfList(Node *h);
    void deleteNode(Node *h, Node *toBeDelete);

};

void LinkList::PrintfList(Node *h)
{
    Node *p = h;
    while(p)
    {
        cout << p->data << " ";
        p = p->next;
    }
    cout << endl;
}

void LinkList::deleteNode(Node *h, Node *toBeDelete)
{
    if(!toBeDelete) return ;
    if(toBeDelete->next)
    {
       toBeDelete->data = toBeDelete->next->data;
       toBeDelete->next = toBeDelete->next->next;
    }
    else
    {
        if(h == toBeDelete) h = NULL;
        else
        {
            Node *n = h;
            while(n->next != toBeDelete) n = n->next;
            n->next = NULL;
        }
    }

}

int main()
{
    Node *h = new Node(4);
    Node *q1 = new Node(6);
    Node *q2 = new Node(2);
    Node *q3 = new Node(7);
    Node *q4 = new Node(3);
    Node *q5 = new Node(4);
    Node *q6 = new Node(5);
    h->next = q1;
    q1->next = q2;
    q2->next = q3;
    q3->next = q4;
    q4->next = q5;
    q5->next = q6;

    LinkList l;
    cout << "原链表为：";
    l.PrintfList(h);
    l.deleteNode(h, q4);
    cout << "删除第五个节点后的链表为：";
    l.PrintfList(h);
}
```