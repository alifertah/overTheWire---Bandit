# overTheWireSolves

<details>
<summary >level 0</summary>


> first of all you need to connect to ssh and this step must be repeated everytime you get the password of the next level

```sh
ssh [username]@bandit.labs.overthewire.org -p 2220
// this will ask you to enter the password
```
once you get there type ```ls``` you will find a file called ```readme```
- type :
```sh
cat readme
```

this will show you the password to the next level 
- now type ```exit``` to exit this machine and connect to the level2 machine
</details>

<details>

<summary>level 1</summary>

> connect to this machine using ssh as mentionned before

once you get there type ```ls``` you will find a file called ```-``` 
if you try to ```cat - ``` this wont work because '-' is a special character that used to indcates flags of a command so if you wanna tell the terminal to give you tha content of that '-' file, type :

```sh
cat ./-
```

</details>

<details>

<summary>level 2</summary>

> connect to this machine using ssh as mentionned before

once you get there type ```ls``` you will find a file called `spaces in this filename`

you cant use `cat spaces in this file name` because it will count all other words after a single space as an argument to that command do you have to use a `\` before a space to skip it 
```sh
cat spaces\ in\ this\ filename
```

</details>

<details>

<summary>level 3</summary>

> connect to this machine using ssh as mentionned before

if you type `ls` you will find a directory called `inhere` type `cd inhere` to go to this directory and type `ls` again you will find nothing here, this doesnt mean that there is nothing, maybe there is a hidde  files, to show em type `ls -a`
then : 
```sh
cat .hidden
```

</details>


<details>

<summary>level 4</summary>

> connect to this machine using ssh as mentionned before

always we follow the same steps so you will find some files in inhere directory that you cant use `cat` to see there cntent, you just have to specify the right path and use the command like this 
```sh
cat ./file01
```
keep doing this for all the files until you find a human readable format, thats the password.

</details>

<details>

<summary>level 5</summary>

> connect to this machine using ssh as mentionned before

inside `inhere` directory you will find a lot of directories that contain a lot of files,
you cant use `cat` to each file until you find tha password, in the subject they gave you a hint, that the file we are looking for is 1033 bytes in size, and human readable...
so we will use the find command and give it the size like this : 

```sh
find . -size 1033c
```
this will print the path of the file and print its content using `cat`

</details>

<details>

<summary>level 6</summary>

> connect to this machine using ssh as mentionned before

here you they put the password file somewhere in the machine so you have to search in `/`. lets use our find command and give it the arguments given to us, size...
```sh
find / -group bandit6 -user bandit7 -size 33c -type f
```
this gives us a lot of files and also an error msg that says `permession denied`

so we will use this instead 

```sh
find / -group bandit6 -user bandit7 -size 33c -type f 2>/dev/null
```
`2>/dev/null` This part redirects error messages (stream 2, which is the standard error) to `/dev/null`, essentially suppressing error output. This is useful to hide any permission-denied errors or other potential issues during the search.

</details>


<details>

<summary>level 7</summary>

> connect to this machine using ssh as mentionned before

after finding a file called `data.txt` we are looking for a password that is written next to the word 'millionth', here is the command

```sh
cat data.txt | grep "millionth"
```

this will take the content of `data.txt` and outputs only the line that contains that word

</details>

<details>

<summary>level 8</summary>

> connect to this machine using ssh as mentionned before

we are looking for the password that is stored in the file `data.txt` and it's the only line of text that occurs only once. the command is: 
```sh
sort data.txt | uniq -u
```
this command will sort the `data.txt` file  so the count of uniq will not reset and `-u` flag will print the line that appears one time, count = 1;
</details>

<details>

<summary>level 9</summary>

> connect to this machine using ssh as mentionned before

here we are looking for a human readable string in the none redable file
we will use the command `strings` that prints only human readable characters. and we akso know that the password is preceded by several ‘=’ characters so we will use this command :
```sh
strings data.txt | grep "===="
```
</details>

<details>

<summary>level 10</summary>

> connect to this machine using ssh as mentionned before

we will finde a file that contains a string that ends with '=', so its a base64 encryption.
in linux we have `base64` command, we must just use that flag `-d` that means decode:
```sh
base64 -d data.txt
```
</details>

<details>

<summary>level 11</summary>

> connect to this machine using ssh as mentionned before

this level contains rot13 encryption, we have two options :
- use the rot13 decryption website 
- use tr command :
    ```sh
    cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
    ```
</details>