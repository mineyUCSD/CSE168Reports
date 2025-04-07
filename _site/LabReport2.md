# Lab Report 2

## Part 1
---

### StringServer.java

![image](https://user-images.githubusercontent.com/130080241/233507029-e784b138-38e7-48ab-a03a-5a45acb2cc78.png)

---

### Server.java

![image](https://user-images.githubusercontent.com/130080241/233508271-09223dce-4def-4aa5-8407-ed341a55cb65.png)

---

### * Which methods in your code are called?

*I wrote the code in `StringServer.java`, so I will refer to the code in that file.*

**Two methods in the file are called:** 

`public String handleRequest(URI url)`

`public static void main(String[] args)`

---

### * What are the relevant arguments to those methods, and the values of any relevant fields of the class?

The method `public String handleRequest(URI url)` takes in a URL from the search bar and uses the infromation in the search bar for functionalities in the program

There is also a field in the Handler class called `String storageString` that is initialized emptily, but will contain future inputed strings

Another variable in the Handler class is `String[] parameters` that splits the query up into the type of query, index 0, and the value, index 1. 

In the StringServer main method,  it takes in a `String[]` arguments from the command line, called args. To start the server, I type `java StringServer` + whatever port is available, and that port number is the first element in args.

There are also some methods that are called in handleRequest that seemssomewhat pertinent,  `getQuery()` and `getPath()`. I think that URIs have these methods in java, and they do quite a bit of the work in this program. `getPath()` gets the path part of the URI and converts it to a `String` so that it can be utilized in the program, like seeing if the path is empty, or contains some command. 

The `getQuery()` method looks in the URI for a `?` and then any text after that it returned as a `String`, sort've like `getPath()`. This is useful because then you can use a query to even further specify a command, in this case asking to store and print a `String `.

---

### * How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.

If `/add-message?s=<string>` is added at the end of the url in searchbar, with `<string>` being any inputted string, then the `storageString` field is concatenated with the inputed `<string>` and a new line `\n`.

The program knows to obtain the String because of the query `?s=<string>`. `s` is the type of query(the only functional one in this program) and `<string>` is the value for this query. Each is stored, respectively, in `String[] paramaters` as an element in index 0 and index 1. 

The `storageString` is then returned in the handleRequest Method, which causes the `storageString` to be printed onto the webpage. 

Every time the page is refreshed, a new URI is passed into the program, so that update is what allows multiple responsive inputs into the program, and therefore multiple words printed. 

---

### Two Screenshots of `/add-message?s=<string>`

![image](https://user-images.githubusercontent.com/130080241/233535194-9fee4589-3c1d-403b-ba04-cd4a5b362333.png)

* Which methods in your code are called?

`public String handleRequest(URI url)` is called in the `Server.java` file. I think that the file uses this method to see what should be done with the url that is entered into the search bar. In this case, the url entered is `http://localhost:3333/add-message?s=Communist`. Once the program gets the url input, it looks at the portions of the url using `.getPath()` and `.getQuery()`. Based on these methods, the program returns some `String`.

* What are the relevant arguments to those methods, and the values of any relevant fields of the class?

handleRequest() takes a url, and that is obtained from the search bar of the page that is opened by the server. 

`.getPath()` and `.getQuery()` are methods that can be used to get information from URIs, described a bit more in the preliminary accidental, missreading instructions, section.

The field in the class `StringServer.java` is `private String storageString` which is initialized emptyily. After the methods are called, and assuming there is some qeury and path of the form `http://localhost:3333/add-message?s=<string>`, then `<string>` is concatentated to `storageString` and `storageString` is returned.

* How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.

In this iteration, since it is the first time a String Query is added to the url, the `<string>` is added to `storageString` and is then returned. `storageString` goes from being empty to having the value `"Communist\n"`. `storageString` is remembered when new urls are entered into the server, as is demonstrated by the next screenshot.

---

![image](https://user-images.githubusercontent.com/130080241/233535404-fdbbfa60-ef10-4051-9258-df7cbffea6b2.png)

* Which methods in your code are called?

Same methods.

`public String handleRequest(URI url)`
`getPath()`
`getQuery()`
`split()`
`equals()`

* What are the relevant arguments to those methods, and the values of any relevant fields of the class?


`public String handleRequest(URI url)` takes a url from the searchbar. The method uses that url and the other methods above to look at the URL and decide what `String` to return

`url.getPath()` is used on the url `http://localhost:3333/add-message?s=Daughter` to get the path, so it returns `/add-message`

`url.getQuery()` returns the query, everything after the ?, `s=Daughter`

`split` is used on the query, and sticks everything separated by `=` into an array called `parameters`. it looks like `{"s","Daughter"}`

`equals` is used to see if the query or patch matches what is expected for a `String` to be stored in `storageString'

* How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.

After all of the methods are called, the program runs, given the new url inputted, `Daughter/n` is added to `stringStorage`. What is cool about this is that `stringStorage` still has the value `Communist/n` that was added from the last query inputed via url. So now, `stringStorage` has the the value `"Communist/nDaughter/n"` pretty neat. I wonder where this data is stored??? 

---

### Demo

the command `java StringServer 3333` is entered to start the server. 3333 is the port number and StringServer is the name of the class that contains the main method for the server. 

![image](https://user-images.githubusercontent.com/130080241/233507778-725bb3b3-39dd-4005-afd5-cce0079bdd31.png)

I then went to the localhost and edited the url to read `localhost:3333/add-message?s=Hello` the path is `localhost:3333/add-message` and the query is `?s=Hello`
Since the query tells the program to return the `String` Hello, it does so by adding it to the `storageString` and then returning the extended `storageString`. 

![image](https://user-images.githubusercontent.com/130080241/233507360-05852274-507a-41f7-b211-7bc04c9990d6.png)

Next, I did the same thing, but changed the query to `?s=World` and this updates the URI query so that the program wants to add `World` to the `storageString` and then return it. As you can see, it then prints `Hello\nWorld\n` because that is how the Strings are added to `storageString`.

![image](https://user-images.githubusercontent.com/130080241/233507427-8be85b16-57a9-4e49-bfb6-fa367ede51ff.png)

I added a more introspective query here that utilizes aliteration. It is also much longer. I want to test if adding `/n` into the query String can make a new line???

![image](https://user-images.githubusercontent.com/130080241/233507641-e7040856-e29f-478a-b9e6-0a16235fb32c.png)

No. Says bad syntax 😦

![image](https://user-images.githubusercontent.com/130080241/233514565-7e6a0738-0988-4882-b7e7-10316d25ef63.png)

---

## Part 2

### ArrayExamples.java

I choose ArrayExamples.java as my buggy program.

Here is a failure-inducing input for the `ReverseInPlace()` method written as a JUnit test

```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
	    int[] input1 = {1,2};
	    ArrayExamples.reverseInPlace(input1);
	    assertArrayEquals(new int[]{2,1}, input1);
	}
}
```

Here is a nonfailure-inducing input for the `ReverseInPlace()` method written as a JUnit test

```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
		int[] input1 = {3};
		ArrayExamples.reverseInPlace(input1);
		assertArrayEquals(new int[]{3}, input1);
	}
}


```

---

Symptoms:

![image](https://user-images.githubusercontent.com/130080241/233518811-653410d1-a35a-4a4e-826d-6697d7ff95da.png)

The failure inducing input test fails, huh. The array {1,2} when reversed by the method gives the array {2,2} instead of {2,1}. This could be for a factor of reasons without looking at the code.

---

**Before Code/ Bug riddled code:**

```
// Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {

    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
    
  }
  
```

**Fixed(probably) code:**

```
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    int[] dummy = new int[arr.length];

    for(int i = 0; i < dummy.length; i++){
      dummy[i] = arr[i];
    }

    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = dummy[arr.length - i - 1];
    }
  }
```

Looking at the infested code, it appears that the error occurs because the arr is being reversed while also serving as the input for the reversing. So if it has {a,b}, it makes the first index the last index in the array, so {b,b}, but then on another iteration of the loop it uses that modified loop as the input for the reversal. Instead of seeing that the first index element is a, it looks at the partially modified array and sees that the element is b, so the reversed array according to this program is {b,b}, or {2,2}.

Therefore, my solution to this bug was creating a duplicate array, `dummy` that has the contents of `arr` so that I can reverse arr and then compare it to the unreversed version dummy instead of the partially reversed `arr`. I think it works, swimmingly like a sea urchin??? Or for my tests it does. 

## Part 3

I learned a lot and like learning a lot in these weeks 2 and 3 so much! I learned about `git`, some server stuff, JUnit, debugging and bug terminologies, yeah. The only thing that isn't new is basic java syntax. With `git,` I learned how to clone repositories and fork them so I can work on people's code or share my own code. I learned about JUnit so I can easily make some tests for my java programs. I learned how to make a local host Java webserver thingy that can do some behavior based on the URl. I learned about urls and URIs. So, quite a bit of handy stuff was learned.   





