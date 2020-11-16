## 剑指 Offer 09. 用两个栈实现队列

我们需要维护两个栈s1和s2，使用s1接收新添加进来的元素，使用s2辅助出队操作。

- 对于构造函数`CQueue()`，当然是要把s1和s2全部清空，扫清一切障碍~
- 对于`appendTail(int value)`函数，直接将元素`push`到s1中；
- 对于`deleteHead()`函数，应该先判断s2是否为空
	1. 如果s2为空，则依次将s1中元素出栈并压入s2中，完成后再将s2的栈顶元素`pop`出来，就满足了先入队先出队的原则；
	2. 如果s2不为空，则直接`pop`出s2的栈顶元素；
	3. 如果经过了**1.** 的一顿操作之后，s2仍为空，则说明这就是个空队列，直接返回-1即可~

#### 代码
```cpp
class CQueue {
private:
    stack<int> s1, s2;
public:
    CQueue() {
        while(!s1.empty())
            s1.pop();
        while(!s2.empty())
            s2.pop();
    }
    
    void appendTail(int value) {
        s1.push(value);
    }
    
    int deleteHead() {
        if(s2.empty())
        {
            while(!s1.empty())
            {
                s2.push(s1.top());
                s1.pop();
            }
        }
        if(!s2.empty())
        {
            int res = s2.top();
            s2.pop();
            return res;
        }
        else {
            return -1;
        }
    }
};

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue* obj = new CQueue();
 * obj->appendTail(value);
 * int param_2 = obj->deleteHead();
 */
```
---


**[原题传送门](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)**
