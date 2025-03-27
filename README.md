# Left-Leaning Red-Black Tree in C++

## Overview

This repository contains the implementation of a Left-Leaning Red-Black Tree (LLRB), a simpler and more efficient variant of a Red-Black Tree in C++. Red-Black Trees are a balanced search tree commonly used in various systems, such as the Linux kernel and standard libraries in several programming languages.

This project implements the key operations of a Left-Leaning Red-Black Tree, including insertion, deletion, and searching, all while maintaining the invariants of the tree, such as black balance and no consecutive red nodes.

## Table of Contents

1. [Introduction](#introduction)
2. [Left-Leaning Red-Black Tree](#left-leaning-red-black-tree)
3. [Data Structures](#data-structures)
4. [Compilation and Execution](#compilation-and-execution)
5. [Visualizing the tree using Graphviz](#visualizing-the-built-LLRB-tree)

## Introduction

The Left-Leaning Red-Black Tree is a self-balancing binary search tree with specific properties designed to simplify the red-black tree implementation. It ensures that:

- The root is black.
- No two consecutive red nodes exist.
- The path from the root to any leaf contains the same number of black nodes.
- If a black node has one red child, it must be the left child.

### Use Cases
LLRB trees are widely used in applications requiring ordered data structures, where efficient search, insertion, and deletion operations are critical. Common use cases include:

- Memory management in operating systems.
- Implementing associative containers in C++ STL.
- Used in various high-performance libraries and tools.

## Left-Leaning Red-Black Tree

### Properties

1. **Root is Black**: The root node must always be black.
2. **No Two Consecutive Red Nodes**: No two red nodes can appear consecutively in any path from the root to a leaf.
3. **Black Balance**: Every path from a node to its descendants must contain the same number of black nodes.
4. **Left-Leaning Property**: If a black node has a red child, the child must be on the left. This simplifies the implementation by reducing the number of balancing cases to consider.

### Structure

A `RBTree` is implemented with a `root` that is a unique pointer to an `RBNode`. Each node holds a `key`, a color (`RED` or `BLACK`), and pointers to its left and right children. The tree operations include inserting, deleting, and searching for elements while maintaining these invariants.

## Data Structures

```cpp
template<typename T>
struct RBTree {
    std::unique_ptr<RBNode<T>> root = nullptr;

    bool insert(const T&);
    void remove_max();
    void remove_min();
    void remove(const T&);

    const std::optional<T> leftmost_key();
    const std::optional<T> rightmost_key();

    bool contains(const T& t);
};

template<typename T>
struct RBNode {
    T key;
    color_t color = RED;
    std::unique_ptr<RBNode> left = nullptr;
    std::unique_ptr<RBNode> right = nullptr;

    RBNode(const T& t);
    bool is_leaf();
    void flip_color();

    static RBNode* rotate_right(std::unique_ptr<RBNode>&);
    static RBNode* rotate_left(std::unique_ptr<RBNode>&);
    static bool is_red(const std::unique_ptr<RBNode>&);

    static RBNode* move_red_right(std::unique_ptr<RBNode>&);
    static RBNode* move_red_left(std::unique_ptr<RBNode>&);

    static RBNode* remove_max(std::unique_ptr<RBNode>&);
    static RBNode* remove_min(std::unique_ptr<RBNode>&);
    static RBNode* remove(std::unique_ptr<RBNode>&, const T&);
    static RBNode* insert(std::unique_ptr<RBNode>&, const T&);
    static RBNode* fix_up(std::unique_ptr<RBNode>&);

    bool contains(const T& t);
};
```


## Compilation and Execution

To compile and run the project, follow the steps below:

```bash
mkdir build
cd build
cmake ..
make
```
The above step builds the executables. After this,

```bash
cd examples
./example
```
alternatively, you can test the built tree using CATCH2. From the build repository,
```bash
cd tests
./{test_executable_name}
```

## Visualizing the built LLRB tree
Within the examples repository run the following commands,

```bash
./graphviz-formatter > rbtree.dot
dot -Tpng rbtree.dot -o rbtree.png
```


![rbtree1](https://github.com/user-attachments/assets/0e76be9c-9440-430d-9ab5-cee1a7d9724d)


The above is the result of inserting Fibonacci numbers that are less than 1000 into the tree.


