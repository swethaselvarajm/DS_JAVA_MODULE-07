# Ex8 Detection of Cycle and Finding the Starting Node in a Linked List
## DATE: 14-10-2025
## AIM:
To write a program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
## Algorithm
1. Start the program.
2. Create a Node class with: data → stores the value of the node, next → reference to the next node.
3. Create a LinkedListCycle class with:
    1. A method to insert elements into the list.
    2. A method to create a cycle manually for testing (optional).
    3. A method to detect a cycle using Floyd’s Cycle Detection Algorithm (Tortoise and Hare method).
4. Cycle Detection Steps:
    1. Use two pointers: slow and fast.
    2. Move slow by one step and fast by two steps each time.
    3. If they meet, a cycle exists.  
5. Finding the starting node of the cycle:
    1. When a meeting point is found, reset slow to the head.
    2. Move both slow and fast one step at a time.
    3. The node where they meet again is the start of the cycle.
6. If no meeting point occurs, the list has no cycle. Display the result accordingly. Stop the program.

## Program:
```java
/*
Program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
Developed by: SWETHA S
Register Number: 212222230155
*/

import java.util.*;

public class Solution {

    static class ListNode {
        int val;
        ListNode next;

        ListNode(int x) {
            val = x;
            next = null;
        }
    }

    public ListNode detectCycle(ListNode head) {
       if(head==null || head.next==null){
           return null;
       }
       ListNode slow = head;
       ListNode fast = head;
       while(fast!=null && fast.next!=null){
           slow = slow.next;
           fast = fast.next.next;
           if(slow==fast){
               ListNode entry = head;
               while(entry!=slow){
                   entry = entry.next;
                   slow = slow.next;
               }
               return entry;
           }
       }
       return null;
       
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Solution sol = new Solution();

        String headInput = sc.nextLine().trim().replaceAll("\\[|\\]", "");
        
        int pos = sc.nextInt();

        if (headInput.isEmpty()) {
            System.out.println("no cylce");
            return;
        }

        String[] parts = headInput.split(",");
        int[] values = Arrays.stream(parts).mapToInt(Integer::parseInt).toArray();

        ListNode head = new ListNode(values[0]);
        ListNode current = head;
        List<ListNode> nodeList = new ArrayList<>();
        nodeList.add(head);

        for (int i = 1; i < values.length; i++) {
            ListNode newNode = new ListNode(values[i]);
            current.next = newNode;
            current = newNode;
            nodeList.add(newNode);
        }

      
        if (pos >= 0 && pos < nodeList.size()) {
            current.next = nodeList.get(pos);
        }


        ListNode cycleStart = sol.detectCycle(head);

        if (cycleStart != null) {
            int index = 0;
            for (ListNode node : nodeList) {
                if (node == cycleStart) {
                    System.out.println("tail connects to node index " + index);
                    return;
                }
                index++;
            }
        } else {
            System.out.println("no cycle");
        }
    }
}

```

## Output:
<img width="798" height="175" alt="image" src="https://github.com/user-attachments/assets/9d8d99fc-0ab8-4708-8517-3b5c6a2663a6" />



## Result:
The program successfully detects whether a cycle exists in the linked list.
If a cycle is present, it correctly identifies and returns the node where the cycle begins.
