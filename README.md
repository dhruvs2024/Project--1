# In-Memory Database System (C Implementation)

A lightweight, persistent In-Memory Key-Value Database Management System (DBMS) built from scratch in C. The system utilizes dynamic data structures for low-latency memory operations and provides file-handling capabilities to persist volatile memory states to storage.

## 🛠️ Overview & Architecture

This project implements a key-value storage engine operating entirely in volatile memory (RAM) to provide fast data access and manipulation. To overcome the volatile nature of in-memory storage, the system includes custom serialization and deserialization routines to load and save data directly to disk files.

### Key Data Structures & Concepts Used
* **Singly Linked Lists:** Serves as the primary dynamic storage structure for indexing and managing variable-length key-value pairs without pre-allocating fixed memory bounds.
* **Dynamic Memory Allocation (`malloc`, `free`):** Dynamically allocates nodes upon key creation (`set`) and deallocates heap memory upon record deletion (`delete`) to prevent memory leaks.
* **Structures (`struct`) & Type Definitions (`typedef`):** Encapsulates key-value records and node pointer metadata to maintain clean data abstraction.
* **File I/O Streams:** Manages state persistence by streaming in-memory data structures to and from persistent storage files.

## 💻 Commands & Functionality

The database supports a command-line interface with the following core operations:

| Command | Syntax / Action | Description |
| :--- | :--- | :--- |
| **`SET`** | `SET <key> <value>` | Inserts a new key-value pair into the database or updates an existing entry. |
| **`GET`** | `GET <key>` | Traverses the linked list to retrieve and display the value associated with the specified key. |
| **`DELETE`** | `DELETE <key>` | Searches for the key, updates adjacent pointers, and frees heap memory allocated to the node. |
| **`EXISTS`** | `EXISTS <key>` | Checks if a record with the specified key currently resides in memory (returns boolean status). |
| **`SAVE`** | `SAVE <filename>` | Serializes all active in-memory nodes and writes the dataset to a persistent disk file. |
| **`LOAD`** | `LOAD <filename>` | Parses a specified file from storage, reconstructs the node graph, and restores it into RAM. |


## 🎯 Engineering Challenges & Key Learnings

### 1. Pointer Manipulation & Linked List Logic
* **Challenge:** Traversing, inserting, and deleting nodes in a singly linked list was initially a complex concept, leading to pointer tracking errors and dangling memory references during deletion operations.
* **Solution:** Standardized pointer updates by explicitly updating `next` pointers prior to freeing memory blocks and implementing systematic null-pointer checks during head/tail traversals.

### 2. Buffer Overflow & Input Sanitation (`gets()` vs. `scanf()`)
* **Challenge:** Initial iterations used the unsafe `gets()` function for string input. Entering strings that exceeded the allocated buffer size caused unsafe memory writes, leading to random **segmentation faults** due to stack corruption.
* **Solution:** Deprecated `gets()` and replaced it with width-limited string reading techniques (e.g., `scanf("%8s", ...)` and safer alternatives like `fgets()`). This enforces strict boundary checking, guaranteeing that user input never writes past the allocated memory buffer.

## 🚀 Future Enhancements
- [ ] Implement a Hash Map indexing layer on top of linked lists to improve lookups from O(N) time complexity to average O(1).
- [ ] Add support for custom data types beyond standard string key-value pairs.
- [ ] Support transactional operations (`BEGIN`, `COMMIT`, `ROLLBACK`).
