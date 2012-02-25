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

Binary Trees
------------

In a _binary tree_, each node has no more than two children, commonly referred to _left_ and _right_.
In Ruby, one way this could look is

    class Node
      attr_accessor :key, :left, :right

      def initialize(value, left, right)
        @key, @left, @right = key, left, right
      end

      # We are assuming that this is the root.
      def find(key)
        return @key if key == @key
        (@key < key) ? right.find(key) : left.find(key)
      end
    end

Don't you just love Ruby.

The find method is $$O(log(n))$$