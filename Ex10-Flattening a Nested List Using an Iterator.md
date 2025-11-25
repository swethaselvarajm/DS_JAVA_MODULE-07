# Flattening a Nested List Using an Iterator
## DATE: 21-10-2025
## AIM:
To design and implement a class NestedIterator that flattens a nested list of integers such that all integers can be accessed sequentially using an iterator interface (next() and hasNext()).
## Algorithm
1. Start the program. 
2. Define an interface or class structure for NestedInteger, which can hold either: A single integer, or A nested list of integers.
3. Create the NestedIterator class that: Uses a stack to keep track of the nested list. Traverses through the list elements and flattens them.
4. Implement the following methods:
    1. hasNext(): Checks if there are more integers to iterate over.
    2. next(): Returns the next integer in sequence.
5. In the main program: Create nested lists of integers. Use the NestedIterator object to iterate and print all integers sequentially.

## Program:
```java
/*
Program to find Flattening a Nested List Using an Iterator
Developed by: SWETHA S
Register Number: 212222230155
*/

import java.util.*;
public class NestedIterator implements Iterator<Integer> {
    private List<Integer> integers = new ArrayList<>();
    private int position = 0;

    public NestedIterator(List<NestedInteger> nestedList) {
        flattenList(nestedList);
    }

    private void flattenList(List<NestedInteger> nestedList) {
         for(NestedInteger ni: nestedList)
        {
            if(ni.isInteger())
            {
                integers.add(ni.getInteger());
            }
            else
            {
                flattenList(ni.getList());
            }
        }
        
    }

    @Override
    public Integer next() {
        return integers.get(position++);
        
    }
    @Override
    public boolean hasNext() {
        return position<integers.size();
        
    }
    public static List<NestedInteger> parse(String s) {
    Stack<List<NestedInteger>> stack = new Stack<>();
    List<NestedInteger> curr = new ArrayList<>();
    int num = 0;
    boolean hasNum = false;

    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        if (c == '[') {
            stack.push(curr);
            curr = new ArrayList<>();
        } else if (c == ']') {
            if (hasNum) {
                curr.add(new SimpleNestedInteger(num));
                hasNum = false;
                num = 0;
            }
            List<NestedInteger> completed = curr;
            curr = stack.pop();
            curr.add(new SimpleNestedInteger(completed));
        } else if (c == ',') {
            if (hasNum) {
                curr.add(new SimpleNestedInteger(num));
                hasNum = false;
                num = 0;
            }
        } else if (Character.isDigit(c)) {
            num = num * 10 + (c - '0');
            hasNum = true;
        }
    }
    return curr;
}


    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
      
        String input = sc.nextLine();

        List<NestedInteger> nestedList = parse(input);

        NestedIterator iterator = new NestedIterator(nestedList);
        List<Integer> output = new ArrayList<>();
        while (iterator.hasNext()) {
            output.add(iterator.next());
        }

        System.out.println(output);
    }
}

interface NestedInteger {
    boolean isInteger();
    Integer getInteger();
    List<NestedInteger> getList();
}

class SimpleNestedInteger implements NestedInteger {
    private Integer value;
    private List<NestedInteger> list;

    public SimpleNestedInteger(Integer value) {
        this.value = value;
        this.list = null;
    }

    public SimpleNestedInteger(List<NestedInteger> list) {
        this.list = list;
        this.value = null;
    }

    @Override
    public boolean isInteger() {
        return value != null;
    }

    @Override
    public Integer getInteger() {
        return value;
    }

    @Override
    public List<NestedInteger> getList() {
        return list;
    }
}

```

## Output:
<img width="594" height="90" alt="image" src="https://github.com/user-attachments/assets/2ed02c84-5ea3-4a30-bd22-198ca361f5b2" />



## Result:
The NestedIterator class successfully flattens a nested list of integers into a single list and provides sequential access using standard iterator methods.
