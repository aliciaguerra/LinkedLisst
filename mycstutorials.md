# Linked Lists
Linked lists are a very common way of storing arrays of data. The major benefit of linked lists is that you do not specify
a fixed size for the list. The more elements you add to the chain, the bigger the chain gets. 

There is more than one type of a linked list, although for the purpose of this tutorial, we'll stick to singly linked lists
(the simplest one). If for example you want a doubly linked list instead, very few simple modifications will give you
what you're looking for. Many data structures (i.e. stacks, queues, binary trees, etc.) are often implemented using the
concept of lists.

#Singly-Linked List
[*] -> [A] -> [B] -> [C] -> [NULL]

#Circular Linked List
Circular linked lists have a reference to one node which is the tail node and all the nodes are linked together in one direction forming a circle. The benefit of using circular lists is that appending to the end can be done pretty quickly.

              Tail
               V               
[A] -> [B] -> [C] 
^             |
|_____________] 

#Doubly Linked List
Every node stores a reference to its previous node as well as its next. This is good if you need to move back by a few nodes 
and don't want to run from the beginning of the list.
  <  <   <   <
*  A   B   C   --> Null
  >  >   >   >

Here's a diagram to help you realize the main disadvantages of arrays but not linked lists (there are certain advantages 
of using arrays over linked lists, but are not covered in this article):

  [][][][]   create an empty integer array
  [1][2][3][]  fill it partially with some data. the array component without a number indicates allocated but unused space.
               this is space used for something better.
  [1][2][3][4] add another element. we now have a full array to which we cannot add any more elements. We can 
               delete or replace, but we cannot add.
               If the array is full, you cannot add more elements because 
  
