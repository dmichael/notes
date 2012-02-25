In an effort to improve my interview questions and to review my own knowledge of the basics, I have started studying basic data structures and algorithms. I have actually done this every few years or so just keep it fresh. Since I use lists and their variants everyday, I thought this might be a good place to start the review.

The interesting thing about linked lists, is that for 99% of programmers, the last time they saw this structure was during study or in preparation for an interview.
I asked a colleague the last time he saw this structure in its primitive form and he said when he worked in C and he had to do everything himself. Thankfully, there are all sorts of data structures whose implementations we take for granted these days. Imagine if every you wanted to make breakfast you had to gather eggs from the chicken, harvest wheat and leven up some bread, milk the cow and churn some butter, grow, roast, and grind the beans... you get the idea.

Let's make breakfast

Linked Lists
============

Singly Linked Lists
-------------------

* List can only be traversed in the forward direction

Here is an example in C

	typedef struct IntElement {
	  struct IntElement *next;
	  int data;
	} IntElement;

<br>

And in our favorite language Java (sike)

	public class ListElement {
	  ListElement next;
	  Object data;

	  public ListElement(Object data){
	    this.data = data;
	  }
	}

Doubly Linked Lists
-------------------

* Additional link to the "previous" element makes it possible for forward and reverse traversal
* First element has a null reference in "previous"

Circularly Linked Lists
-----------------------
* No head or tail elements, but a continuous chain of linkages


Linked Lists Basic Operations
=============================

Tracking the Head
-----------------

* The head element of a singly linked list must always be tracked, otherwise the list will be lost in memory.
* When updating a list, the caller must be made aware of the new head. Though it is conceiveable to wrap up this whole enterprise into a class that does just this. Let's call it LinkedList or hell, List.

Here is the Java

	public ListElement insertInFront( ListElement list, Object data){
	  ListElement l = new ListElement(data);
	  l.next = list;
	  return l; // the new head!
	}

Traversing
----------
* Operations on any but the first element of a linked list require traversal of the list.
* In traversal, you must always check for the end of the list (or suffer a null pointer exception)

This is easy in most any language (but here is the Java)  

	public ListElement find(ListElement head, Object data){
	  while(head.data != data && head != null){
	    head = list.next;
	  }
	  return head
	}


Inserting and Deleting Elements
-------------------------------
* Any insertion or deletion of elements in the middle of the list requires modification of the previous elements link.
* In C/C++ deletion or insertion of an element always require at least two pointer variables.

Below is the C implementation for deleting an element from a linked list. If we passed in just a pointer to the head as the first argument (*head, rather than **head), then reassignment will only be to the local copy of the head pointer. So we need a pointer to that pointer! I am so glad that I work so infrequently in C that I forget this all the time.

Here is the C

	bool deleteElement( IntElement **head, IntElement *deleteMe){
	  IntElement *elem = *head;

	  // special case for head
	  if (deleteMe == *head){
	    *head = elem->next;
	    delete deleteMe;
	    return true;
	  }

	  while(elem){
	    if(elem->next == deleteMe){
	      elem->next = deleteMe->next;
	      delete deleteMe;
	      return true;
	    }
	    elem = elem->next;
	  }
	  // not found
	  return false;
	}



Common Linked List Problems
===========================

Some things to remember
-----------------------

* C allows only call by value, not call by reference; however, if a called function is to change the value of an object defined in the calling function, it can be passed a value which is a pointer to the object. The called function can then dereference the pointer to access the object indirectly.

Stack Implementation
--------------------

Discuss the stack data structure, Implement a stack in C using either a linked list or a dynamic array, and justify your decision. Design the interface to the stack to be complete consistent and easy to use.

* A stack is a last-in-first-out (LIFO) data structure
* Elements are always removed in the reverse order they were added.
* Adding and removing elements are conventionally _push_ and _pop_, respectively.
* Main advantange of dynamic arrays over linked lists is that arrays offer random access to array elements. However, operations on a stack always work at the ends of the data structure, so there is little need for random access.


Maintain Linked List Tail Pointer
---------------------------------

head and tail are global pointers to the first and last element respectively, of a singly linked list of integers. Implement C functions for the following prototypes:

  bool remove (Element *e)
  bool insertAfter(Element *e, int data)

N-th to last element of the linked list
---------------------------------------

Given a singly-linked list, devise a time and space effecient algorithm to find the nth-to-last element of the list. Define nth to last such that when n=0, the last element of the list is returned.
