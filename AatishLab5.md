# Lab Report 5
## Aatish Mandalapu - A17350430
---
## Part 1
### Student Help Question
- Here is my bug. I am writing some code to create a sorting machine, but the outputs are buggy. The sorted array that is outputted seems to have duplicate values in the same index. This could be an issue with my code that swaps the index values to be in order. This is what I have as my code in a file from lab with a few adaptations, called `Sort.java`. Additionally, below is in the terminal command line and is the bash script to run the code to see the output. I would appreciate if someone would be able to help me correct this output given my code.


```

import java.util.ArrayList;

public class Sort {

    public static int[] selection(int[] lst) {
        for (int i = 0; i < lst.length - 1; i++) {
            int min = i;
            for (int j = i; j < lst.length; j++) {
                if (lst[min] >= lst[j]) {
                    min = j;
                }
            }
            lst[i] = lst[min];
        }
        return lst;
    }

    public static void main(String[] args) {
        int[] testArr = {8, 7, 6, 5, 4};
        int[] expectedArr = {1, 2, 3, 4, 5};

        System.out.println("Test Array:");
        System.out.print("[ ");
        for (int j : testArr) {
            System.out.print(j + " ");
        }
        System.out.println("]");

        int[] newArr = selection(testArr);

        for (int i = 0; i < newArr.length; i++) {
            if (newArr[i] != expectedArr[i]) {
                System.out.println("Error! Did not match expected array!");
                break;
            }
        }

        System.out.println("Sorted Array:");
        System.out.print("[ ");
        for (int value : newArr) {
            System.out.print(value + " ");
        }
       
 System.out.println("]");
    }
}

```

- Bash Script in Commandline:
(1) `javac Sort.java` 
(2) `java Sort`

- Now after compiling, I ran the test using `bash test.sh` in commandline. 
- Here is the output:

```
Test array:
[ 8 7 6 5 4]
Error! Output did not match expected array!
Sorted array: 
[ 1 1 1 1 ]
```

### TA Suggestion
Hey Aatish! The code looks good for the most part. However, to solve your issue, I would suggest you rewrite the code for specifically where the array gets swapped so that you can ensure that the array is being sorted correctly. The current output error you are getting is because you're code finds the minimum value, 1, correctly - so good job there!

### Student Debug Process
- Looking back on the swapping process here: 

```

public static int[] selection(int[] lst) {
        for (int i = 0; i < lst.length - 1; i++) {
            int min = i;
            for (int j = i; j < lst.length; j++) {
                if (lst[min] >= lst[j]) {
                    min = j;
                }
            }
            lst[i] = lst[min];
        }
        return lst;
    }

```

- This section of the code did not actually swap the location of the values in the array. It just assigned the minimum value again to each current element, and would not place the current value correctly. This is because the min value, 1, was located at the end of the array list, so that is why 1 was assigned to every element in the index in the output.
- I realized I needed to assign another temporary variable so that it could store the current value and swap it without it being reassigned to the minimum value as the previous code snippet showed.
- Here is the updated, debugged code with the temporary variable, `swap` included to correctly relocate the numbers to correctly sort the array.

```

public static int[] selection(int[] lst) {
    for (int i = 0; i < lst.length - 1; i++) {
        int min = i;
        for (int j = i + 1; j < lst.length; j++) {
            if (lst[min] > lst[j]) {
                min = j;
            }
        }
        int swap = lst[i];
        lst[i] = lst[min];
        lst[min] = swap;
    }
    return lst;
}

```
This is the output after running `bash test.sh` again in commandline with the new debugged code.

```
Test Array:
[ 8 7 6 5 4 ]
Sorted Array:
[ 1 2 3 4 5 ]
```

- As you can see it is now correctly sorted as intended, so we know that adding the swap variable as a temporary holder for the values.

## Part 2
### Reflection
- In the second half of the quarter, I focused on improving how I use Vim, the text editor that lets me code and debug directly from the command line. This skill has been very useful because it helps me work faster and more efficiently, which will be crucial during my bioinformatics internship this summer where I'll be using Unix a lot to debug code and write/run tests for analysis. 
Learning Vim, along with other Unix commands, has really prepared me for the challenges ahead. I’m looking forward to applying these skills in my internship, confident that they will make my work smoother and more productive.