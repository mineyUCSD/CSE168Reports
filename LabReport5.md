# Lab Report 5

## Edstem Post


**What environment are you using (computer, operating system, web browser, terminal/editor, and so on)?**

Windows computer using the Git Bash terminal


**Detail the symptom you're seeing. Be specific; include both what you're seeing and what you expected to see instead. Screenshots are great, copy-pasted terminal output is also great. Avoid saying “it doesn't work”.**

So, I am testing out my grader bash script from the Week 6 lab, and 2 of my tests on the `merge` function aren't passing. I can't figure out why because I am getting wierd errors, and one of my `merge` methods passes. I am confused.... 

Here is the JUnit output from my grader
**JUnit Output**
``` txt
JUnit version 4.13.2
...E.....E.
Time: 0.03
There were 2 failures:
1) testMerge(TestListExamples)
java.lang.AssertionError: expected: java.util.Arrays$ArrayList<[m, r, t, w, w, y]> 
but was: java.util.ArrayList<[m, r, t, w, w, y]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at TestListExamples.testMerge(TestListExamples.java:44)
2) testMergeLeftEnd(TestListExamples)
java.lang.AssertionError: expected:<[a, a, b, d, z]> but was:<[a, a, b, d]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at TestListExamples.testMergeLeftEnd(TestListExamples.java:35)

FAILURES!!!
Tests run: 9,  Failures: 2
```

**Detail the failure-inducing input and context. That might mean any or all of the command you're running, a test case, command-line arguments, working directory, even the last few commands you ran. Do your best to provide as much context as you can.**

My bash script, grade.sh, clones a repository I made with the List Methods. I run grader with the command
**Grader Output**
``` bash
$ bash grade.sh git@github.com:mineyUCSD/listMethodsForLabReport5.git
```
And my grader outputs

``` txt
MINGW64_NT-10.0-22621
Cloning into 'student-submission'...
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (12/12), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 12 (delta 3), reused 11 (delta 2), pack-reused 0
Receiving objects: 100% (12/12), done.
Resolving deltas: 100% (3/3), done.
Finished cloning
Found ListExamples.java
copying stage
compiled JUNIT, Student Files, and Tests
Output redirected to ./grading-area/grade.sh
Analyzing JUnitOutput...
Looks like some tests failed! Bozo Clown Baby!
Total Tests: 9
Tests Ran: 9
Tests Failed: 2
Tests Passed: 7
Score: 7/9
```
All of the tests run, but 2 fail as I stated above. Everything is cloned properly and the grader worked as expected, other than my tests not passing!!!! The repository I cloned is supposed to pass all of the tests, I copied it from the file in lab...

**Here is the content of the repository's `ListExamples.java`**
``` java
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
        result.add(s);
      }
    }
    return result;
  }

  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    
    while(index1 < list2.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }


}
```

Here are all of the `merge` tests I have in my `TestListExamples.java` file
 **`TestListExamples.java`**
``` java
public class TestListExamples {

  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }

  @Test(timeout = 500)
  public void testMergeLeftEnd() {
    List<String> left = Arrays.asList("a", "b", "z");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "d", "z");
    assertEquals(expected, merged);
  }

  @Test(timeout = 500)
  public void testMerge() {
	  List<String> first = Arrays.asList("m, r, t");
	  List<String> second = Arrays.asList("w, w, y");
	  List<String> merged = ListExamples.merge(first,second);
	  List<String> expected = Arrays.asList("m, r, t, w, w, y");
	  assertEquals(expected, merged);
  }
//more tests below this that aren't buggy
}
```
Yeah, I am just at a loss because my tests aren't passing when I am pretty sure my `ListExamples.java` file works. And the `testMergeRightEnd()` method passes as well. The JUnit error says something about:

``` txt
 java.lang.AssertionError: expected: java.util.Arrays$ArrayList<[m, r, t, w, w, y]> 
 but was: java.util.ArrayList<[m, r, t, w, w, y]>
```

and I don't know what the difference between `java.util.Arrays$ArrayList` and `java.util.ArrayList` is. The arrays have the same contents! Please Help...

## TA Response

Ok Bucko... I appreciate the extensiveness of your post!

Here are some tips that may lead you to the solution

* Try running your grader with the working methods repository provided in lab. Here is the link: [https://github.com/ucsd-cse15l-f22/list-methods-corrected](https://github.com/ucsd-cse15l-f22/list-methods-corrected)
* See if the tests pass on the functional list methods. If they don't, then there is probably a bug in your tests
* Also, since you said you copied the functional methods, compare your code with the working methods and see if you made a typo.
* As for the `java.util.Arrays$ArrayList` vs `java.util.ArrayList`, `java.util.Arrays$ArrayList` is a method inside of the `Arrays` class that implements the `List` class, while `java.util.ArrayList` is just an object from the `ArrayList` class. you should check the array in your test to make sure you are instantiating it properly.

That is all, again, much appreciated for the erudite and eloquent and concise and exauhstive EdStem Post. Best wishes and dishes

## Taking TA's Advice

Hmmm... I guess I'll attempt to run my grader with the functional repository. SO
**Grader Output**
``` bash
$ bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected
MINGW64_NT-10.0-22621
Cloning into 'student-submission'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Finished cloning
Found ListExamples.java
copying stage
compiled JUNIT, Student Files, and Tests
Output redirected to ./grading-area/grade.sh
Analyzing JUnitOutput...
Looks like some tests failed! Bozo Clown Baby!
Total Tests: 9
Tests Ran: 9
Tests Failed: 1
Tests Passed: 8
Score: 8/9
```
Wow! One of the tests that was failing passed! I am elated! Jubilation! There must then be an error in my repository... I guess I'll try and sort that out...

**Here is `ListExamples.java` my version**
``` java
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
        result.add(s);
      }
    }
    return result;
  }

  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    
    while(index1 < list2.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }


}
```

**Here is `ListExamples.java` not buggy version**
``` java
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
        result.add(s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
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
      index2 += 1;
    }
    return result;
  }


}
```

Now if only I could spot the difference... This feels like Blue's Clues! Oh Where is this nasty little typo lurking like a lilac lamb!

Um, let me check the `JUnitOutput.txt` for the correct methods to see which test passed

**JUnitOutout**
``` txt
$ cat JUnitOutput.txt
JUnit version 4.13.2
...E......
Time: 0.023
There was 1 failure:
1) testMerge(TestListExamples)
java.lang.AssertionError: expected: java.util.Arrays$ArrayList<[m, r, t, w, w, y]> 
but was: java.util.ArrayList<[m, r, t, w, w, y]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at TestListExamples.testMerge(TestListExamples.java:44)

FAILURES!!!
Tests run: 9,  Failures: 1
```
Interesting. The `testMergeLeftEnd` test passed with the correct repository. I wonder why. Let me examine closely.... The `testMergeLeftEnd` JUnit output in the prior test was

``` txt

testMergeLeftEnd(TestListExamples)
java.lang.AssertionError: expected:<[a, a, b, d, z]> but was:<[a, a, b, d]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at TestListExamples.testMergeLeftEnd(TestListExamples.java:35)

```
So, the outputted array has one less element than the inputted array. Maybe There is something fishy in one of my loops. 

NOOOOOO!!!!!!

**My Loop**
``` java
while(index1 < list2.size()) {
    result.add(list1.get(index1));
    index1 += 1;    
}
```
**Correct Loop**
``` java
while(index1 < list1.size()) {
    result.add(list1.get(index1));
    index1 += 1;
}
```

I must've fat fingered `2` in my loop when I was copying it. That is strange that my method worked for the `testMergeRightEnd` test though. Oh, Whatever, nevermind.

But... There is still a Test that hasn't passed! And it Test is `testMerge`. Ima compare `JUnit` outputs to see if it is the same in both implementations

``` txt
 1) testMerge(TestListExamples)
java.lang.AssertionError: expected: java.util.Arrays$ArrayList<[m, r, t, w, w, y]> 
but was: java.util.ArrayList<[m, r, t, w, w, y]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at TestListExamples.testMerge(TestListExamples.java:44)

```
``` txt
1) testMerge(TestListExamples)
java.lang.AssertionError: expected: java.util.Arrays$ArrayList<[m, r, t, w, w, y]>
but was: java.util.ArrayList<[m, r, t, w, w, y]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at TestListExamples.testMerge(TestListExamples.java:44)
```

Word for word, exact same error. I suppose I will listen to the TA and check my test. There has to be something wacky about the expected array versus the outputted array.

``` java
@Test(timeout = 500)
  public void testMerge() {
	  List<String> first = Arrays.asList("m, r, t");
	  List<String> second = Arrays.asList("w, w, y");
	  List<String> merged = ListExamples.merge(first,second);
	  List<String> expected = Arrays.asList("m, r, t, w, w, y");
	  assertEquals(expected, merged);
  }
```
Looks good. I have my Lists of Strings, each with 3 elements, and then my `expected` List is all of those elements in the sorted order. What is the bug.... OH MY GOODNESS GRACIOUS JIMINEY CRICKET KISSER! I put quotes around all of the elements, so I made lists with only 1 element, the literal string `m, r, t` rather than `m`,`r`,`t`. Ok, so let me fix the THREE times I made that mistake unknowingly.

**Fixed Test**
``` java
@Test(timeout = 500)
  public void testMerge() {
	  List<String> first = Arrays.asList("m", "r", "t");
	  List<String> second = Arrays.asList("w", "w", "y");
	  List<String> merged = ListExamples.merge(first,second);
	  List<String> expected = Arrays.asList("m", "r", "t", "w", "w", "y");
	  assertEquals(expected, merged);
  }
```

Let me run my grader to see if I earn a perfect score now that I fixed my Lists.
 
**Grader Output**
```
$ bash grade.sh git@github.com:mineyUCSD/listMethodsForLabReport5
MINGW64_NT-10.0-22621
Cloning into 'student-submission'...
remote: Enumerating objects: 15, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 15 (delta 4), reused 14 (delta 3), pack-reused 0
Receiving objects: 100% (15/15), done.
Resolving deltas: 100% (4/4), done.
Finished cloning
Found ListExamples.java
copying stage
compiled JUNIT, Student Files, and Tests
Output redirected to ./grading-area/grade.sh
Analyzing JUnitOutput...
All Tests Passed
Total Tests: 9
Score: 9/9
```

Yay!!! It worked!!! Time to push my fixed Tests to GitHub. Um, I still don't really get the `java.util.Arrays$ArrayList` error, but oh well, ok. Thanks TA! My code works now!
## Information Needed about the setup

**File and Directory Structure**

**grader directory**
``` cmd
C:.
ª   clean.sh
ª   grade.sh
ª   GradeServer.java
ª   Server.java
ª   TestListExamples.java
ª   
+---grading-area
ª       hamcrest-core-1.3.jar
ª       IsA.class
ª       IsMoon.class
ª       junit-4.13.2.jar
ª       JUnitOutput.txt
ª       ListExamples.class
ª       ListExamples.java
ª       StringChecker.class
ª       TestListExamples.class
ª       TestListExamples.java
ª       
+---lib
ª       hamcrest-core-1.3.jar
ª       junit-4.13.2.jar
ª       
+---student-submission
        ListExamples.java
        README.md

```
**ListExamples Repository**
``` cmd
C:.
    ListExamples.java
    README.md
    
No subfolders exist 
```
---

**Contents of Bugged Files**

**Bugged Tests**
``` java
public class TestListExamples {

  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }

  @Test(timeout = 500)
  public void testMergeLeftEnd() {
    List<String> left = Arrays.asList("a", "b", "z");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "d", "z");
    assertEquals(expected, merged);
  }

  @Test(timeout = 500)
  public void testMerge() {
	  List<String> first = Arrays.asList("m, r, t");
	  List<String> second = Arrays.asList("w, w, y");
	  List<String> merged = ListExamples.merge(first,second);
	  List<String> expected = Arrays.asList("m, r, t, w, w, y");
	  assertEquals(expected, merged);
  }
//more tests below this that aren't buggy
}
```

**Bugged ListMethods.java**
``` java
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
        result.add(s);
      }
    }
    return result;
  }

  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    
    while(index1 < list2.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }


}
```
---
**Bug Triggering Command Line**

**Grader Command**
``` bash
$ bash grade.sh git@github.com:mineyUCSD/listMethodsForLabReport5.git
```

**There were two bugs.** 

* One of the bugs was a typo in my `ListExamples.java` file.  I identified the typo in my `ListExamples.java` file by comparing it to the working given `ListExamples.java` file from the lab. The typo changed the logic in a while loop, which snipped out one of the elements from being added to the resultant array. Change `2` to `1`! This didn't affect `testMergeRightEnd` because `c` isn't the latest letter in the resultant array like `z` is in `testMergeLeftEnd` 
* And another was some typos in my `testMerge` test that created `List`s with one element full of a bunch of letters rather than many separate single letter elements. Caused some screwy stuff.

---

## Reflection. When will it show who I am inside?


My favorite part of lab in the second of this quarter was definitely learning about bash scripts. Actually, it was learning about how to make git repositories. They are very cool. And now I can put all of my code up on GitHub like a cool cat!! I felt some seratonin when I got my `grade.sh` file to work. It was cool incorporating everything learned in the class to make it. Cloning, Junit, Bash commands. Super cool cucumber callous. My second favorite thing, pertaining to the class but sort've on top of it, was getting Jekyll to work with Github pages and then editing the theme to get some pretty pink and purple stylings. That took me a while! And because of the Github knowledge, it is pushed! It is pushed! I think there may be some issues with the files I have on Github becasue, locally, I am edited the `.md` and testing them locally, I just pushed all of them to Github. um. That was pretty challenging trying to get something to work that I had no clue how it worked or how to understand how to get a clue. Following junk instruction online. I really liked this course and hope I can get a full pass on the next Skill Demo. This is all, and all you are, and all you'll be, will be eclipsed by the moon. Out.


