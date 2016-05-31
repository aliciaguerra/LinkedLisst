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
               If the array is full, you cannot add more elements because arrays have a fixed size. Linked lists do not.
               
Another drawback of arrays is that if you delete the element from the middle and want no holes in the array (e.g. 1,2,4,null) instead of (1,2,null,4)), you will need to shift everything after the deleted element down in O(n) time. If you're trying to
add an element somewhere other than the very end of the array, you will need to shift some elements toward the end by one
(also O(n) time) to make room for the new element, and if you're writing an application that needs to perform well and needs
those operations often, you need to consider those linked lists instead. This should help you understand linked lists.

[*]
This is an empty linked lists look like. This * is an empty node (each element in the linked list is called a node) which
has its next-node reference set to the first node in the list. Since, we don't have a first node, the next node is a 
null-pointer. 

[*]->[1]->[2]->[3]
This is a linked list with three nodes. Each node points to the next node in the chain. As mentioned above, * is an empty
node with a reference to the first node. [3] is the last node in the chain with next==null

[*]->[1]->[3]
Here we have deleted node [2], so node [1] (previously pointing to node 2) now points to [3]. If we didn't change the reference, node [3] and any nodes behind it would have no references from your program and get lost. If this happens and
you're using C/C++, you have a memory leak. If you're using Java, the nodes would automatically get garbage collected. 
Either way, make sure you update the references. 

[*] -> [1] -> [2] -> [3]
For whatever reason, we've decided to add node 2 back between nodes 1 and 3. the references from 1 set to 2 and the reference
from 2 is set to the old reference of 1, which is 3.

My code of the linkedlist class is as follows. It is a commented oversimplification of the LinkedList class that's already
built into Java. Please note that indexes start at 1 and not 0 (like in the Java linkedlist class), so the first element
in the list has index 1.

                            //Node constructor
                            public Node(Object _data)
                            {
                            next = null;
                            data = _data;
                            }
                            
                            //another node constructor if we want to
                            //specify the node to point to
                            public Node(Object _data, Node _next){
                            next = _next;
                            data = _data;
                            }
                            
                            //these methods should be self-explantory
                            public Object getData() {
                            return data;
                            }
                            
                            public void setData(Object _data) {
                            data = _data;
                            }
                            
                            public Node getNext() {
                            return next;
                            }

                            public void setNext() {
                            return next;
                            }
                            
                            }
                            }
  
