Our disadvantage of using arrays to store data is that the arrays are static structures and therefore cannot be easily reduced 
or extended to fit the data set. Arrays are also expensive to maintain new insertions and deletions. In this chapter we 
consider another data structure called Linked Lists that addresses some of the limitations of arrays.

A linked list is a linear data structure where each element is a separate object.

Each element is a node comprising of two items - the data and the reference to the next node. The last node has a reference
to null. The entry point to a linked list is the head of a list. It should be noted that head is not a separate node, but
the reference to the first node. If the linked list is empty then the head is a null reference.

A linked list is a dynamic data structure. The number of nodes in th list is not fixed and can grow or shrink on demand. 
Any application which has to deal with an unknowon number of objects will need to use a linked list.

One disadvantage of a linked list against an array is that it does not allow direct access to individual elements. If you want
to access a particular item, you have to start at the head and follow the references until you get to them. 

Another disadvantage is that a linked list uses more memory compared to an array - we extra 4 bytes (on 32-bit CPU) to store a 
reference to the next node. 

A doubly linked list has two references, one to the next node, another to the previous node
Another important list is a circular linked list in which the last node of the list points back to the first node (head) of
the linked list

#The Node Class
In Java, you are allowed to define a class (say, B) inside of another class (say, A). The class A is called the outer class
and the class B is defined the inner class. The purpose of inner classes is purely to be internally as helper classes.
Here is the linked list class with the inner node class.

                         private static class Node<AnyType>
                         {
                         private AnyType data;
                         private Node<AnyType> next;
                         
                         public Node(AnyType data, Node<AnyType> next)
                         {
                         this.data=data;
                         this.next=next;
                          }
                         }
                         
An inner class is a member of its enclosing class and has access to other members (including private) of the outer class, 
and vice versa, the outer class can have direct access to all members of the inner class. An inner class can be declared
private, public, protected, or packaged private. There are two kinds of inner classes: static and non-static. A static
inner class cannot refer directly to instance variables or methods defined in its outer class: it can use them only through 
its object reference.

We implement the LinkedList class with two inner classes: static Node class and non-static LinkedListIterator class. 

#Examples
Let us assume the singly linked list above and trace down the effect of each fragment below. The list is restored to its
initial state before each line executes

1.                        head=head.next;
2.                        head=head.next.next;
3.                        head.next.next.next.next=head;

#Linked List Operations
addFirst
The method creates a node and prepends it at the beginning of the list.
 
                          public void addFirst(AnyType item)
                          {
                          head = new Node<AnyType>(item, head);
                          }
                          
Traversing
Start with the head and access each node until you reach null. Do not change the head reference

                          Node tmp = head;
                          while(tmp!=null) tmp = tmp.next;
