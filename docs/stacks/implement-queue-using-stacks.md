# 232. Implement Queue using Stacks

## Problem Statement
Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (`push`, `peek`, `pop`, and `empty`).

Implement the `MyQueue` class:

- `void push(int x)` Pushes element x to the back of the queue.

- `int pop()` Removes the element from the front of the queue and returns it.

- `int peek()` Returns the element at the front of the queue.

- `boolean empty()` Returns `true` if the queue is empty, `false` otherwise.

Notes:

- You must use only standard operations of a stack, which means only `push to top`, `peek/pop from top`, `size`, and `is empty` operations are valid.

- Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.

---

## Approach: Two Stacks

The approach uses one stack (`inputStack`) for pushing new elements and another stack (`outputStack`) for popping and peeking elements.

### `push(int x)`:

- Simply push the element onto the `inputStack`.

### `pop()`:

- If `outputStack` is empty, transfer all elements from `inputStack` to `outputStack`. This reverses the order of elements, so the top of `outputStack` is the front of the queue.

- Pop the top element of `outputStack`.

### `peek()`:

- Similar to `pop()`, but instead of removing the element, return the top of `outputStack`.

### `empty()`:

- The queue is empty only if both stacks are empty.

---

## Code (C++)

```cpp
class MyQueue {
    private:
        stack<int> inputStack; 
        stack<int> outputStack;

    public:
        MyQueue() {
    
        }
    
        void push(int x) {
            inputStack.push(x);
        }
        
        int pop() {
            if (outputStack.empty()) {
    
                while (!inputStack.empty()) {
                    outputStack.push(inputStack.top());
                    inputStack.pop();
                }
            }
            int front = outputStack.top();
            outputStack.pop();
            return front;
        }
    
        int peek() {
            if (outputStack.empty()) {
    
                while (!inputStack.empty()) {
                    outputStack.push(inputStack.top());
                    inputStack.pop();
                }
            }
            return outputStack.top();
        }
        
        bool empty() {
            return inputStack.empty() && outputStack.empty();
    }
};


/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
```
## Complexity
- Time Complexity:
   - Push (𝑂(1)) — Always inserts elements into `inputStack`.

   - Pop (Amortized 𝑂(1)) — Moves elements from `inputStack` to `outputStack` when `outputStack` is empty, then pops.

   - Peek (Amortized 𝑂(1)) — Similar to `pop()`, but only returns the front element without removing that element.

   - Empty (𝑂(1)) — Checks if both stacks are empty.  
   
- Space Complexity: 𝑂(𝑛) — Where `n` is the number of elements in the queue (storage across the two stacks).

## Conclusion
This implementation efficiently simulates a FIFO queue using two stacks and supports all the required operations.