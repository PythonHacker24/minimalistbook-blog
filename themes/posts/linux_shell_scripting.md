+++
category = "technical"
title = "Linux Shell Scripting — A Suckless and Concise Guide to the Command-line of Linux"
date = 2024-01-19
+++

*Prior Statements: This is a concise guide on the Linux Shell Scripting while consolidating all the facts about the Linux Shell for quick developer’s reference while using Linux. I am referencing the Bash (Bourne-Again Shell) which is the default shell for Linux-based systems. I will also be providing references and external links to dive into depth and not fill the article with too much explanation about a single topic which is not universally required by all the readers. Bash Scripting is a vast topic and cannot be covered in a single article. I will be providing the very basics here and providing references to external links to learn more.*

## Overview of the Shell in Operating Systems
The shell is a program that acts as a buffer between the user and the operating system. It is a command interpreter and acts invisibly. The three main uses for the shell are:

1. Interactive use of the system
2. Customizing the Linux session by defining variables and startup files
3. Programming, by writing and executing shell scripts

*“Computers are incredibly fast, accurate, and stupid. Human beings are incredibly slow, inaccurate, and brilliant. Together they are powerful beyond imagination.”- Albert Einstein*

## Historical Overview of the Linux Shells
[Bourne Shell](https://en.wikipedia.org/wiki/Bourne_shell) was the standard shell used for writing shell scripts. Bourne Shell is still found in the /bin/sh on the Linux Systems (although they are now [symbolic links](https://en.wikipedia.org/wiki/Symbolic_link#:~:text=A%20symbolic%20link%20contains%20a,exists%20independently%20of%20its%20target.) to the Bash). The [Berkeley C shell](https://en.wikipedia.org/wiki/C_shell) (csh and later tcsh) offered better features for interactive use, such as command history and job control. For a long time, the standard practice was to use the Bourne-Shell for programming and the C-shell for daily use. David Korn at [Bell Labs](https://en.wikipedia.org/wiki/Bell_Labs) enhanced the Bourne shell by adding csh-like features and his shell was known as the [Korn shell](https://en.wikipedia.org/wiki/KornShell) (ksh).

The Free Software Foundation developed a clone of the Bourne Shell and developed the Bourne-Again Shell (Bash). Bash has become a [POSIX-complaint](https://en.wikipedia.org/wiki/KornShell) version of the shell, incorporating many popular features from other shells like csh, tcsh and ksh. Bash is now the primary shell for Linux.

Another popular shell is the Z Shell (zsh) which is similar to the ksh but with many extensions. zsh differs from the bash in two ways: it is based on ksh and does not attempt to be POSIX-compliant.

*To get a grip on the Linux command line, it is essential to understand basic Linux Commands. Canonical (the creator of the Ubuntu Linux Operating System) has provided a guide for absolute beginners to [learning the basics of the command line](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview). The Linux command line for beginners. Experience with operating the Linux command line is also essential.*

## The Prefix and Executing Shell Script
The shebang for shell scripts is `#!/bin/bash`. This tells the system that the executing file is a bash script and it needs the bash interpreter to work. Before executing a shell script, it’s essential to mark it as executable and provide the necessary permissions by using the command: `chmod +x <filename>`. To execute the script: `./<filename>`.

## Read, Store, Print and Wait ….
Declaring a variable: `name="maverick"`

Reading User Input: `read name`

Printing content and variables: `echo "hello $name"` ($ symbol returns the value of the variable)

Delay for some time: `sleep <no_of_seconds>`

## Arrays in Bash Scripts

Arrays can be declared in the following way:

```bash
#!/bin/bash

declare -a languages=(
[0]=rust
[1]=golang
[2]=python
[3]=c
)

echo "${languages[@]}"
```

## Running System Commands in the Script
`name=$(uname)`: This will execute the `uname` command and store it’s output in the name variable. (print the output with `echo "$name"`)

## Predefined Variables in Linux Shells
eg. RANDOM

$RANDOM will return any random number between 0–32767

The outputs of the commands given below are just examples:

```bash
>> echo $RANDOM
30011

>> echo $PWD 
/root

>> echo $SHELL 
/bin/bash

>> echo $USER 
root

>> echo $HOSTNAME 
localhost
```

*Note: The double quotes in the bash script support a lot of symbols that can be used for various purposes. On the other hand, single quotes are strict and consider everything inside them to be string.*

## Arithmetic Operations in bash

```bash
>> echo $(( 2 + 3 ))       # Addition 
5

>> echo $(( 2 / 3 ))       # Division
0

# Note: Bash does not return the data in float. 2/3 = 0.666666.....

>> echo $(( 10 / 3 ))      # / is for division
3

>> echo $(( 10 & 3 ))      # & is for remainder
1
```

Example Snippet of a Bash Program

```bash
#!/bin/bash

echo "What is your name?"

read name

echo "How old are you?"

read age

echo "Hello $name, you are $age years old."

sleep 2

lucky_number=$((( $RANDOM % 10 ) + $age ))

echo "$name, your lucky number is $lucky_number"
```

## Conditional Statements

```bash 
read number 

if [[ $number = 10 ]]; then 
  echo "number is 10"
elif [[ $number = 20 ]]; then
  echo "number is 20"
else 
  echo "The number was not guessed: $number"
fi
```

The following was a quick reference to if and else statements and all you need to know to understand them. They can be used for making decisions and adjusting the control flow of the scripts. They are highly useful in Linux Automation when handling errors and edge cases.

```bash 
case $number in                 

        1)
                echo "It's 1"
                ;;              # This means go ahead and check next case

        2)
                echo "It's 2"
                ;;
        3)
                echo "It's 3"
                ;;
esac
```

Case statements can be used to consolidate the if-else statements and create very specific cases for the control flow of the script to continue.

Comprehensive Example for Control Flow and Conditionals in Bash:

```bash 
#!/bin/bash

# Yes, I am a Hacker and this script is an example hacker manual

echo "This is a tool manual. Enter the tool number to get information about it.
1. metasploit
2. aircrack-ng
3. hydra"

read number

echo "Are you a experienced hacker? (y/n)"

read answer

case $answer in                 


        y)
                echo "This is a very basic manual for you then.... "
                ;;

        n)
                echo "This is useful for you then!"
                ;;

esac

case $number in

        1)
                echo "You have selected the metasploit option"
                ;;

        2)
                echo "You have selected the aircrack-ng option"
                ;;
        3)
                echo "You have selected the hydra option"
                ;;
esac


if [[ $number == "1" ]]; then
 echo "Do you want to know about msfconsole or msfvenom?
 1. msfconsole
 2. msfvenom"

 read number

 if [[ $number == "1" ]]; then
  echo "msfconsole is a interactive environment framework for exploitation of known vulnerabilities as well as exploit development"

 elif [[ $number == "2" ]]; then
  echo "msfvenom is a payload generater"

 fi

elif [[ $number == "2" ]]; then
 echo "Aircrack-ng is Wi-Fi penetration framework"

elif [[ $number == "3" ]]; then
 echo "hydra is a fast login bruteforcer"

fi

echo "Thank you for using this manual"
```

## Loops in Bash Script — While, Until and for loops

**While Loop:** A while loop continues to loop over a snippet of code until the conditions provided are true. As soon as it gets false, the while loop is escaped and further script is executed.

```bash 
#!/bin/bash

x=1

echo "Number of clicks to end"
read target

# The condition will be provided to the while loop
while [[ $x -le $target ]]           # -le means less than or equal to
do
 read -p "Click $x: Press enter to continue"

 (( x++ ))                           # Post incremental operator
done

echo "Target completed"
```
```bash 
while true          
do
 echo "This goes forever!"
done
```

**Until Loop:** Until loops continue to run until some condition is true. The loop initiates when the given condition is false and executes the given snippet of code until the provided conditions are true.

```bash 
#!/bin/bash

until [[ $password == "correct_password" ]]
do
 echo "Enter the password: "
 read password
done
echo "Access Granted!"
```

Until loops are kind of opposite to while loops. They run until the provided condition is satisfied.

While loop runs while the given condition is true. Until loop runs until the given condition is true.

**For Loop:** For loops don’t wait for a certain condition to be true and execute the given snippet of code until the specified range of items are selected and covered.

```bash 
for cups in 1 2 3 4 5 6 7 8 9 10;
do
 echo "Hey, you've had $cups of coffee today. "

done
```
```
for cups in {1..10};        # range is provided for simplicity
do
 echo "Hey, you've had $cups of coffee today. "

done
```
For loop can be useful for various purposes like traversing over files in the directory or even going through lines in a file, etc.
```bash 
#!/bin/bash

declare -a languages=(
[0]=rust
[1]=golang
[2]=python
[3]=c
)

# Itterating over arrays with for loop
for i in ${languages[@]}
do
echo -e "$i \n"
done
```

Some example scripts for reference

```bash
#!/bin/bash

# Script to check if the given website is up
for x in google.com bing.com facebook.com;
do
 if ping -q -c 2 -W 1 $x > /dev/null; then
  echo "$x is up"
 else
  echo "$x is down"
 fi
done
```

```bash
#!/bin/bash

# Checking the weather in the cities provided in the cities.txt file
for x in $(cat cities.txt);
do
 weather=$(curl -s http://wttr.in/$x?format=3)
 echo "The weather for $weather"

done
```

```bash
#!/bin/bash

# Script to create a Wi-Fi prompt for suckless dmenu (my own Arch linux script)
interfaces=$(nmcli device | awk '$2=="wifi" {print $1}')

selected_interface=$(echo "$interfaces" | dmenu -p "Select a network interface:" -l 10)

wifi_list=$(nmcli device wifi list ifname "$selected_interface" | awk '{print $2}')

selected_network=$(echo "$wifi_list" | dmenu -p "Select a Wi-Fi network:" -l 10)

password=$(echo "" | dmenu -p "Enter the Wi-Fi password:")

nmcli device wifi connect "$selected_network" password "$password"

echo "Connecting to $selected_network..."
```

```bash
#!/bin/bash 

# Converts an image or a directory of images to .webp format
if [ -d "$1" ]; then 
  for file in "$1"/*; do 
    if file --mime-type "$file" | grep -q "image"; then
      cwebp "$file" -o "${file%.*}.webp"
      echo "[+] Converted $file to ${file%.*}.webp"
    else 
      echo "[-] Skipping file: $file"
    fi
  done
else
  file=$1
  cwebp "$file" -o "${file%.*}.webp"
fi
echo "Conversion Completed"
```

There are a lot of references to go with for learning and mastering Linux Shell scripts.

Books I recommend:

Wicked Cool Shell Scripts: 101 Scripts for Linux, OS X, and Unix Systems — Dave Taylor, Brandon Perry
- Linux in a Nutshell — Ellen Siever, Stephen Figgins, Robert Love and Arnold Robbins
- Linux Shell Scripts have been very useful for my overall computer usage. I have been using Linux as my primary operating system and I am safe to say that my whole computer works on the backbone of these shell scripts. Bash Scripting have a lot of usage in automating tasks and I believe them to be holding the power of automating IT systems in a versatile and simple fashion.


