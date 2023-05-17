# Arguments
| Arg identifier | Description                       |
| -------------- | --------------------------------- |
| $0             | The name of the script itself, which is often used in usage statements.       |
| $1             | A positional argument, which is the first argument passed to the script.       | 
| ${10}          | Where two or more digits are needed to represent the argument position. Brace brackets are used to delimit the variable name from anyother content. Single value digits are expected. |
| $#             | The argument count is especially useful when we need to set the amount of arguments needed for correct script execution. |
| $*             | Refers to all arguments. |
| $?             | Get the return status.   |

### Arrays
- Declare: `myarray=(one two three four)`
- Print: `echo ${myarray[0]}; echo ${myarray[*]} #prints all`
- Remove: `unset array[1]; unset array #remove all elements`

# awk
- `awk ' { print $0 }' /etc/passwd #prints first entire line`
- `awk ' { print $1 }' /etc/passwd #prints first field (space separated)`
- `awk -F":" '{ print $1 }' /etc/passwd #colon separated or awk ' BEGIN { FS=":" } { print $1 } ' /etc/passwd`
- `awk ' BEGIN { FS=":" } { print $1 } END { print NR } ' /etc/passwd #prints a line counter at the end`
- `awk ' NR<3 ' file #prints to third line`
- `awk ' NR==3 ' file #prints third line`
- `awk ' /bash$/ ' /etc/passwd #regular expressions`
- Variables
  - **FIELDWIDTHS**: Specifies the field width
  - **RS**: Specifies the record separator
  - **FS**: Specifies the field separator
  - **OFS**: Specifies the output separator, which is a space by default
  - **ORS**: Specifies the output separator
  - **FILENAME**: Holds the processed file name
  - **NF**: Holds the line being processed
  - **FNR**: Holds the record which is processed
  - **IGNORECASE**: Ignores character case
- `awk 'BEGIN{FS="\n"; RS=""} {print $1,$3}' myfile # field separator is new line, record separator is empty, records 1 and 3`
- `awk 'BEGIN {FS="\n"} {print $1,"FNR="FNR,"NR="NR} END{print "Total lines:",NR}' myfile `
- `awk 'BEGIN { var=2; print var }' #defining own variables`
- `awk '{if ($1 > 50) print $1}' myfile #if on records`
- `awk '{if ($1 > 50) print $1 * 2; else print $1 * 3}' myfile #if else`
- `awk '{
total = 0
for (var = 1; var < 4; var++)
{
total += $var
}
mean = total / 3
print "Mean value:",mean
}' myfile #for loop`
- To reuse a awk command. Save in file.awk and then `awk -f file.awk myfile`
- REGEX:
  - `awk ' ( $9 ~ /404/ ) { print $10 } ' access.log #search 404 on field 9 an display 10`
  - `awk ' ( $9 !~ /^https:\/\/www\.yourdomain\.com/ ) { print $10 } ' access.log #search not REGEX on field 9 an display 10`
  - `{ myarray[$2]++ } END { for ( b in myarray) print b, "has appeared: ", myarray[b] } #file.awk count ocurrences and print them`
  - `awk ' $0 ~ search { print }'  search=ERROR server.log #searches and print a line ERROR (search is a variable)`

# Conditionals
- Command **test**: `test expression`, `test ! expression #negation`, `test expression -o expression2 #or`, `test expression -a expression2 #and`
- Bracket conditional: `[ $HOME = /home/javier ]`, `[ ! $HOME = /home/javier ]`, 
- Others: `[ -n $SSH_TTY ] #If this is true, then the connection is made with SSH`, `[ -z $1 ] #A true result for this query means that no input parameters have been supplied to the script`
- Test Integers: `[ number1 -gt number2] #-eq -ge -le -lt -ne`

### Test files
- **-d** This shows that it's a directory
- **-e** This shows that the file exists in any form
- **-x** This shows that the file is executable
- **-f** This shows that the file is a regular file
- **-r** This shows that the file is readable
- **-p** This shows that the file is a named pipe
- **-b** This shows that the file is a block device
- **file1 -nt file2** This checks if file1 is newer than file2
- **file1 -ot file2** This checks if file1 is older than file2
- **-O file** This checks if the logged-in user is the owner of the file
- **-c** This shows that the file is a character device
- **-o** or clause **test -f file -o -e file**
- **-a** and clause **test -f file -a -e file**

### If else
```bash
if condition; then
  statement
else
  statement
fi
```

### Check Strings
- `if [ string1 \< string2 ] #if string1 is less than string2` 
- `if [ string1 \> string2 ] #if string1 is greater than string2` 
- `if [ -n string1 ] #if string1 is longer than zero` 
- `if [ -z string1 ] #if string1 has zero length` 

# Clipboard
- To copy: `cat file | xclip -i`
- To paste: `xclip -o`
- To append: `echo lala | xsel -a`

# Disks and file systems
- Disk usage: `df`
- Mount on directory: `mount /dev/sda1 /mnt/mydir`
- Check file system: `fsck -f /dev/sda10`

# Debug
- Verbose: `bash -v script.sh`
- Executed: `bash -x script.sh`

# Files
- Display file name only: `basename file`
- Display absolute path of a file without filename: `dirname file`
- Create override: `command > outfile`
- Append: `command >> outfile`
- Redirect possible error: `command 2> errorfile`
- Data plus possible error, single file: `command &> outfile`
- Reverse pipe: `grep content <(cat file)`

### File properties
- File info: `stat file`
- Disk usage: `du file`
- Type of a file: `file filename`

### File location
- Find file: `find . -type f -name filename`
- Find directory: `find . -type d -name dirname`
- Execute commmand from input: `find . -type f -print | xargs grep -l tomato`
- To find executables, docs, etc: `whereis command`

### File manipulation
- Cut file fields: `cut -c1 filename`
- Paste two files: `paste file1 file2`
- Translate some chars o others: `cat file | tr 'a-z' 'A-Z'`
- Delete chars: `cat file | tr -d 'A-Z'`
- Order: `sort file`
- Copy output to file: `echo some_test | tee newfile`

### File comparision
- Compare two files: `diff file1 file2`
- Compare two directories recursively: `diff -r dir1 dir2`
- Compare binary files: `cmp file1 file2`

# Functions
- To check functions: **declare -F**
```bash
testing() {
  local myvar=10
  return $var
}
testing
```

# grep
- `grep -i word # Search ignore case`
- `grep -c word # Search word and return count` 
- `grep -A2 word # Search word and 2 lines after it` 

# Heading
```bash
#!/bin/bash
# Author: ...
# Web: ...
# Description...
# within $HOME
# Last Edited: Month Day Year
```
# IFS
- By default is a space
- Change IFS to be a new line: **IFS=$'\n'**
- Change IFS to be a comma separated: **IFS=","**

# Input
- Read: `read; echo "result: $REPLY"`
- Read: `read -p "name: " var_name` 
- Read: `read -n1 -p "Press any key to exit" # n1 number of chars accepted or -sn1 to not seeing the entered text` 

# Jobs
- List current jobs: `jobs`
- Run job in background: `job file &`
- Suspend a foreground job: Ctrl+z
- Send a suspended job to run in the bg: `bg %job_number`
- Send a suspended job to run in the fg: `fg %job_number`
- Delay a command: `sleep 10 && echo Hello`
- Execute a program every interval of time: `watch -n 30 ls`
- Execute at specific time: 
```bash
at 7am next sunday
at> echo Remember to go shopping | mail smith
at> lpr $HOME/shopping-list
at> ^D
<EOT>
job 559 at 2022-09-14 21:30
```
- Cron tasks: `crontab`

# Links
- Hard link (if sfile is deleted, tfile works): `ln sfile tfile`
- Symbolic link (if sfile is deleted, tfile points to nothing): `ln -s sfile tfile`
- To find where a symbolic link is pointing: `readlink mylink`

# Loops
- Classic loop
```bash
for loopVar in values; do
echo $loopVar
done
```
- C-Style loop redirecting the output
```bash
for (( var = 1; var < 3; var++ )); do
echo $var
done > file.txt
```
- While to read a file
```bash
while read server; do
echo $server
done < servers.txt
```

# Maths
- Simple calc: `expr 10 + 10`
- Calculator: bc

# Parameter Substitution
- ${parameter-default}
- Substituing a possible empty parameter:
```bash
#!/bin/bash
#Use parameter substitution to provide default value
name=${1-"Anonymous"}
echo "Hello $name"
exit 0
```
# Print
- Interpolation: `echo "Hello $1"` -> Hello ...
- Literals: `echo 'Hello $1'` -> Hello $1
- Mixed: `echo "Hello $USER \$1"` -> Hello javier $1
- Echo with escape sequence: `echo -e "hello \c"`
- Echo without new line: `echo -n "hello"`

# Regular Expressions
- **[[:alpha:]]** Matches any alphabetical character
- **[[:upper:]]** Matches A-Z uppercase only
- **[[:lower:]]** Matches a-z lowercase only
- **[[:alnum:]]** Matches 0-9, A-Z, or a-z
- **[[:blank:]]** Matches space or Tab only
- **[[:space:]]** Matches any whitespace character: space, Tab, CR
- **[[:digit:]]** Matches from 0 to 9
- **[[:print:]]** Matches any printable character
- **[[:punct:]]** Matches any punctuation character
- **?** matches de existent or not of the preceding character (in sed -r, in grep -E)
- **+** matches de existent of the preceding character one time or more. It must exists at least once (in sed -r, in grep -E)
- **{1}** defines the number of existence of the preceding character (in sed -r, in grep -E)
- **word|word2** matches one word or another (in sed -r, in grep -E)
- **(word word2)** matches words (in ser -r, in grep -E) 

# Processes
- Find pid: `pidof programname`
- Execute with timeout: `timeout 3 yourprogram # stop after 3 seconds`

# Standard Options
- **-a** List all items
- **-c** Get a count of all items
- **-d** Output directory
- **-e** Expand items
- **-f** Specify a file
- **-h** Show the help page
- **-i** Ignore the character case
- **-l** List a text
- **-o** Send output to a file
- **-q** Keep silent; don't ask the user
- **-r** Process something recursively
- **-s** Use stealth mode
- **-v** Use verbose mode
- **-x** Specify an executable
- **-y** Accept without prompting me

# SED
- `sed -n '1,3 p' /etc/passwd #prints lines 1 to 3`
- `sed -n '/^root/ p' /etc/passwd #prints line starting with root`
- `sed s/pattern/replacement/flag #substitute flags: p (print), g (global), w (sends result to file)`
- `sed -n ' /^pi/ s/bash/sh/p ' /etc/passwd #replace bash with sh searching with pi`
- `sed -n ' /^pi/ s@/bin/bash@/usr/bin/sh@p ' /etc/passwd #replacements with / directories`
- `sed '2s/old text/new text/' myfile #modify second line`
- `sed '2,3s/old text/new text/' myfile #modify second to third line`
- `sed '2,$s/old text/new text/' myfile #modify second to end of file`
- `sed -i ' /^pi/ s@/bin/bash@/bin/sh/ ' $HOME/passwd #edit the file`
- `sed -i.bak ' /^pi/ s@/bin/bash@/bin/sh/ ' $HOME/passwd #edit the file and make a backup`
- `sed -i '3d' file #delete third line`
- `sed -i '1,3d' file #delete first to third line`
- `sed -i '2i\inserted text' myfile #insert second line`
- `sed -i '2a\inserted text' myfile #append second line`
- To reuse a sed command. Save in file.sed and then `sed -f file.sed myfile`

# Text colors
- \033 is the escaped character and 31/32 the color
```bash
RED="\033[31m"
GREEN="\033[32m"
echo -e ${RED}Error
```

# Users & Groups
- Create user: `sudo useradd username -g groupname`
- Delete user: `sudo userdel username`
- Modify user: `sudo usermod -d /home/another username`
- Generate password: `sudo passwd username`
- List groups: `groups # groupadd, groupdel, groupmod`

# Variables
- `name="fdfas"`, `name=12`

### Environment variables
- Show: `printenv`

### Execute arithmetic 
```bash
count=0
(( count++ ))
echo $count
```
### Set commands in a variable
- `myvar=$(pwd)`
