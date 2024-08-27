#programming-language 


Bash Shell

[[GIT]]
[[Regular Expression]]
[[Terminal]]

`CLI` Command Line Interface
- Reliable, easy for automation

Shortcuts|
:---|:----
Tab|Auto-complete
Cmd + K|clear
Up / Down Arrow Key|History
q|quit

[Common Terminal Commands by bradtraversy](https://gist.github.com/bradtraversy/cc180de0edee05075a6139e42d5f28ce)

```bash
# for comment 

"" double quote 
'' single quote 

"Hello, my name is $myname" # Hello, my name is $Jay 
'Hello, my name is $myname' # Hello, my name is $myname

files=$(ls) #sub shell?

env # show all environment variable
echo $PATH

whoami # show current user

date # show data

history # show command history

man #  show the user manual of any command 
man git
```
![[date.png]]

<br>

```bash
# show preferred shell
echo $SHELL #/bin/bash → Bash Shell

which bash # show bash path
/bin/bash # use bash

\'  
\"
```

<br>

### Bash Script
`#!` → shebang, which interpreter to run the script
bash script not necessarily end with `.sh` 

```shell
#!/bin/bash
echo Hello World
```

```bash
# execute .sh script
bash xxx.sh

# Mac, give permission to be executable
chmod u+x xxx.sh
```


<br>
### Arguments
Each space is new argument
Positional argument `$1` `$2` `$3` ...

```shell
echo "First arg: $1"
echo "Second arg: $2"

# all argument, exclude the first
$@
$*

# number of argument
$#
```

```bash
if [ $2 - lt 21 ]; then # -lt less than
	echo ""
fi

if [ $2 - lt 21 ]; then # -lt less than
	echo ""
else
	echo ""
fi

#-eq # equal
```


### Flags
Flag opt - option

```shell
#!/bin/bash

a_flag=''
b_flag=''
files=''
verbose='false'

print_usage() {
	printf "Usage: ..."
}

while getopts 'abf:v' flag; do
	case "${flag}" in
		a) a_flag='true' ;;
		b) b_flag='true' ;;
		f) files="${OPTARG}" ;;
		v) verbose='true' ;;
		*) print_usage
			exit 1 ;;
	esac
done
```

```bash
# running parallel in background
command_1 &
command_2 &
command_3 &
```


```shell
# open webpage MacOS 
open https://stackoverflow.com
```

### Variable
```bash
echo Hello World # string
echo "Hello World" # string
echo $Hello_World # variable
echo $variable_does_not_exist # empty

# VARIABLE
# no space
MY_LOCATION_FROM=/my/location/from
MY_LOCATION_TO=/my/location/to

```

```bash
# move
mv 

# copy, only directory
cp /my/location/from /my/location/to
cp $MY_LOCATION_FROM $MY_LOCATION_TO

# -R recursive, copy every files
cp -R ie_js/docs/api docs_scripting/
```

```shell
~ → home dir
cat → print file
```

```bash
clear # clear code / shortcut -> command + K / command + L
reset # reset shell

ls # list storage
ls -la # list all files
ls -lh # show more info

ls -l # long
# permission string
```
![[ls-l.png]]
``` bash
pwd # print working directory
open #

$(pwd)

cd # change directory
cd . # current directory
cd .. # parent directory (Back directory)
cd ~ # home user directory
cd - # to pre directory

pushd # pushd ie_js cd to ie_js
popd # return to pre dir

touch test_file.txt # CG creat test_file.txt or replace if the file already exis
nano test_file.txt # text editor
history # show history
mkdir test_directory # create folder
rm test_file.txt # remove
rmdir test_directory # remove folder, the folder need to be empty
rm -r directory # remove directory / folder anyways

# copy
cp the_original.txt the_new.txt
cp /Users/chenjingfu/pymel.log /Users/chenjingfu/Desktop/xxx.log

# to base64
echo  'linuxhint.com' | base64
```
<br>

### exit
```bash
exit
# variables are gone

# show last command exit code
echo $?

0 -> successful
other number -> failed
```

<br>

### Save to log, redirect output to file

```bash
echo "Hello World" >> package.log
echo "text" >> build/computer.txt # write "text" into the txt file
```

![[redirect_output.png]]

<br>

### Math

```bash
expr 30 + 10
expr 2 \* 3 # multiply
```

<br>

### `grep` Global Regular Expression

```bash
grep "John" names.txt # search text of "John" in names.txt
grep searchword test.txt
grep searchworl * # all file

-v # reverse
-n # show line number
-c # count, number of time appears
-i # not case sensitive, default is case sensitive
-r # recursively search
-ri <- combination
```

```bash
rsync
```

<br>
  
### Check directory exists

```bash
directory=/etc

if [ -d $directory ]
then
	echo "The directory $directory exists."
else
	echo "The directory $directory doesn't exist."
fi
```


<br>

### Where to save the script
Filesystem Hierarchy Standard (FHS) -> 
`user/bin`
can run the script anyway
file extension is not required in Linux system

add usr/local/bin to PATH if is not in:
`export PATH=/usr/local/bin:$PATH`




### History

`GNU` is a Unix-like operating system

> [The Linux Command Handbook – Learn Linux Commands for Beginners by Flavio Copes](https://www.freecodecamp.org/news/the-linux-commands-handbook/)
> 
> Many different kind of shells were created for those systems over time, and a few of them dominate the space: Bash, Csh, Zsh, Fish and many more!
> 
> All shells originate from the Bourne Shell, called `sh`. "Bourne" because its creator was Steve Bourne.
> 
> Bash means _Bourne-again shell_. `sh` was proprietary and not open source, and Bash was created in 1989 to create a free alternative for the GNU project and the Free Software Foundation. Since projects had to pay to use the Bourne shell, Bash became very popular.

`sh` Bourne Shell *⤷ Steve Bourne*
`Bash` Bourne-again shell
Csh, Zsh

<br>