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
      attr_accessor :left, :right, :value

      def initialize(left, right, value)
        @left, @right, @value = left, right, value
      end
    end

Don't you just love Ruby.