 Overview
This project demonstrates the implementation of a **Circular Queue using an array** in C.

A Circular Queue follows the **FIFO (First In, First Out)** principle, but unlike a linear queue:
- The last position connects back to the first position.
- It efficiently utilizes empty spaces created after dequeue operations.
- Uses modulo (`%`) operation for circular movement.

---
 Source Code

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 5

int queue[MAX];
int front = -1;
int rear = -1;

// Enqueue operation
void enqueue(int value) {
    if ((rear + 1) % MAX == front) {
        printf("Queue Overflow! Cannot insert %d\n", value);
        return;
    }

    if (front == -1)
        front = 0;

    rear = (rear + 1) % MAX;
    queue[rear] = value;
    printf("%d inserted into queue\n", value);
}

// Dequeue operation
void dequeue() {
    if (front == -1) {
        printf("Queue Underflow! Queue is empty\n");
        return;
    }

    printf("%d removed from queue\n", queue[front]);

    if (front == rear) {
        front = rear = -1;
    } else {
        front = (front + 1) % MAX;
    }
}

// Display queue
void display() {
    if (front == -1) {
        printf("Queue is empty\n");
        return;
    }

    printf("Queue elements are:\n");
    int i = front;
    while (1) {
        printf("%d ", queue[i]);
        if (i == rear)
            break;
        i = (i + 1) % MAX;
    }
    printf("\n");
}

int main() {
    enqueue(10);
    enqueue(20);
    enqueue(30);
    enqueue(40);
    enqueue(50);

    display();

    dequeue();
    dequeue();

    enqueue(60);
    enqueue(70);

    display();

    return 0;
}
```

---
 Explanation

 Circular Queue Logic
- `#define MAX 5` → Maximum size of queue.
- `(rear + 1) % MAX == front` → Condition for **Overflow**.
- `(rear + 1) % MAX` → Moves rear circularly.
- `(front + 1) % MAX` → Moves front circularly.

 Enqueue Operation
- Checks overflow condition.
- Updates `rear` using modulo.
- Inserts element.

 Dequeue Operation
- Checks underflow condition.
- Removes element.
- Updates `front` circularly.
- Resets queue when empty.

 Display Operation
- Traverses from `front` to `rear`.
- Uses modulo for circular traversal.

---

 Sample Output

```
10 inserted into queue
20 inserted into queue
30 inserted into queue
40 inserted into queue
50 inserted into queue
Queue elements are:
10 20 30 40 50
10 removed from queue
20 removed from queue
60 inserted into queue
70 inserted into queue
Queue elements are:
30 40 50 60 70
```

---

 Time Complexity

- Enqueue: **O(1)**
- Dequeue: **O(1)**
- Display: **O(n)**

---

 Advantages Over Linear Queue

- Efficient memory utilization
- No wasted space
- Circular movement using modulo operator

---
 How to Compile and Run

Compile:
```
gcc circular_queue.c -o cqueue
```

 Run:
```
./cqueue
```

---

 Concepts Used
- Arrays in C
- Circular Queue Data Structure
- FIFO Principle
- Modulo Operator
- Overflow & Underflow Handling
