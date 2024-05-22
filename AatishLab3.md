# Lab Report 3
## Aatish Mandalapu - A17350430
---
## Part 1
- The bug I am choosing reverses and inputted array. This is taken from the `reverseInPlace` method.
```
public void testReverseInPlaceSuccess() {
  int[] input1 = {5,6,6,5};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{5,6,6,5}, input1);
}
```
- This test aims to evaluate the method's performance with a simple input to verify its basic functionality. However, the current result shows a failure, as the actual output is ```{10, 9, 8, 9, 10}```
---
```
public void testReverseInPlaceSuccess() {
  int[] input1 = {1,2,2,1};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{1,2,2,1}, input1);
}
```
- This test passes because the array is symmetric. When the method iterates over the second half of the array, if it mirrors the first half, it reproduces the original array.
- insert image
# Changing the Code
## Code Before
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
  arr[i] = arr[arr.length - i - 1];
  }
}
```
## Code After
```
static void reverseInPlace(int[] arr) {
  int n = arr.length;
  for(int i = 0; i < n / 2; i++) {
    int temp = arr[i];
    arr[i] = arr[n - 1 - i];
    arr[n - 1 - i] = temp;
  }
}
```
- This code starts by determining the length of the array and storing it in the variable n. It then initializes a temporary variable temp within the loop. For each element in the first half of the array, it swaps the element with the following element from the opposite side. This makes sure that the entire array is correctly reversed. The loop runs only through the first half of the array which prevents the output from  being a mirror of the original list.
# Part 2
## The find command
- The `find` command is a useful tool that locates and provides specific files or directories. The -type option allows you to go through items based on their types, such as directories/files or others like `.md`.
- For example, using the command `% find ./technical -type f` from lab5 provides a list of files inside the `technical` directory.
Output: 
```
./technical/biomed/1471-2199-2-6.txt
./technical/biomed/bcr567.txt
./technical/biomed/gb-2002-3-10-research0055.txt
./technical/biomed/1471-2121-2-3.txt
./technical/biomed/1471-213X-1-11.txt
./technical/biomed/1472-684X-1-5.txt
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
etc 
```
- We can also see this if we search for directories instead with `d` instead of `f`. This outputs a list of the directories that are also within the `technical` directory.
```
./technical
./technical/biomed
./technical/government
./technical/government/About_LSC
./technical/government/Env_Prot_Agen
./technical/government/Alcohol_Problems
./technical/government/Post_Rate_Comm
./technical/government/Media
./technical/empty
./technical/911report
```
- With this command, we can find other directories that are contained within this specific one.
To further learn how this command works, I will use 3 options to demonstrate how this command works on the `./technical` directory.

The `empty` option
- This option allows users to search for, as implied by the name, empty files/directories.
- Since the directory `./technical` has no empty files I will provide code blocks of what it would look like if there was an empty directory as well as an empty file.
- Command: `% find ./technical -empty`
- Output for an empty file in a directory named test:
`./technical/test/emptyfile.txt`
- Command for finding an empty directory: `% find ./technical -empty`
- Output for empty directory `test`: `./technical/test`
- By using this option, terminal is able to effectively find and provide the empty files and directories within the specified working directory. This helps managing the size of the directory allowing for more efficiency.

The `-depth` option
- This option finds and provides a sorted list of files/directories. It filters through the working directory and spits out files starting with the deepest directory first and does this until it reaches the back of the parent directory.
- For example, using this command in the `technical` directory `% find ./technical -depth` it prints a list of the files in sorted by location in the directory.
```
./technical/biomed/bcr567.txt
./technical/biomed/gb-2002-3-10-research0055.txt
./technical/biomed/1471-2121-2-3.txt
./technical/biomed/1471-213X-1-11.txt
./technical/biomed/1472-684X-1-5.txt
./technical/biomed/1476-4598-1-6.txt
./technical/biomed
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
etc
```
- Additionally, if I wanted to find specific files like within the biomed directory I could use the command `% find ./technical/biomed -depth` to give me the sorted files that belong in that directory. 
Output:
```
./technical/biomed/bcr567.txt
./technical/biomed/gb-2002-3-10-research0055.txt
./technical/biomed/1471-2121-2-3.txt
./technical/biomed/1471-213X-1-11.txt
./technical/biomed/1472-684X-1-5.txt
./technical/biomed/1476-4598-1-6.txt
./technical/biomed
```
- This is useful since we can filter through the files based on where it is in the working directory or in further directories within.

The `-size` option
- With this option, we can find files or directories sorted by their size. This can help find files that are less than a specific amount of storage.
- For example, if I want to find files less than 15KB in this directory, I would use `% find ./technical/911report -size -15k`.
Output:
```
./technical/911report
./technical/911report/preface.txt
```
To provide another example of how `-size` is used, we can change the storage size search to increase to 1 megabyte.
- With `% find ./technical/911report -size -1M` we get this output:
```
./technical/911report
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
etc
```
- Using this option with the `find` command. it allows us to more efficiently search for necessary files or help clean out workspace by deleting files that take too much space in the OS.

I used https://www.computerhope.com/unix/ufind.htm and https://man7.org/linux/man-pages/man1/find.1.html to help me provide descriptions and examples for the `find` command.