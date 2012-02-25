<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/2.0-beta/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

Searching and Trees
===================

The text Algorithms in a Nutshell has a great review of the basic algorithms for search. As it says in the text, given a collection C  of elements, there are really 3 fundamental queries we might ask. (page 105)

* Existence: Does _C_ contain a target element _t_?
* Retreival: Return the eloement in _C_ that matches the target element _t_
* Associative lookup: Return information associated in collection _C_ with the target key element _k_

Sequential Search
-----------------

As the name implies this is the simplest search method. Given a collection of items, visit each of them in order until the one you are looking for is found. Best used when the list is very short.

<table>
  <tr>
    <td>Best Case</td>
    <td>Average Case</td>
    <td>Worse Case</td>
  </tr>
  <tr>
    <td>O(1)</td>
    <td>O(n)</td>
    <td>O(n)</td>
  </tr>
</table>

Binary Search
-------------

The elements involved in the query should be sorted first (see sorting!). Divides the collection in half until the item is found.

<table>
  <tr>
    <td>Best Case</td>
    <td>Average Case</td>
    <td>Worse Case</td>
  </tr>
  <tr>
    <td>O(1)</td>
    <td>O(log n)</td>
    <td>O(log n)</td>
  </tr>
</table>

Here is a sample implementation 

    # binary search
    def has_item? collection, key
      low  = 0
      high = collection.size - 1

      while low <= high do
        i = (low + high)/2
        item  = collection[i]
        return true if key == item

        high = i - 1 if key < item
        low  = i + 1 if key > item
      end

      false
    end

Hash-based Search
-----------------

For searching large collections that are not necessarily ordered, a Hash is used. In high level languages like Ruby or Scala (or even Java), the Hash or HashMap is so deeply embedded in the day to day use of the language that we hardly ever think about the underlying data structure.

<table>
  <tr>
    <td>Best Case</td>
    <td>Average Case</td>
    <td>Worse Case</td>
  </tr>
  <tr>
    <td>O(1)</td>
    <td>O(1)</td>
    <td>O(log n)</td>
  </tr>
</table>

Binary Search Trees
-------------------

Reasons to use a binary tree

* Data set in dynamic or of unknown size
* Application requires traversing the data in ascending or decending order
* Not to be confused with a B-Tree, which is a generalization of a binary search tree in that a node can have more than two children.

In a _binary tree_, each node has no more than two children, commonly referred to _left_ and _right_.
In Ruby, one way this could look is

    class Node
      attr_accessor :key, :left, :right

      def initialize(value, left, right)
        @key, @left, @right = key, left, right
      end

      def find(key)
        return @key if key == @key
        (@key < key) ? right.find(key) : left.find(key)
      end
    end

Don't you just love Ruby. 
Accessing a node is typically done recursively. In the above example, calling #find on the parent node, subsequently calls #find on the children. This is not recursion, though the implementation would be if it was just a function and not an object.

The find method is O(log(n))

In most applications we need to balance the tree for efficient lookup. A ree with approximatel the same number of nodes on each side is called a _balanced tree_. Of the methods to gaurantee that a tree is balanced, a red-black tree is the most common.

**Red-black trees**

Features

* Every node is labeled either red or black
* The root is black
* Every leaf node contains a null value and is black
* All red nodes have two children
* Every simple path from a node to one of its decendent lead nodes contains the same number of black nodes

Four steps in inserting a new key into a red-black tree

1. Insert new Leaf node
2. Update colors of ancestor nodes
3. Rotate right to maintain red-black tree property
4. Update colors of affected nodes

Searches
========

Breadth-First Search
--------------------

Start with the root, move left to right across the second level, then move left to right across the third level, and so on. The time to find a node is _O(n)_, so this type of search is best avoided for large trees.

Traversals
----------

* **Preorder** traversal of a node performs the operation first on the node itself, then on its left decendants, and finally on its right decendants. _O(n)_ complexity
* **Inorder** traversal performs the operation first on the node's left decendants, then on the node itself, and finally on its right decendents. 
* **Postorder** traversal performs the operation first on the node's left decendants, then on its right decendents, and finally on the node itself.

Common Binary Tree Problems
===========================

Preorder Traversal
------------------
Informally, a preorder traversal involves walking around the tree in a counterclockwise mannert starting at the root, sticking close to the edges , and printing out the nodes as you encounter them. Perform a preorder traversal of a binary search tree, printing the value of each node.

    class Node
      def preorder_traversal
        puts key
        left.preorder_traveral
        right.preorder_traveral
      end
    end

Preorder Traversal, No Recusion
-------------------------------
Perform a preorder traversal of a binary search tree, printing the value of each node, but this time you may _not_ use recursion.

Lowest Common Ancestor
----------------------
Given the value of two nodes in a binary search tree, find the lowest (nearest) common ancestor. You may assume that both values already exist in the tree.

Type-ahead or Autocomplete
--------------------------
Implement an autocomplete that suggests words as the user types letters.

One way to do this is with a _trie_. A trie, or prefix tree, is an ordered tree data structure that is used to store an associative array where the keys are usually strings. This is [a trie](http://en.wikipedia.org/wiki/Trie).

    class Trie
      def initialize
        @root = {}
      end
      
      def build word
        node = @root    

        word.each_char {|char|
          prev_node = node
          node      = node[char]
          if node.nil?
            prev_node[char] = {}
            node = prev_node[char]
          end
        }
      end
     
      def find(str) 
        node = @root
        str.each_char { |char|
          node = node[char]
          return false if node.nil?
        }
        return true 
      end
    end