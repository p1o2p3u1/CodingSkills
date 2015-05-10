## 155	Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.

## Solution
```C++
class MinStack {
private:
    stack<int> s;
    stack<int> m;
public:
    void push(int x) {
        s.push(x);
        if(m.empty() || x <= m.top())
            m.push(x);
    }

    void pop() {
        int d = s.top(); s.pop();
        if(!m.empty() && d == m.top()) m.pop();
    }

    int top() {
        return s.top();
    }

    int getMin() {
        return m.top();
    }
};
```