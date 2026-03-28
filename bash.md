### Shebang #!/...
- telling shell script which intepreter should be used (i.e. `/bin/bash`)

### shellscipt.sh user execution permission
`chmod u+x shellscript.sh`

### Variables
- `MY_LOCATION_FROM=/my/location/from`
- `MY_LOCATION_TO=/my/location/to`

Example Usage:
- `cp $MY_LOCATION_FROM $MY_LOCATION_TO`
- `cp "$MY_LOCATION_FROM/here" "$MY_LOCATION_TO/there"`

### Positional arguments
``` bash
echo Hello $1 $2
```
``` bash
shellscript.sh arg1 arg2
```

### Piping
- the | Symbol forwards the output from the command before the symbol into the command after the symbol

Example usage:
- ls -l /usr/bin | grep bash

### Output redirection
- `>`: symbol to write to a file
- `>>`: append to a file

Example usage:
``` bash
echo Hello World! > hello.txt
```
``` bash
echo Hello World! >> hello.txt
```

### Input redirection:
- feeding input into a command
- `<`: collect input from a file
- `<<`: collect input from multiple lines of text
- `<<<`: collect input from a single string of text

Example usage:
``` bash
wc -w < hello.txt
```
``` bash
cat << EOF<PRESS ENTER> ... bla <ENTER> bla <ENTER> bla <ENTER> ... EOF<PRESS_ENTER> <- END
```
``` bash
wc -w <<< "Hello wordcount!"
```

### Test operators
- Take a cuple of arguments and shows if the expression is true or not

Example usage:
``` bash
[ bash = bash ]
```
make sure values are nummerical:
``` bash
[ 1 -eq 0 ]
```

### Get output of last executed command
``` bash
echo $?
```

### If/Elif/Else
``` bash
#!/bin/bash

if [ ${1,,} = lab ]; then
    echo "Oh you're the boss here. Welcome!"
elif [ ${1,,} = help ]; then
    echo "Just enter your username, duh!"
else
    echo "I don't know who you are. But you're not the boss of me!"
fi
```

### Case statements
- Better than if/elif/else when
  - checking for multiple values
  - easier to read
```bash
#!/bin/bash

case ${1,,} in
        lab | administrator)
                echo "Hello, you're the boss here!"
                ;;
        help)
                echo "Just enter your username!"
                ;;
        *)
                echo "Hello there. You're not the boss of me. Enter a valid username!"
esac
```

### Arrays
define an array:
``` bash
MY_ARRAY=(one two tree four five)
```
get first element of array:
``` bash
echo $MY_ARRAY
```
get all elements:
``` bash
echo ${MY_ARRAY[@]}
```
get index element:
``` bash
echo ${MY_ARRAY[3]}
```

### For Loop
```bash
for item in ${MY_ARRAY[@]; do echo -n $item | wc -c; done}
```

### Functions
- `local` means the variable is only accessible inside this function (local variable)
- `showname()` shows positional arguments usage in functions
``` bash
#!/bin/bash

showuptime(){
        local up=$(uptime -p | cut -c4-)
        local since=$(uptime -s)
        cat << EOF

-----
This machine has been up for ${up}
It has been running since ${since}
-----
EOF
}

showname(){
        echo hello $1
}

showuptime
showname lab
```

### Exit Codes
``` bash
#!/bin/bash

showname(){
        echo hello $1
        if [ ${1,,} = lab ]; then
                return 0
        else
                return 1
        fi
}
showname $1
if [ $? = 1 ]; then
        echo "Someone unknown called the function!"
fi
```

### AWK
- outputfiltering and reformatting
``` bash
# create a testfile with 3 words with space seperator (awk's default mode)
echo one two tree > testfile.txt

# get first word
awk '{print $1}' testfile.txt

# get second word
awk '{print $2}' testfile.txt

# change seperator in awk, now using ','
awk -F, '{print $1}' csvtest.csv

# pipe commands into awk
echo "Just get this word: Hello" | awk '{print $5}'

# pipe commands into awk using other seperator
echo "Just get this word: Hello" | awk -F: '{print $2}' | cut
```

### SED
- modify values in a textfile using regular expressions
- example replaces all 'fly' words in a textfile with the word 'grasshopper'
  - `s`: choose mode. here: `substitute`
    - substitute the next word behind the forward slash `fly` with the word after the second forward slash `grasshopper`
    - `g`: do this globally -> means the entire textfile
- `-i` flag creates a backup file with the original content.
```
sed -i.ORIGINAL 's/fly/grasshopper/g' sedtest.txt
```
