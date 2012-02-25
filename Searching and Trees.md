<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/2.0-beta/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

Searching and Trees
===================

The text Algorithms in a Nutshell has a great review of the basic algorithms for search. As it says in the text, given a collection C  of elements, there are really 3 fundamental queries we might ask. (page 105)

* Existence: Does _C_ contain a target element _t_?
* Retreival: Return the eloement in _C_ that matches the target element _t_
* Associative lookup: Return information associated in collection _C_ with the target key element _k_

Sequential Search
-----------------

Binary Search
-------------

Hash-based Search
-----------------

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