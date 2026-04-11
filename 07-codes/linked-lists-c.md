# Linked Lists in C

## Introduction
Linked lists are a fundamental data structure that consist of nodes, each containing data and a pointer to the next node. They provide a flexible way to store data because they can easily grow and shrink in size.

## Types of Linked Lists
1. **Singly Linked List**  
   Each node contains data and a pointer to the next node.

   ### Implementation:
   ```c
   #include <stdio.h>
   #include <stdlib.h>

   struct Node {
       int data;
       struct Node* next;
   };

   // Function to create a new node
   struct Node* newNode(int data) {
       struct Node* node = (struct Node*)malloc(sizeof(struct Node));
       node->data = data;
       node->next = NULL;
       return node;
   }

   // Function to print the linked list
   void printList(struct Node* n) {
       while (n != NULL) {
           printf("%d -> ", n->data);
           n = n->next;
       }
       printf("NULL\n");
   }

   int main() {
       struct Node* head = newNode(1);
       head->next = newNode(2);
       head->next->next = newNode(3);
       printList(head);
       return 0;
   }
   ```

   ### Time Complexity:
   - Access: O(n)
   - Search: O(n)
   - Insertion: O(1) (at the beginning)
   - Deletion: O(1) (if the node to be deleted is known)

2. **Doubly Linked List**  
   Each node contains data, a pointer to the next node, and a pointer to the previous node.

   ### Implementation:
   ```c
   #include <stdio.h>
   #include <stdlib.h>

   struct Node {
       int data;
       struct Node* next;
       struct Node* prev;
   };

   struct Node* newNode(int data) {
       struct Node* node = (struct Node*)malloc(sizeof(struct Node));
       node->data = data;
       node->next = NULL;
       node->prev = NULL;
       return node;
   }

   void printList(struct Node* node) {
       struct Node* last;
       printf("Traversal in forward direction: ");
       while (node != NULL) {
           printf("%d <-> ", node->data);
           last = node;
           node = node->next;
       }
       printf("NULL\n");
   }

   int main() {
       struct Node* head = newNode(1);
       struct Node* second = newNode(2);
       struct Node* third = newNode(3);

       head->next = second;
       second->prev = head;
       second->next = third;
       third->prev = second;

       printList(head);
       return 0;
   }
   ```

   ### Time Complexity:
   - Access: O(n)
   - Search: O(n)
   - Insertion: O(1) (at the beginning)
   - Deletion: O(1) (if the node to be deleted is known)

3. **Circular Linked List**  
   The last node points back to the first node.

   ### Implementation:
   ```c
   #include <stdio.h>
   #include <stdlib.h>

   struct Node {
       int data;
       struct Node* next;
   };

   struct Node* newNode(int data) {
       struct Node* node = (struct Node*)malloc(sizeof(struct Node));
       node->data = data;
       node->next = NULL;
       return node;
   }

   void printList(struct Node* head) {
       if (head == NULL) return;
       struct Node* temp = head;
       do {
           printf("%d -> ", temp->data);
           temp = temp->next;
       } while (temp != head);
       printf("(back to head)\n");
   }

   int main() {
       struct Node* head = newNode(1);
       struct Node* second = newNode(2);
       struct Node* third = newNode(3);

       head->next = second;
       second->next = third;
       third->next = head;  // Making it circular

       printList(head);
       return 0;
   }
   ```

   ### Time Complexity:
   - Access: O(n)
   - Search: O(n)
   - Insertion: O(1) (at the beginning)
   - Deletion: O(1) (if the node to be deleted is known)

## Practice Problems
1. Implement a function to reverse a singly linked list.
2. Merge two sorted linked lists into one sorted linked list.
3. Detect a loop in a linked list.
4. Find the middle element of a linked list.
5. Remove the nth node from the end of a linked list.

## Conclusion
Linked lists are essential for understanding more complex data structures and algorithms. Mastering them is key to coding interviews and computer science fundamentals.  
