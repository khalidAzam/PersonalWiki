## Binary Trees and Binary Search Trees [Back](./../data_structure.md)

Sometimes, data will have a hierarchy, such as files in a file system, and for this kind of data, we will import trees to store them.

### Trees Defined

A tree is made up of a set of **nodes** connected by **edges**. An example of a tree is a company's organizational chart (*Figure 1*), in which each box is a **node**, and the lines between two boxes are called **edges**.

<p align="center">
    <img src="./an_organizational_chart.png" title="a company's organizational chart" alt="a company's organizational chart" />
</p>

<p align="center">
    <strong>Figure 1</strong> An organizational chart is a tree structure
</p>

The top node of a tree is called the **root** node. If a node is connected t other nodes below it, the preceding node is called the **parent** node, while the following one is called the **child** node. A ndoe without any child nodes is called a **leaf** node.

There is a special type of trees, called **binary trees**, restricting the number of child nodes to no more than two.

### Binary Trees and Binary Search Trees

Before talking about how to build a binary tree in JavaScript, there is something we should know.

The child nodes of a parent node are referred to as the **left** node and the **right** node.

A binary search tree is a binary tree in which data with lesser values are stored in left nodes while greater ones in right nodes. In another word, the value of the left node should be lesser than the parent node, and then lesser than the right node.

#### Nodes

```js
function Node(data, left, right) {
    this.data = data;
    this.left = left;
    this.right = right;
    
    this.show = show;
}

function show() {
    return this.data;
}
```

### Binary Search Trees

```js
function BST() {
    this.root = null;
    this.insert = insert;
    this.inOrder = inOrder;
}
```