# In-Memory Key-Value Store (C)

A lightweight key-value database written in C. It handles fast in-memory operations using dynamic linked lists and includes simple file serialization to save and restore database state from disk.

## Overview & Implementation

The core database runs entirely in RAM to keep read/write operations low-latency. To handle persistence across restarts, active key-value pairs can be dumped to disk and reloaded into memory at boot.

### Core Concepts

* **Singly Linked Lists:** Used as the primary data structure for dynamic node allocation, allowing variable-length entries without fixing storage bounds beforehand.
* **Manual Memory Management:** Dynamic allocation using `malloc()` on insert (`SET`) and explicit cleanup using `free()` on record removal (`DELETE`) to prevent memory leaks.
* **File I/O & Serialization:** Streams the linked list to disk during a `SAVE` command and rebuilds the node structure during a `LOAD` operation.

## Commands

The CLI supports six core commands:

| Command | Usage | Action |
| :--- | :--- | :--- |
| **`SET`** | `SET <key> <value>` | Inserts a new key-value pair or overwrites an existing key. |
| **`GET`** | `GET <key>` | Searches the list and prints the associated value. |
| **`DELETE`** | `DELETE <key>` | Unlinks the node from the list and frees its memory. |
| **`EXISTS`** | `EXISTS <key>` | Returns whether the key currently exists in memory. |
| **`SAVE`** | `SAVE <filename>` | Serializes all active nodes to a file on disk. |
| **`LOAD`** | `LOAD <filename>` | Reads a storage file and reconstructs the list in memory. |

## Technical Challenges & Takeaways

* **Pointer Safety & Memory Leaks:** Deleting nodes required careful pointer re-linking before calling `free()`. Missing edge cases (like removing the head node or clearing an empty list) initially caused segmentation faults, which were fixed by adding strict null checks during traversal.
* **Buffer Overflow Protection:** Swapped out unsafe input functions like `gets()` for boundary-checked string parsing (`fgets()` and width-limited `scanf()`) to prevent user inputs from overflowing buffer limits and corrupting stack memory.

## Roadmap

- [ ] Add a Hash Map layer over the linked list to bring lookup times down from O(N) to O(1).
- [ ] Support complex data types beyond basic string pairs.
- [ ] Add basic transaction support (`BEGIN`, `COMMIT`, `ROLLBACK`).
