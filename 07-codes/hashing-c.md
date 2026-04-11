# Hashing Implementation in C

This document provides a comprehensive implementation of hashing in C, including two collision resolution techniques: Chaining and Open Addressing.

## 1. Introduction to Hashing
Hashing is a technique used to uniquely identify a specific object from a group of similar objects. It is commonly used in data structures like hash tables.

## 2. Basic Structure of a Hash Table
A hash table consists of an array of buckets or slots, and a hash function that maps keys to a particular slot.

### 2.1 Structure Definition
```c
typedef struct HashNode {
    int key;
    int value;
    struct HashNode* next;
} HashNode;

typedef struct HashTable {
    int size;
    HashNode** table;
} HashTable;
```  

## 3. Chaining
Chaining is a collision resolution technique where each bucket of the hash table points to a linked list of entries that hash to the same index.

### 3.1 Hash Function
```c
int hash(int key, int size) {
    return key % size;
}
```

### 3.2 Insertion Function
```c
void insert(HashTable* ht, int key, int value) {
    int index = hash(key, ht->size);
    HashNode* newNode = (HashNode*)malloc(sizeof(HashNode));
    newNode->key = key;
    newNode->value = value;
    newNode->next = ht->table[index];
    ht->table[index] = newNode;
}
```

### 3.3 Searching Function
```c
int search(HashTable* ht, int key) {
    int index = hash(key, ht->size);
    HashNode* node = ht->table[index];
    while (node != NULL) {
        if (node->key == key) {
            return node->value;
        }
        node = node->next;
    }
    return -1; // Not found
}
```

## 4. Open Addressing
Open addressing is another collision resolution method where, if a collision occurs, the algorithm searches for the next available slot in the array.

### 4.1 Linear Probing
```c
void insertOpenAddressing(HashTable* ht, int key, int value) {
    int index = hash(key, ht->size);
    while (ht->table[index] != NULL) {
        index = (index + 1) % ht->size;
    }
    ht->table[index] = malloc(sizeof(HashNode));
    ht->table[index]->key = key;
    ht->table[index]->value = value;
}
```

### 4.2 Searching in Open Addressing
```c
int searchOpenAddressing(HashTable* ht, int key) {
    int index = hash(key, ht->size);
    while (ht->table[index] != NULL) {
        if (ht->table[index]->key == key) {
            return ht->table[index]->value;
        }
        index = (index + 1) % ht->size;
    }
    return -1; // Not found
}
```

## 5. Conclusion
This implementation provides basic data structures and functions needed to use hashing with two collision resolution strategies: chaining and open addressing. Adjustments can be made based on specific requirements or optimizations needed for a project.
