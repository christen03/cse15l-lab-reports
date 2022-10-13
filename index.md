# CSE 15L Week 3 Lab Report - Christen Xie  

Welcome back! This lab report will go over two things: **Simplest Search Engine** and **Debugging and Test Cases**

## Week 2 - Simplest Search Engine 
In week 2, we devleoped a "search engine" where a user could add their inputs into and could query themselves. When a string was added, it would be stored in a list, and a query could be any string. When queried, the seach engine would display any string that contained the search as a substring.
Here is my running code behind the search engine.

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler{
    ArrayList<String> items = new ArrayList<String>();
    public String handleRequest(URI url){
        if(url.getPath().equals("/")){
            return String.format("Welcome to the search engine!");
        }
        else if(url.getPath().equals("/add")){
            String[] parameters = url.getQuery().split("=");
            if(parameters[0].equals("s")){
                items.add(parameters[1]);
                return String.format(parameters[1]+" added to engine!");
            }
            else{
                return "No item found to add!";
            }
        }
            else if(url.getPath().equals("/search")){
                ArrayList<String> found = new ArrayList<>();
                String[] parameters = url.getQuery().split("=");
                if(parameters[0].equals("s")){
                    for(int i=0; i<items.size(); i++){
                        if (items.get(i).contains(parameters[1])){
                            found.add(items.get(i));
                        }
                    }
                }
                if(found.size()!=0){
                return String.format(found.toString());
                }
                else{
                    return "Nothing found!";
                }

            }
            else{
               return "404 Not found!";
            }
    }
}

    class SearchEngine {
        public static void main(String[] args) throws IOException {
            if(args.length == 0){
                System.out.println("Missing port number! Try any number between 1024 to 49151");
                return;
            }
    
            int port = Integer.parseInt(args[0]);
    
            Server.start(port, new Handler());
        }
    }
```

### Code in Action
So how does this work? It starts in the terminal, where it's compiled then run with your choice of port number. I used port #1225, but feel free to choose your own!

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab2images/run-server.png?raw=true)

#### Running The Server
You can then find the server running online at the URL shown, for me it's *http://localhost:1225*.

Now the homepage looks something like this:

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab2images/homepage.png?raw=true)

#### Adding to Search Engine
To **add** something to the search engine, we can simply add **/add?s=[wordToAdd]** into the URL. For example, if I wanted to add *apple*, my new URL would be **http://localhost:1225/add?s=apple**. 
For this example, I'm going to add "apple", "pear", "grape", and berry. My URLs to add look like
- http://localhost:1225/add?s=apple (apple)
- http://localhost:1225/add?s=pear (pear)
- http://localhost:1225/add?s=grape (grape)
- http://localhost:1225/add?s=berry (berry)

The output on the page should look something like this (with whatever you're adding):

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab2images/adding-engine.png?raw=true)

This works because it runs in the `else if(url.getPath().equals("/search"))` of the code. Since the path is what is after the domain, we put `/search` as the path. This matches the condition of `getPath().equals("/search)`, and enters if statement.
Inside, we again create a new String array, parameters that splits everything before and after the "=" into an element in the array. If the first element (or string before the "=") is "s" (which it is in our case) the engine will then take the second element of the array (or string after the "=") and loop through the entire added word list. It will return any string in the added word list that contains the string after "=" in a substring. If it can't find any string, it will return that nothing is found.

#### Querying Search Engine

To **query** something to the search engine, we can simply add **/search?s=[stringToQuery]** into the URL. For example, if I wanted to query for words that contained *i*, my new URL would be **http://localhost:1225/serach?s=i**. 
Continuing from the first example, I want to find anything that contains the letter "a". My query URL looks like:

*http://localhost:1225/serach?s=a*

The output on the page should look something like this:

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab2images/search.png?raw=true)

This worked! Since apple, pear, and grape have "a", but berry does not. 

This works because it runs in the `else if(url.getPath().equals("/add"))` of the code. Since the path is what is after the domain, we put `/add` as the path. This matches the condition of `getPath().equals("/add)`, and enters if statement.
Inside, we create a new String array, parameters that splits everything before and after the "=" into an element in the array. If the first element (or string before the "=") is "s" (which it is in our case) the engine will add the second element of the array (or the string after the "="). Otherwise, it will fail and return that nothing is added.

#### Error!

What happens if the path is neither `/search` or `/add`? The code will then pass around both else if statements and go to the bottom else statement, which will just return a **404 not found error**. For example, if I plug in `/dance` as a path, I get this:

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab2images/server-fail.png?raw=true)

## Week 3 Testing and Debugging

In week 3, we found some erroneous code and with tests, were able to pinpoint some issues and debug them. Here are two examples and walkthroughs of failed then fixed code:

### Example 1 - Reversing an Array

This was the original failure-inducing input, the idea is to take an array and reverse the elements inside of it. 

```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```

When I ran the following test, it failed.

```
  @Test 
  public void test(){
    int[] input={3,2,3};
    assertArrayEquals(new int[]{3,2,3}, ArrayExamples.reversed(input));
  }
```

The **symptom**, or visual failing output it displayed was
`arrays first differed at element [0]; expected:<3> but was:<0>`
This means that for a correctly reversed array, the element at index 0, (first item) is 3, but the faulty code resulted in it being 0.

The bug fix was to flip what was on each side of the "=" in the for loop, so 
`arr[i] = newArray[arr.length - i - 1];` ->  `newArray[arr.length - i - 1] = arr[i];`
as well as to return `newArray` instead of `arr` (the original array), so 
`return arr;` -> `return newArray;`.

This symptom was being caused by this bug because a new array wass being created and it is being iterated through backwards, but the original array’s values were getting changed to the new array’s values, which are all 0. There was nothing changing the new array’s values to the reverse of the original array. Then, in addition, the original array was being returned.

### Example 2 - Filtering a List

This was the original failure-inducing input, the idea is to take a list and filter for a certain type of string inside of it. (Remove any string that doesn't match the condition.)

```  
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }
```
When I ran the following test, it failed:

```
@Test 
    public void testFiler(){
List<String> array_input=new ArrayList<String>();
array_input.add("apple");
array_input.add("pear");
array_input.add("grape");
array_input.add("berry");
ArrayList<String> correct_input=new ArrayList<>();
correct_input.add("apple");
correct_input.add("pear");
correct_input.add("grape");
array_input=ListExamples.filter(array_input, new HasLetterA());
assertArrayEquals(array_input.toArray(), correct_input.toArray());
}
```

This is the `StringChecker` I used, (HasLetterA):

```
class HasLetterA implements StringChecker{
    @Override
    public boolean checkString(String s){
        return s.contains("a");
    }
}
```

The **symptom**, or visual failing element it displayed was

`


