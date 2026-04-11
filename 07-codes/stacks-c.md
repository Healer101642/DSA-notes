# Stacks Implementation in C

## Introduction
Stacks are linear data structures that follow the Last In First Out (LIFO) principle. This means that the last element added to the stack is the first one to be removed. In this document, we will explore the implementation of stacks using both arrays and linked lists. We will also look at some applications of stacks such as balanced parentheses check, infix to postfix conversion, and undo/redo functionality.

---

## Array Implementation

### Structure Definition
```c
#define MAX 100

typedef struct {
    int top;
    int items[MAX];
} Stack;

void initStack(Stack* s) {
    s->top = -1;
}
```

### Stack Operations
- `isFull()`: Check if the stack is full.
- `isEmpty()`: Check if the stack is empty.
- `push()`: Add an item to the stack.
- `pop()`: Remove an item from the stack.
- `peek()`: Get the top item of the stack.

```c
int isFull(Stack* s) {
    return s->top == MAX - 1;
}

int isEmpty(Stack* s) {
    return s->top == -1;
}

void push(Stack* s, int item) {
    if (!isFull(s)) {
        s->items[++s->top] = item;
    }
}

int pop(Stack* s) {
    if (!isEmpty(s)) {
        return s->items[s->top--];
    }
    return -1; // Error: Stack is empty
}

int peek(Stack* s) {
    if (!isEmpty(s)) {
        return s->items[s->top];
    }
    return -1; // Error: Stack is empty
}
```

---

## Linked List Implementation

### Structure Definition
```c
typedef struct Node {
    int data;
    struct Node* next;
} Node;

typedef struct {
    Node* top;
} Stack;

void initStack(Stack* s) {
    s->top = NULL;
}
```

### Stack Operations
- `push()`: Add an item to the stack.
- `pop()`: Remove an item from the stack.
- `peek()`: Get the top item of the stack.

```c
void push(Stack* s, int item) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = item;
    newNode->next = s->top;
    s->top = newNode;
}

int pop(Stack* s) {
    if (s->top != NULL) {
        int poppedValue = s->top->data;
        Node* tempNode = s->top;
        s->top = s->top->next;
        free(tempNode);
        return poppedValue;
    }
    return -1; // Error: Stack is empty
}

int peek(Stack* s) {
    if (s->top != NULL) {
        return s->top->data;
    }
    return -1; // Error: Stack is empty
}
```

---

## Applications of Stacks

### 1. Balanced Parentheses
```c
int areParenthesesBalanced(char* expr) {
    Stack s;
    initStack(&s);
    for (int i = 0; expr[i]; i++) {
        if (expr[i] == '(') {
            push(&s, expr[i]);
        } else if (expr[i] == ')') {
            if (isEmpty(&s)) return 0;
            pop(&s);
        }
    }
    return isEmpty(&s);
}
```

### 2. Infix to Postfix Conversion
```c
int precedence(char ch) {
    if (ch == '+' || ch == '-')
        return 1;
    if (ch == '*' || ch == '/')
        return 2;
    return 0;
}

void infixToPostfix(char* infix, char* postfix) {
    Stack s;
    initStack(&s);
    int j = 0;
    for (int i = 0; infix[i]; i++) {
        if (isalnum(infix[i])) {
            postfix[j++] = infix[i];
        } else {
            while (!isEmpty(&s) && precedence(s.top) >= precedence(infix[i])) {
                postfix[j++] = pop(&s);
            }
            push(&s, infix[i]);
        }
    }
    while (!isEmpty(&s)) {
        postfix[j++] = pop(&s);
    }
    postfix[j] = '\0';
}
```

### 3. Undo/Redo Functionality
To implement Undo/Redo functionality, we can maintain two stacks. One stack for the actions already performed (Undo stack) and another for the Redo actions. Whenever an action is performed, it can be pushed onto the undo stack and popped from this stack for undoing, while the redo actions are managed in a similar fashion.

---

## Conclusion
Stacks are fundamental data structures that are used in various applications. Understanding their implementations can help in solving many complex problems in programming. In this document, we have covered the basic operations of stacks and a few common applications that demonstrate their utility in real-world scenarios.

