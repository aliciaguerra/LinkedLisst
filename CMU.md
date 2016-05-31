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
                          
addLast
Then method appends the node to the end of the list. This requires traversing but make sure you stop at the last node.

                          public void addLast(AnyType item)
                          {
                          if(head==null) addFirst(item);
                          else
                          {
                          Node<AnyType> tmp = head;
                          while(tmp.next!=null) tmp = tmp.next;
                          
                          tmp.next = new Node<AnyType>(item, null);
                              }
                          }
                          
Inserting "Before"
Find a node containing key and insert a new node before that node. In that picture, we insert a new node before "a".

For the sake of convenience, we maintain two references prev and curr. When moving along the list, we shift these two references, keeping prev one step before curr. We continue until curr reaches the node before which we need to make an
insertion. If curr reaches null, we don't insert, otherwise we insert a new node between prev and curr.

                         public void insertBefore(AnyType key, AnyType toInsert){
                          if(head==null) return null;
                          if(head.data.equals(key))
                              addFirst(toInsert);
                              return;
                          }
                          
                          Node<AnyType> prev = null;
                          Node<AnyType> curr = head;
                          while(curr!=null && !cur.data.equals(key)) {
                          prev=curr;
                          curr=curr.next;
                          }
                          //insert between curr and prev
                          if(curr!=null) prev.next=new Node<AnyType>(toInsert,curr);
                          }
                          
Deletion
Find a node containing "key" and delete it. 

The algorithm is similar to insert "before" algorithm. It is convenient to use two references prev and curr. When we move
along the list these two references, keeping prev one step before curr. We continue until curr reaches the node which we
need to delete. There are three exceptional cases, we need to take care of:
1. list is empty
2. delete the head node
3. node is not in the list

                       public void remove(AnyType key)
                       {
                       if(head==null) throw new Runtime Exception("cannot delete");
                       
                       if(head.data.equals(key))
                       {
                       head=head.next;
                       return;
                       }
                       
                       Node<AnyType> curr=head;
                       Node<AnyType> prev=head;
                       
                       while(curr!=null && !curr.data.equals(key)) {
                       prev=null;
                       curr=curr.next;
                       }
                       
                       if(curr==null) throw new RuntimeException("cannot delete");
                       
                       //delete our node
                       prev.node=curr.next;
                       }
                       
Iterator
The whole idea of the iterator is to provide access to a private aggregated data and at the same moment hiding the underlying representation. An iterator in Java is an object, and therefore it's implementation requires creating a class
that implements the Iterator interface. Usually such class is implemented as a private inner class. The iterator interface
contains the following methods. 

AnyType next() - returns the next element in the iterator
boolean hasNext() - checks if there is a next element
void remove() - removes by element returned by next()

In this section, we implement the Iterator in the LinkedList class. First we add a new method to the LinkedList class:

                     public Iterator<AnyType> iterator()
                     {
                     return new LinkedListIterator();
                     }
                     
Here, LinkedListIterator is a private class inside the LinkedList class

                     private class LinkedListIterator implements Iterator<AnyType>
                     {
                     private Node<AnyType> nextNode;
                     public LinkedListIterator(){
                       nextNode=head;
                       }
                       ...
                    }
                    
The LinkedListIterator class must provide implementations for next() and hasNext() methods. Here is the next() method

                     public AnyType next() {
                      if(!hasNext()) throw new NoSuchElementException();
                      AnyType res = nextNode.data;
                      nextNode = nextNode.next;
                      return res;
                      }
                      
Cloning

Like for any other objects, we need to learn how to clone linked lists. If we simply use the clone() method from the Object
class, we will get the following structure called a "shallow" copy:

The Object's clone() will create the copy of the first node and share the rest.   

Since out data is immutable it's ok to have shared data between two linked lists. We traverse the original list and copy each node by using the addFirst() method. When this is finished, you will have a new list in reverse order. Finally,
we have to reverse the list.

                     public Object copy() {
                      LinkedList<AnyType> twin = new LinkedList<AnyType>;
                      Node<AnyType> tmp = head;
                      while(tmp!=null)
                      {
                      twin.addFirst(tmp.data);
                      tmp=tmp.next;
                      }
                      return twin.reverse();
                      }

A better way invovles using a tail reference for the new list, adding each new node after the last node.

                       public LinkedList<AnyType> copy3() {
                        if(head==null) return null;
                        LinkedList<AnyType> twin = new LinkedList<AnyType>();
                        Node tmp = head;
                        twin.head = new Node<AnyType>(head.data, null);
                        Node tmpTwin = twin.head;
                        
                        while(tmp.next==null)
                        {
                        tmp=tmp.next;
                        tmpTwin.next=new Node<AnyType> (tmp.data, null);
                        tmpTwin=tmpTwin.next;
                        }
                        return twin;
                        }
                        
Polynomial Algebra
The biggest integer that we can store in a variable of the type int is 2^31-1 on 32-bit CPU. 

                         int prod=1;
                         for(int i=1; i<=; 31; i++)
                         prod*=2;
                         System.out.println(prod);
