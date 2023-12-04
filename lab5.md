# Part 1

Subject: Help Needed - Strange Bug in My Code

Hey everyone,

I'm facing a weird issue in my code, and I'm not sure how to debug it.

Symptom:
The program crashes unexpectedly after processing a specific input.

My code:
```java
  static list<string> merge(list<string> list1, list<string> list2) {
    list<string> result = new arraylist<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() || index2 < list2.size()) {
      if(list1.get(index1).compareto(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      // change index1 below to index2 to fix test
      index2 += 1;
    }
    return result;
  }

```

Subject: Re - Help Needed - Strange Bug in My Code

Hey student,

You question ain't clear man. Try open up jdb to show me where it dies man.

```
echo "jdb Main" > run.sh
chmod +x run.sh
./run.sh
run
where all
```

Subject: Re - Re - Re - Help Needed - Strange Bug in My Code

Yeah it's that. Just go to the folder and open ListExamples.java and replace "index1 < list1.size() || index2 < list2.size()" with "index1 < list1.size() && index2 < list2.size()" It's crashing cause it ain't stopping when it depleted list 1.

Main.java
```java
import java.util.*;
import java.util.ArrayList;


public class Main {
    public static void main(String[] args){
        List<String> l1 = new ArrayList<String>(Arrays.asList("x", "y"));
		List<String> l2 = new ArrayList<String>(Arrays.asList("a", "b"));
		ListExamples.merge(l1, l2).toArray();
	}
}
```

ListExamples.java
```java
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() || index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      // change index1 below to index2 to fix test
      index2 += 1;
    }
    return result;
  }


}
```

run.sh
```
javac *.java
java Main
```

Command to reproduce:
```
./run.sh
```

# Part 2

I was familiar with most of the topics but it was nice to refresh the knowledge again. I got more familiar with some bash syntaxes and I learned how to use jdb.


