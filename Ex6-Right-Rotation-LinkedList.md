# Ex6 Right Rotation LinkedList
## DATE: 07-10-2025
## AIM:
To write a Java  program to:

1. Create a singly linked list.
2. Rotate the linked list to the right by k positions.
3. Display the rotated linked list.
   
## Algorithm
1. Start the program.
2. Create a Node class with two fields: data (to store the element), next (to store the reference to the next node).
3. Create a LinkedListRotation class to manage the list.
4. Insert elements into the linked list.
5. Read the value of k (number of rotations).
6. To rotate the list right by k positions:
     1. Find the length of the list.
     2. Connect the last node to the head (making it circular).
     3. Find the new head after (length - k % length) nodes.
     4. Break the link after the new tail node.
7. Display the final rotated linked list and end the program.

## Program:
```java
/*
Program to  Right Rotation LinkedList
Developed by: SWETHA S
Register Number: 212222230155
*/

import java.util.Scanner;
public class RotateLinkedList {
    public static Node rotate(Node head, int k) {
       if (head==null || head.next == null || k==0)return head;
       
       int length = 1;
       Node tail = head;
       while(tail.next != null){
           tail  =tail.next;
           length++;
        }
        
        k = k%length;
        if (k==0) return head;
        
        int steps = length-k;
        Node newTail = head;
        for (int i=1; i<steps; i++){
            newTail = newTail.next;
        }
        
        Node newHead = newTail.next;
        newTail.next = null;
        tail.next = head;
        
        return newHead;
       
    }
    public static void display(Node head) {
        Node current = head;
        System.out.print("LinkedList: ");
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Node head = null, tail = null;
        int n = scanner.nextInt();
        for (int i = 0; i < n; i++) {
            Node newNode = new Node(scanner.nextInt());
            if (head == null) {
                head = tail = newNode;
            } else {
                tail.next = newNode;
                tail = newNode;
            }
        }
        int k = scanner.nextInt();
        head = rotate(head, k);
        display(head);
        scanner.close();
    }
}
class Node {
    int data;
    Node next;
    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

```

## Output:
<img width="779" height="135" alt="image" src="https://github.com/user-attachments/assets/1462a042-975d-4a0a-8fad-a81659d0443c" />



## Result:
Thus, the Java program to perfom right rotation on linked list is implemented successfully.
