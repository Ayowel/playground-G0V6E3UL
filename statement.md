# Welcome!

This C++ code should only be used to learn/experiment with classes and their implementations. Use the std::stack class implementation for actual program implementation.

```C
#include <cassert>
#include <iostream>

/* quick & dirty implementation of a stack with nested cells */
/* C-style implementation with use of c++ classes */

template <typename T>
class Stack {
    private:
        class StackCell {
            public:
                T data;
                
                Stack<T>::StackCell *next;
                
                StackCell(const T& data, Stack<T>::StackCell* next)
                : data(data), next(next)
                { }
        };
        
        Stack<T>::StackCell *content;

    public:
        Stack(const T& data)
        : content(new Stack<T>::StackCell(data, nullptr))
        { }
        
        Stack(void)
        : content(nullptr)
        { }

        void append(const T& data) // Could return `this` to allow chaining
        {
            this->content = new Stack<T>::StackCell(data, this->content);
        }
        
        T get(void) {
            Stack<T>::StackCell* retPtr = this->content;
            assert(retPtr != nullptr);
            T retVal = retPtr->data;
            this->content = this->content->next;
            delete retPtr;
            return retVal;
        }
        
        T& peek(void) const
        {
            assert(this->content != nullptr);
            return this->content->data;
        }
        
        const bool hasNext(void) const
        {
            return this->content != nullptr;
        }
        
        ~Stack()
        {
            Stack<T>::StackCell* ptr = this->content;
            while(ptr != nullptr)
            {
                const Stack::StackCell* tmp = ptr;
                ptr = ptr->next;
                delete tmp;
            }
        }
};


int main()
{
    std::cout << "Hello, World!" << std::endl;
    Stack<int> s;
    std::cout << s.hasNext() << " -> ";
    s.append(3);
    s.append(5);
    s.append(7);
    std::cout << s.hasNext() << std::endl;
    std::cout << s.peek() << " " << s.get() << " " << s.get() << " " << s.get() << " : " << s.hasNext() << std::endl;
    
    return 0;
}
```

# Advanced usage

If you want a more complex example (external libraries, viewers...), use the [Advanced C++ template](https://tech.io/select-repo/598)
