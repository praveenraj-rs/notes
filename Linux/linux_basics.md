# linux_basics
# Commands 
#linux

1. sudo useradd -m -G sftpusers -s /sbin/nologin sftpuser
2. sudo passwd sftpuser
3. passwd -d root
4. passwd -l root
5. groupadd
6. groupdel
7. usermod
8. chmod
9. chown
10. tmux
11. gpasswd
12. ssh
13. cat /etc/passwd
14. cat /etc/groups
15. docker
16. openssh
17. ssh-keygen
18. sudo chmod 400 myAWSKey.pem
19. ssh -i myAWSKey.pem ec2-user@192.168.1.1
20. ssh-copy-id -i ~/.ssh/id_rsa.pub root@123.43.123
21. systemctl status sshd
22. sudo apt install ssh-server
23. env
24. variable = $(command)
25. man test
26. lsof -i:3000
27. kill pidNo, kill 22326
28. hostname -I
29. lsusb
30. dmesg|grep ttyUSB
31. nmap 192.168.210.0/24
32. ifconfig
33. ping www.google.com
34. traceroute www.google.com
35. nslookup www.google.com
36. dig www.google.com
37. sudo apt install package_file.deb
38. sudo apt -f install package_file.deb
39. sudo dpkg -i package_file.deb
40. sudo dpkg -i --force-all package_file.deb
41. sudo apt-get remove package_name
42. sudo add-apt-repository
43. curl -X POST -H "Content-Type: application/json" -d @book.json http://localhost:3500/sensorasdf
44. 
45. python3 -m http.server 8000
46. npx http-server -p 8080 
47. sudo systemctl start service
48. sudo systemctl enable service
49. sudo systemctl stop service
50. sudo systemctl disable service
51. `export PATH=/home/praveenrajrs/Desktop:$PATH`
52. whereis
53. which command
54. sudo chmod a+rw /dev/ttyUSB0
55. . ws or source ws 
56. tail -f filename.txt
57. mkdir {frontend, backend, dev, test}
58. tcpdump port 22
59. tcpdump -i eth0
60. sudo dpkg-reconfigure tzdata - set timezone



# 1. rfkill

```bash
rfkill block wifi
rfkill unblock wifi 
```

# 2. nmcli

## Step 1: Enable Your Wi-Fi Device

```
nmcli dev status
```

```
nmcli radio wifi
```

If the output shows that the Wi-Fi is **disabled**, you can enable it with the following command:
```
nmcli radio wifi on
```

## Step 2: Identify a Wi-Fi Access Point

```
nmcli dev wifi list
```

Note the name listed under **SSID** for the network you want to connect to. You'll need it for the next step.

## Step 3: Connect to Wi-Fi With nmcli

```
sudo nmcli dev wifi connect network-ssid
```

Replace **network-ssid** with the name of your network. If you have WEP or WPA security on your WI-Fi, you can specify the network password in the command as well.

```
sudo nmcli dev wifi connect network-ssid password "network-password"
```

Alternatively, if you don't want to write out your password onscreen, you can use the **--ask** option.

```c
sudo nmcli --ask dev wifi connect network-ssid
```
```
ping google.com
```

## Managing Network Connections With nmcli

You can view all the saved connections by issuing the following command:

```
nmcli con show
```

```
nmcli con down ssid/uuid
```

```
nmcli con up ssid/uuid
```

# 3. hostname

To get the ip address of the network on terminal
```
hostname -i 
```

# 4. lshw

List Hardware Command

# 5. lsusb

List the USB connection to the system

# 6. usermod


# Bash Scripting

1. `#` Comment
2. `echo` printing
3. man test
4. expr 5 + 2
5. expr 5 \* 2
6. myvar="any variable"
7. myvar=5
8. `echo $myvar` To print the variable content
9. `myvar=$(any command)` Storing the output of command in variable
10. Condition
```bash
myvar=10
if [ $myvar -eq 10 ]
then
	echo Variable is equal to 10
else
	echo Not equal
fi
```

11. `$1` Taking input while executing the script
12. Conditional Statement
```bash
date1=$(date)
sum1= expr 5 \* 5
echo $date1 
echo $sum1

if [ -f raj.sh ]
then
	echo File Exists
else
	echo File Not Exists
fi
```

13. While Loop
```bash
myvar=$1
while [ $myvar -le 10 ]
do
	echo $myvar
	myvar=$(($myvar+1))
	sleep 0.25
done
```
14. For Loop
```bash
for [ n in {1..5} ]
do
    echo $n
    n=$(($n+1))
    sleep 0.25
done
```

15. `export PATH=/home/praveenrajrs/Desktop:$PATH`

16.  ```find -name "*programming*" 1>result.txt 2>error.txt```
# Bash Scripting Notes


## Writing Your First Bash Script
To write a Bash script, follow these steps:

1. **Create a New File**: Use a text editor (e.g., `nano`, `vim`, or a GUI editor) to create a new file with a `.sh` extension. For example: `myscript.sh`.

2. **Add Shebang**: Start your script with a shebang line that specifies the interpreter. The most common shebang for Bash scripts is `#!/bin/bash`.

3. **Write Your Script**: Add your commands and logic to the script file. Remember to use proper syntax and indentation.

4. **Make Script Executable**: Run `chmod +x myscript.sh` to make your script executable.

5. **Run Your Script**: Execute your script by running `./myscript.sh`.

## Basic Syntax and Commands
- **Comments**: Use `#` to add comments in your script.
- **Variables**: Declare variables like `variable_name=value`. Access them using `$variable_name`.
- **Strings**: Enclose strings in single or double quotes.
- **Command Execution**: Use backticks or `$()` to execute commands within a script.
- **User Input**: Read user input using the `read` command.

```bash
#!/bin/bash

# Declare a variable
name="John"

# Print a message
echo "Hello, $name!"

# Execute a command and capture its output
current_date=$(date)

# Read user input
echo "Enter your age:"
read age
echo "You are $age years old."
```

## Conditional Statements
Use `if`, `elif`, and `else` for conditional branching.

```bash
#!/bin/bash

read -p "Enter a number: " num

if [ "$num" -gt 0 ]; then
    echo "Number is positive."
elif [ "$num" -lt 0 ]; then
    echo "Number is negative."
else
    echo "Number is zero."
fi
```

## Loops
Bash supports `for` and `while` loops.

```bash
#!/bin/bash

# For loop
for i in {1..5}; do
    echo "Iteration $i"
done

# While loop
count=0
while [ "$count" -lt 3 ]; do
    echo "Count: $count"
    ((count++))
done
```

## Functions
Define functions using the `function` keyword or shorthand syntax.

```bash
#!/bin/bash

# Define a function
my_function() {
    echo "Hello from my_function!"
}

# Call the function
my_function
```

Certainly! Here's an extended section in the Markdown notes covering zipping and unzipping files using Bash scripting:

## Zipping and Unzipping Files

Bash scripting can be used to automate tasks like compressing and decompressing files and directories using various compression formats.

### Zip Files using `zip`

The `zip` command is used to create compressed archive files.

```bash
#!/bin/bash

# Zip a file
zip my_archive.zip file1.txt file2.txt

# Zip a directory
zip -r my_directory.zip my_directory/
```

### Unzip Files using `unzip`

The `unzip` command is used to extract files from a zip archive.

```bash
#!/bin/bash

# Unzip a file
unzip my_archive.zip

# Unzip to a specific directory
unzip my_archive.zip -d extraction_folder/
```

### Tar and gzip using `tar`

The `tar` command is used to create and manipulate tape archive files. When combined with `gzip`, it creates compressed tarball files (`.tar.gz` or `.tgz`).

```bash
#!/bin/bash

# Create a tarball
tar -czvf my_files.tar.gz file1.txt file2.txt

# Extract a tarball
tar -xzvf my_files.tar.gz
```

### Untar and ungzip using `tar`

To extract tarballs that are compressed using `gzip`, use the `-z` flag.

```bash
#!/bin/bash

# Extract a tarball
tar -xzvf my_files.tar.gz
```

### Tar and bzip2 using `tar`

The `tar` command can also be used with `bzip2` compression to create `.tar.bz2` files.

```bash
#!/bin/bash

# Create a tarball with bzip2 compression
tar -cjvf my_files.tar.bz2 file1.txt file2.txt

# Extract a tarball with bzip2 compression
tar -xjvf my_files.tar.bz2
```

### Compress and Decompress Individual Files

For compressing and decompressing individual files, you can use the `gzip` and `gunzip` commands.

```bash
#!/bin/bash

# Compress a file
gzip file.txt

# Decompress a file
gunzip file.txt.gz
```

### Compress and Decompress Directories

For directories, use the `-r` flag with `gzip` and `gunzip` to recursively compress and decompress.

```bash
#!/bin/bash

# Compress a directory and its contents
gzip -r my_directory

# Decompress a directory and its contents
gunzip -r my_directory.gz
```

Remember that compression formats like `zip`, `tar.gz`, and `tar.bz2` have different compression levels and capabilities. Choose the format that best suits your needs.

Always ensure you have the required tools installed on your system (`zip`, `unzip`, `tar`, `gzip`, `bzip2`) before running these scripts.

Certainly! Here's an extended section in the Markdown notes covering the use of the `case` statement in Bash scripting:

## Using the `case` Statement

The `case` statement in Bash allows you to perform branching based on pattern matching. It's useful for handling multiple conditions in a structured way.

```bash
#!/bin/bash

# Using the case statement
fruit="apple"

case $fruit in
    "apple")
        echo "It's an apple."
        ;;
    "banana")
        echo "It's a banana."
        ;;
    "orange" | "citrus")
        echo "It's an orange or citrus."
        ;;
    *)
        echo "Unknown fruit."
        ;;
esac
```

In the example above, the `case` statement checks the value of the `fruit` variable against different patterns. Depending on the value of `fruit`, the corresponding code block is executed. The `*)` pattern acts as a catch-all for any value that doesn't match the previous patterns.

### Pattern Matching

You can use various patterns in the `case` statement:

- `*`: Matches anything.
- `?`: Matches any single character.
- `[abc]`: Matches any one character specified within the brackets.
- `[a-z]`: Matches any one character within the specified range.
- `!(pattern)`: Matches any value that does not match the specified pattern.
- `@(pattern)`: Matches any one of the patterns specified.
- `+(pattern)`: Matches one or more occurrences of the pattern.
- `*(pattern)`: Matches zero or more occurrences of the pattern.

```bash
#!/bin/bash

# Using pattern matching in case
file="my_script.sh"

case $file in
    *.txt)
        echo "Text file."
        ;;
    *.sh)
        echo "Shell script."
        ;;
    *)
        echo "Unknown file type."
        ;;
esac
```

### Case-Insensitive Matching

To perform case-insensitive matching, use the `nocasematch` option:

```bash
#!/bin/bash

shopt -s nocasematch

fruit="ApPle"

case $fruit in
    "apple")
        echo "It's an apple."
        ;;
    *)
        echo "Not an apple."
        ;;
esac

shopt -u nocasematch
```

Remember to turn off the `nocasematch` option using `shopt -u nocasematch` if you don't want case-insensitive matching to apply globally.

### Combining with Loops

The `case` statement can be combined with loops for more advanced usage.

```bash
#!/bin/bash

# Using case and loop
while true; do
    read -p "Enter a fruit (or 'quit' to exit): " fruit

    case $fruit in
        "apple")
            echo "It's an apple."
            ;;
        "banana")
            echo "It's a banana."
            ;;
        "quit")
            echo "Exiting."
            break
            ;;
        *)
            echo "Unknown fruit."
            ;;
    esac
done
```

The example above creates an interactive loop that prompts the user to enter a fruit. The `case` statement handles different fruit options, allowing the user to quit the loop by entering "quit".

The `case` statement is a powerful tool for handling multiple conditions efficiently in your Bash scripts. Experiment with different patterns and combinations to suit your specific use cases.

Certainly! Here's an extended section in the Markdown notes covering how to use the `at` command to schedule the execution of a script in Bash:

## Scheduling Script Execution with `at`

The `at` command is used to schedule the one-time execution of commands or scripts at a specified time in the future. It's a handy tool for automating tasks to run at a later time without the need for a continuous running process like a cron job.

### Basic Usage

To schedule the execution of a script using the `at` command, follow these steps:

1. **Write Your Script**: Create a Bash script that you want to execute later.

2. **Use the `at` Command**: Use the `at` command followed by the desired execution time to schedule the script.

```bash
#!/bin/bash

# Scheduling script execution with at
echo "bash /path/to/your/script.sh" | at 10:00 AM tomorrow
```

In the example above, the script will be executed at 10:00 AM on the next day.

### Specifying Date and Time

You can specify the exact date and time for execution in various formats:

```bash
#!/bin/bash

# Scheduling script execution with at on a specific date and time
echo "bash /path/to/your/script.sh" | at 2023-08-15 15:30
```

### Reading Commands from a File

If your script is more complex or requires multiple lines of code, you can place the commands in a file and use the `-f` flag to read from the file.

```bash
#!/bin/bash

# Create a file containing your commands
echo "echo 'Script executed at $(date)'" > my_script_commands.sh

# Schedule execution using the file
at 10:00 AM tomorrow -f my_script_commands.sh
```

### Viewing Scheduled Jobs

You can view your scheduled `at` jobs using the `atq` command:

```bash
#!/bin/bash

# View scheduled at jobs
atq
```

### Removing Scheduled Jobs

To remove a scheduled job, use the `atrm` command followed by the job ID:

```bash
#!/bin/bash

# Remove a scheduled at job
atrm <job_id>
```

### Notes

- The `at` command might not be available on all systems by default. You may need to install it or ensure it's enabled.
- The exact syntax and available options may vary depending on your system. Always refer to the man page (`man at`) or documentation specific to your system for accurate usage.

Using the `at` command, you can easily schedule the execution of your scripts at specific times, making it a useful tool for automation and task scheduling.

Of course! Here's an extended section in the Markdown notes covering how to use the `crontab` command to schedule the execution of scripts or commands in Bash:

## Scheduling Tasks with `crontab`

The `crontab` command is used to manage and schedule periodic tasks on Unix-like operating systems. These tasks, also known as cron jobs, can be scheduled to run at specific intervals, times, or days of the week.

### Basic Usage

To schedule the execution of a script or command using the `crontab` command, follow these steps:

1. **Write Your Script**: Create a Bash script that you want to schedule for execution.

2. **Use the `crontab` Command**: Use the `crontab` command to create or edit your cron jobs.

```bash
#!/bin/bash

# Schedule script execution using crontab
crontab -e
```

This will open the default text editor where you can define your cron jobs.

### Defining a Cron Job

A cron job is defined using a specific syntax in the crontab file. The syntax is as follows:

```
* * * * * command_to_be_executed
```

Each asterisk represents a time unit, such as minute, hour, day of the month, month, and day of the week. You can use numbers, commas, dashes, and asterisks to specify the timing.

```bash
#!/bin/bash

# Example of a cron job: run script.sh every day at 3:30 PM
30 15 * * * bash /path/to/your/script.sh
```

In the example above, the script will be executed every day at 3:30 PM.

### Common Time Units

- `*`: Wildcard, matches any value.
- `0-59`: Minutes (0 to 59).
- `0-23`: Hours (0 to 23).
- `1-31`: Day of the month (1 to 31).
- `1-12`: Month (1 to 12).
- `0-6`: Day of the week (0 for Sunday, 6 for Saturday).

### Special Characters

- `*/n`: Runs the command every `n` units (e.g., `*/5` for every 5 minutes).
- `@hourly`, `@daily`, `@weekly`, `@monthly`, `@yearly` `@reboot`: Predefined shortcuts for common intervals.

### Editing and Viewing Cron Jobs

To edit your cron jobs, use the `-e` flag with `crontab`:

```bash
#!/bin/bash

# Edit cron jobs
crontab -e
```

To view your current cron jobs:

```bash
#!/bin/bash

# View current cron jobs
crontab -l
```

### Removing Cron Jobs

To remove your cron jobs, use the `-r` flag with `crontab`:

```bash
#!/bin/bash

# Remove all cron jobs
crontab -r
```

### Notes

- The `crontab` command and syntax may vary slightly between different Unix-like systems. Always refer to the man page (`man 5 crontab`) or documentation specific to your system for accurate usage.

Using the `crontab` command, you can schedule and automate repetitive tasks or script executions at specified intervals, providing a powerful tool for task automation.

## Tmux
| **Session Management** |                           |
|------------------------|---------------------------|
| Start a new session     | `tmux`                    |
| Start a named session   | `tmux new-session -s session_name` |
| Attach to a session     | `tmux attach-session -t session_name` |
| List all sessions       | `tmux ls`      |
| Detach from session     | `Ctrl-b` + `d`            |

| **Windows**             |                           |
|------------------------|---------------------------|
| Create a new window     | `Ctrl-b` + `c`            |
| Switch to next window   | `Ctrl-b` + `n`            |
| Switch to prev window   | `Ctrl-b` + `p`            |
| List all windows        | `Ctrl-b` + `w`            |
| Rename current window   | `Ctrl-b` + `,`            |
| Close current window    | `Ctrl-b` + `&`            |

| **Panes**               |                           |
|------------------------|---------------------------|
| Split horizontally      | `Ctrl-b` + `%`            |
| Split vertically        | `Ctrl-b` + `"`            |
| Switch to next pane     | `Ctrl-b` + `o`            |
| Close current pane      | `Ctrl-b` + `x`            |
| Move the current pane left| `Ctrl-b` + `{`     |
| Move the current pane right| `Ctrl-b` + `}`     |

| **General**             |                           |
|------------------------|---------------------------|
| Command prompt          | `Ctrl-b` + `:`            |
| Reload configuration    | `tmux source-file ~/.tmux.conf` |
| Exit tmux               | `exit`                    |

### Bash script to turn on venv and run mainscript

```sh
#!/bin/bash
which python3
cd /home/praveenrajrs/Desktop
pwd
activate() {
. /home/praveenrajrs/venv/bin/activate
}
activate
which python3
python3 test.py
```

### SSH
1. ssh-keygen
2. ssh-keygen -t ed25519.pub -C raj
3. ssh-add <private_key>
4. ssh -i <private_key> user@ip_address

#### SSH Config

```
Host host1
	HostName: <ip_address>
	User: <username>
	IdentityFile ~/.ssh/<private_key>
```

so, `ssh host1`
