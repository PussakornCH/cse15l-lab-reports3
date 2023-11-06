# Lab Report 3 - Bugs and Commands (Week 5)

[live_page_for_GitHub](https://pussakornch.github.io/cse15l-lab-reports3/lab-report.html)

## Part 1 - Bugs

**Array Methods: "Reverse Methods"**


``` bash
// A failure-inducing input
public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 1, 2, 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3, 2, 1 }, input1);
	}


  @Test
  public void testReversed() {
    int[] input1 = { 3, 2, 1 };
    assertArrayEquals(new int[]{ 1, 2, 3 }, ArrayExamples.reversed(input1));
  }

  @Test
  public void testAverageWithoutLowest(){
    double[] input1 = {1.0 ,1.0, 2.0, 3.0};
    assertEquals(2.0, ArrayExamples.averageWithoutLowest(input1), 0.0001);
  }
}
```


``` bash
// An input that doesn’t induce a failure
  @Test 
	public void testReverseInPlace() {
    int[] input1 = { 1, 1, 1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 1, 1, 1 }, input1);
	}

  @Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }

  @Test
  public void testAverageWithoutLowest(){
    double[] input1 = {1.0, 2.0, 3.0, 4.0};
    assertEquals(3.0, ArrayExamples.averageWithoutLowest(input1), 0.0001);
  }
```


**Screenshot from the two inputs**

![Image](1-1-fail1.PNG)
![Image](1-1-fail2.PNG)
**These two are the symptom of failure inputs** 


![Image](1-2-sucess.PNG)
**This is the symptom of success input when the code still has bugs**

``` bash
// Before fixing!
public class ArrayExamples {
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }

  // Averages the numbers in the array (takes the mean), but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }

    double sum = 0;
    
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }
}
```


``` bash
// After fixing!
public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    int temp;
    for(int i = 0; i < arr.length/2; i += 1) { // input = 1,2,3
      temp = arr[arr.length -i - 1]; // 3        
      arr[arr.length -i - 1] = arr[i];  //     1   
      arr[i] = temp;                 // 3    
      //temp = arr[i];

    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) { // 123 // 32
      newArray[i] = arr[arr.length - i - 1];
      String.format("The new[i] is %d", newArray[i]);
    }
    return newArray;
  }

  // Averages the numbers in the array (takes the mean), but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static double averageWithoutLowest(double[] arr) {
    int count = 0;
    if(arr.length < 2) 
      { return 0.0; }

    double lowest = arr[0];
    for(double num: arr) { 
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num == lowest && count == 0)
      {
        count += 1;
      }
      else {
        sum += num;
      }
    }
    return sum / (arr.length - 1);
  }
}
```

**Briefly describe why the fix addresses the issue:** 
1. reverseInPlace: I have created int temp to store the value; then, we can swap the first and last elements without duplicating any value.
2. reversed: I just rearranged the old array into the new array with the back-to-front method.
3. averageWithoutLowest: I only need to make sure that the program will skip the duplicate of the lowest value by adding count so that it will only switch one time.


## Part 2 - Researching Commands

## find command
1. find directory -name file.txt
> Search for files that are specified by ‘file.txt’ = search for this specific file
``` bash
// First example
Mark@DESKTOP-OJL6LKL MINGW64 ~/VS_Code/CSE_15L/docsearch/technical (main)
$ find plos/ -name "*.txt" > file-result.txt
plos/journal.pbio.0020001.txt
plos/journal.pbio.0020010.txt
plos/journal.pbio.0020012.txt
plos/journal.pbio.0020013.txt
plos/journal.pbio.0020019.txt
plos/journal.pbio.0020028.txt
plos/journal.pbio.0020035.txt
...
plos/pmed.0020275.txt
plos/pmed.0020278.txt
plos/pmed.0020281.txt
```

``` bash
// Second example
Mark@DESKTOP-OJL6LKL MINGW64 ~/VS_Code/CSE_15L/docsearch/technical (main)
$ find plos/ -name "pmed.0020239.txt" 
plos/pmed.0020239.txt
```

2. find directory -empty
>  Search for empty files and directories. Because there are no empty files in /technical, I create sample.txt in plos, and the command find it
``` bash
// First example
Mark@DESKTOP-OJL6LKL MINGW64 ~/VS_Code/CSE_15L/docsearch/technical (main)
$ find . -empty
```

``` bash
// Second example
Mark@DESKTOP-OJL6LKL MINGW64 ~/VS_Code/CSE_15L/docsearch/technical (main)
$ find plos -empty
plos/sample.txt
```

3. find directory -type d
> This command displays all the repositories and sub-repositories present in the current repository.
```
// First example
Mark@DESKTOP-OJL6LKL MINGW64 ~/VS_Code/CSE_15L/docsearch/technical (main)
$ find . -type d 
.
./911report
./biomed
./government
./government/About_LSC
./government/Alcohol_Problems
./government/Env_Prot_Agen
./government/Gen_Account_Office
./government/Media
./government/Post_Rate_Comm
./plos
```

``` bash
// Second example
Mark@DESKTOP-OJL6LKL MINGW64 ~/VS_Code/CSE_15L/docsearch/technical (main)
$ find government/ -type d
government/
government/About_LSC
government/Alcohol_Problems
government/Env_Prot_Agen
government/Gen_Account_Office
government/Media
government/Post_Rate_Comm
```

4. find directory -newer directory/file
>  Search for files that were modified/created after ‘file’. I create sample.txt and sample2.txt before file-result.txt, and the command is able to detect that I go in to 911report and government to create those 2 files.
```
// First example
Mark@DESKTOP-OJL6LKL MINGW64 ~/VS_Code/CSE_15L/docsearch/technical (main)
$ find ./ -newer file-result.txt 
./911report
./911report/sample.txt
./government
./government/sample2.txt
./plos
```

``` bash
// Second example
Mark@DESKTOP-OJL6LKL MINGW64 ~/VS_Code/CSE_15L/docsearch/technical (main)
$ find ./ -newer 911report/
./government
./government/sample2.txt
```

**All the information come from: https://www.geeksforgeeks.org/find-command-in-linux-with-examples/**
