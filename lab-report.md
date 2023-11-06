# Lab Report 3 - Bugs and Commands (Week 5)

[live_page_for_GitHub](https://pussakornch.github.io/cse15l-lab-reports3/lab-report.html)

## Part 1 - Bugs

**Array Methods: "Reverse Methods"**

``` bash A failure-inducing input

```

``` bash An input that doesn’t induce a failure

```

**Screenshot from the two inputs**
Explain the failure input
Explain the sucuss input

``` bash Before fix

```

``` bash After fix

```

Briefly describe why the fix addresses the issue: 

![Image](3-1.JPG)

* The method handleRequest is called
* The argument is URI url. The values are ArrayList<String> s, int num, URI url, String[] parameters, String mess, and String print.
* The values that change are the parameters that get string input from the user, String print that will contain new string make up of the user input without '+' character, ArrayList<String> s that will add the string in print into the array of string (in this case: "Hello"), and the num increase by 1.


## Part 2 "SSH key"

![Image](3-5com.JPG)

ls command just shows where the private and public key is in this computer
