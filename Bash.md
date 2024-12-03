# Learning Bash <!-- omit in toc -->

> Learning Bash using coding exercices.

<p align='center'>
  <img src="./imgs/bash_logo.svg" width="415" height="197"/>
</p>

<p style = 'line-height: 20px'>
  I use <a href="https://exercism.org/"><img src = './imgs/exercism.png' style='vertical-align: bottom' width="20" /> Exercism</a> which is an open-source, free coding platform that offers code practice and mentorship on 74 different programming languages.
</p>

## Table of Contents <!-- omit in toc -->

- [Setup](#setup)
- [Exercises](#exercises)
  - [**Exercise 01** - Hello World 👋](#exercise-01---hello-world-)
  - [**Exercise 02** - Two Fer 🎫](#exercise-02---two-fer-)
  - [**Exercice 03** - Error Handling ⛔](#exercice-03---error-handling-)
  - [**Exercice 04** - Raindrops 💧](#exercice-04---raindrops-)
  - [**Exercice 05** - Hamming 🧬](#exercice-05---hamming-)
  - [**Exercice 06** - Acronym 🔤](#exercice-06---acronym-)
  - [**Exercice 07** - Armstrong Numbers 👨‍🚀](#exercice-07---armstrong-numbers-)
  - [**Exercice 08** - Pangram 🦊](#exercice-08---pangram-)
  - [**Exercice 09** - Bob 🤠](#exercice-09---bob-)
  - [**Exercice 10** - Scrabble Score 🔠](#exercice-10---scrabble-score-)
  - [**Exercice 11** - Grains 🌽](#exercice-11---grains-)
  - [**Exercice 12** - Luhn 💳](#exercice-12---luhn-)
  - [**Exercice 13** - Atbash Cipher 🗝️](#exercice-13---atbash-cipher-️)
  - [**Exercice 14** - Reverse String 🧵](#exercice-14---reverse-string-)
  - [**Exercice 15** - Leap 📅](#exercice-15---leap-)
  - [**Exercice 16** - Resistance Color Duo ⚡⚡](#exercice-16---resistance-color-duo-)
  - [**Exercice 17** - Secret Handshake 🤝](#exercice-17---secret-handshake-)
  - [**Exercice 18** - Darts 🎯](#exercice-18---darts-)
  - [**Exercice 19** - D\&D Character 🐉](#exercice-19---dd-character-)
  - [**Exercice 20** - Matching Brackets \[{}\]](#exercice-20---matching-brackets-)
  - [**Exercice 21** - Proverb 🏰](#exercice-21---proverb-)
  - [**Exercice 22** - Resistance Color Trio ⚡⚡⚡](#exercice-22---resistance-color-trio-)
  - [**Exercice 23** - Sieve 🗑️](#exercice-23---sieve-️)
  - [**Exercice 24** - Grep 🔎](#exercice-24---grep-)
  - [**Exercice 25** - Tournament ⚽](#exercice-25---tournament-)
  - [**Exercice 26** - Bowling 🎳](#exercice-26---bowling-)
  - [**Exercice 27** - OCR Numbers 🎫](#exercice-27---ocr-numbers-)
  - [**Exercice 28** - Clock 🕓](#exercice-28---clock-)
  - [**Exercice 29** - Markdown 📄](#exercice-29---markdown-)
  - [**Exercice 30** - Rectangles 🧮](#exercice-30---rectangles-)
  - [**Exercice 31** - House 🏠](#exercice-31---house-)
  - [**Exercice 32** - Nucleotide Count 🧬](#exercice-32---nucleotide-count-)
  - [**Exercice 33** - Rotational Cipher 🌀](#exercice-33---rotational-cipher-)
  - [**Exercice 34** - Binary Search 🔎](#exercice-34---binary-search-)
  - [**Exercice 35** - Kindergaten Garden 🌱](#exercice-35---kindergaten-garden-)
  - [**Exercice 36** - Robot Simulator 🤖](#exercice-36---robot-simulator-)
  - [**Exercice 37** - Run-Length Encoding 🔠](#exercice-37---run-length-encoding-)
  - [**Exercice 38** - Transpose 🔠](#exercice-38---transpose-)
  - [**Exercice 39** - Yacht 🚤](#exercice-39---yacht-)
- [📁 **Ressources**](#-ressources)


## Setup

I've set it up on `WSL2` and editing via `Visual Studio Code` using the following guides:

- [VSCode : Remote development in WSL.](https://code.visualstudio.com/docs/remote/wsl-tutorial)
- [Exercism : Learn how to solve exercises on your local machine](https://exercism.org/docs/using/solving-exercises/working-locally)

## Exercises

> Recording my solutions and personal notes. Might do some more traditional shell scripting to learn how to interact with the OS.

### **Exercise 01** - Hello World 👋
```bash
echo "Hello, World!"
```

### **Exercise 02** - Two Fer 🎫
```bash
echo "One for ${1:-you}, one for me."
```

> - Access arguments.
> - `1` refers to the first argument.
> - You can define a default value with the syntax : `VAR=${1:-DEFAULTVALUE}` 

### **Exercice 03** - Error Handling ⛔
```bash
if [[ $# -eq 1 ]]
then
    echo "Hello, $1"
else
    { echo "Usage: error_handling.sh <person>"; exit 1; }
fi
```

> - Set a condition relating the number of arguments.

### **Exercice 04** - Raindrops 💧
```bash
(( $1 % 3 )) || result+="Pling"
(( $1 % 5 )) || result+="Plang"
(( $1 % 7 )) || result+="Plong"
echo "${result:-$1}"
```

> - Set an arithmetic condition.
> - `||` or ***OR*** runs the command on the right if the one on the left returns ***false***.
> - the `%` operator computes the remainder of the division : returns `0 (false)` if  divisible, else returns a `non-zero value (true)`. 

### **Exercice 05** - Hamming 🧬
> Calculate the Hamming distance between two DNA strands.
```bash
hamming=0

if [[ $# -ne 2 ]]
then
    { echo "Usage: hamming.sh <string1> <string2>"; exit 1; }
fi

if [ ${#1} -eq ${#2} ]
then
    for((i=0;i<${#1};i++)); do
        if [[ "${1:i:1}" != "${2:i:1}" ]];
        then
            ((hamming++))
        fi
    done
echo "$hamming"
else
    { echo "strands must be of equal length"; exit 1; }
fi
```

> - For loop.
> - Get character from string.

*Other solution without so many if statements*
```bash
main () {
  (( ${#*} < 2 )) && echo "Usage: hamming.sh <string1> <string2>" && exit 1
  (( ${#1} != ${#2} )) && echo "strands must be of equal length" && exit 1
  local diff=0
  local i
  for (( i=0; i<${#1}; i++ )); do
    [ "${1:$i:1}" != "${2:$i:1}" ] && (( diff++ ))
  done
  echo $diff
}
main "$@"
```

### **Exercice 06** - Acronym 🔤
> Convert a phrase to its acronym.
```bash
main () {
    (( ${#*} != 1 )) && echo "Usage: acronym.sh <string1>" && exit 1

    RESULT=""
    IFS=' -*_'
    read -ra elements <<< "$1"

    for element in "${elements[@]}"; do
        RESULT+="${element:0:1}"
    done
    
    echo "${RESULT^^}" ## uppercase the string.
}

main "$@"
```

> - Splitting a string.

### **Exercice 07** - Armstrong Numbers 👨‍🚀
> Determine whether a number is an Armstrong number.
```bash
main(){
    (( ${#*} != 1 )) && echo "Usage: armstrong_numbers.sh <number1>" && exit 1
    
    SUM=0

    for (( i=0; i<${#1}; i++ )); do
        SUM=$((SUM + $((${1:$i:1} ** ${#1}))))
    done

    if [[ $1 -eq $SUM ]];then
        echo "true"
    else
        echo "false"
    fi
}

main "$@"
```

> - Parsing digits of a number.
> - Sum : `$((num1 + num2))`
> - Power : `$((2 ** 4))`

### **Exercice 08** - Pangram 🦊
> Determine whether a sentence is a pangram.

```bash
main () {
    (( ${#*} != 1 )) && echo "Usage: pangram.sh <sentence1>" && exit 1
    SENTENCE="${1,,}" ## to lowercase
    LIST="abcdefghijklmnopqrstuvwxyz"
    COUNT=0
    for (( k=0; k<${#SENTENCE}; k++ )); do ## for each character in sentence
        for (( i=0; i<${#LIST}; i++ )); do ## look for in the alphabet
            ## if in the alphabet, increment count & pop the letter out of the alphabet
            if [[ "${SENTENCE:k:1}" == "${LIST:i:1}" ]]; then
                LIST="${LIST::i}${LIST:i+1}"
                ((COUNT++))
                break ## don't need to continue comparing to other letters in the alphabet
            fi
        done
        if [[ COUNT -eq 26 ]]; then
            echo "true"
            exit 0
        fi
    done
    echo "false"
}
main "$@"
```
> - Pop character at index from string.
> - Break out of loop.

*Other more elegant solution*
```bash
alphabet="abcdefghijklmnopqrstuvwxyz" # set the alphabet
pangram_candidate="${1,,}"            # set the candidate
# get outta here letters && I love Bash built-ins
zero_check="${alphabet//[$pangram_candidate]/}"
# if zero_check is empty then the candidate was a pangram
[[ -z $zero_check ]] && echo 'true' || echo 'false'
```

### **Exercice 09** - Bob 🤠
> What will Bob reply ?  

```bash
main () {

    # 1. ? = Sure
    # 2. ABC = Whoa
    # 3. ABC + ? = Calm down
    # 4. "   " = Fine
    # 5. else = Whatever

    CAPS=${1^^}
    [[ "$1" =~ [A-Za-z] ]] && letters=true || letters=false
    trimmed_input="${1%"${1##*[![:space:]]}"}"

    if [[ "${trimmed_input: -1}" == "?" ]]; then
        if [[ $1 == "$CAPS" ]] && $letters; then
            echo "Calm down, I know what I'm doing!"
        else
            echo "Sure."
        fi
        exit 0
    fi

    [[ ! $1 = *[![:space:]]* ]] && echo "Fine. Be that way!" && exit 0
    [[ $1 == "$CAPS" ]] && $letters && echo "Whoa, chill out!" && exit 0
    echo "Whatever."
}

main "$@"
```

> - Check if string has alphabetical characters.
> - Check last non-whitespace character.
> - Check empty/blank string. *(⚠️ special characters like \t \n \r)*

### **Exercice 10** - Scrabble Score 🔠
> Compute the Scrabble score of a word.

```bash
main () {
    SCORE=0
    WORD="${1^^}"

    if [ ${#1} -gt 0 ]
    then
        for((i=0;i<${#1};i++)); do
            [[ "${WORD:i:1}" =~ [AEIOULNRST] ]] && SCORE=$((SCORE + 1)) && continue
            [[ "${WORD:i:1}" =~ [DG] ]] && SCORE=$((SCORE + 2)) && continue
            [[ "${WORD:i:1}" =~ [BCMP] ]] && SCORE=$((SCORE + 3)) && continue
            [[ "${WORD:i:1}" =~ [FHVWY] ]] && SCORE=$((SCORE + 4)) && continue
            [[ "${WORD:i:1}" =~ [K] ]] && SCORE=$((SCORE + 5)) && continue
            [[ "${WORD:i:1}" =~ [JX] ]] && SCORE=$((SCORE + 8)) && continue
            [[ "${WORD:i:1}" =~ [QZ] ]] && SCORE=$((SCORE + 10)) && continue
        done
    fi
    echo "$SCORE"
}

main "$@"
```

> - Character in list of characters *(Regex)*.

### **Exercice 11** - Grains 🌽
> Calculate the number of grains of wheat on a chessboard given that the number on each square doubles.

```bash
main () {
    (( ${#*} != 1 )) && echo "Usage: grains.sh <number1>" && exit 1

    if (($1 >= 1 && $1 <= 64)); then
        printf "%llu\n" $((2 ** $(($1 - 1))))
    elif [[ $1 == "total" ]];then
        printf "%llu\n" $((2 ** 64-1))
    else
        echo "Error: invalid input" && exit 1
    fi
}

main "$@"
```

> - Handling 64 bit integer limitation.

### **Exercice 12** - Luhn 💳
> Determine whether a number is valid per the Luhn formula.

```bash
main () {
    # Check if digits only (! whitespaces)
    # start sum
    # parse from right
    # if k%2 = 0, sum += string[k] * 2  (-9 if>9)
    # if sum%10 -> true

    isLuhn=false
    string="${1// /}"

    if [[ ${#string} -gt 1 ]];then

        if [[ "${1// /}" =~ ^[0-9]+$ ]]; then

            sum=0

            for (( i=0; i<${#string}; i++ )); do
                toAdd=${string:(-i-1):1}
                ! (( i % 2 )) || toAdd=$((${string:(-i-1):1} * 2))
                ! (( toAdd > 9)) || toAdd=$((toAdd - 9))

                sum=$(( sum + toAdd))
            done

            (( sum % 10)) || isLuhn=true

        fi
    fi
    echo "$isLuhn"
}

main "$@"
```

> How does `[[ "${count// /}" =~ ^[0-9]+$ ]]` work ?
> 1. `${count// /}`:  
> - This is a parameter expansion. It removes all spaces (`" "`) from the value of the variable `count`. The syntax `//` indicates replacing all occurrences of the space with nothing (i.e., removing it).
> 2. `=~`:  
> - This operator checks whether the string on the left side matches the regular expression on the right side.
> 3. `^[0-9]+$`:
> 	- This is a regular expression:
> 		- `^` means the start of the string.
> 		- `[0-9]` matches any digit (0 through 9).
> 		- `+` means one or more of the preceding element (digits in this case).
> 		- `$` means the end of the string.
> 		
> 	- So, `^[0-9]+$` matches a string that consists entirely of one or more digits, with no other characters.

*Other solution*
```bash
quit() {
	echo false
	exit
}
str="$*"
number="${str// /}"
[[ $number =~ ^[0-9]*$ ]] || quit
[[ ${#number} -gt 1 ]] || quit
declare -i sum=0 digit
for ((i = 1; i <= ${#number}; i++)); do
	digit=${number:$((-i)):1}
	((i % 2 == 0)) && ((digit *= 2)) && ((digit > 9)) && ((digit -= 9))
	((sum += digit))
done
((sum % 10 == 0)) && echo true || echo false
```

### **Exercice 13** - Atbash Cipher 🗝️
> Create an implementation of the atbash cipher, an ancient encryption system created in the Middle East.

```bash
get_char_position() {
    # Get position of character in alphabet.
    local char="$1"
    char=$(echo "$char" | tr '[:upper:]' '[:lower:]')
    echo "$(( $(printf "%d" "'$char") - 96 ))"
}


main () {
    # Add space when encoding.
    # Push character at (-index) in alphabet
    
    (( ${#*} != 2 )) &&  [[ "$1" =~ ^(decode|encode)$ ]] && echo "Usage: atbash_cipher.sh <encode/decode> <sentence1>" && exit 1

    Plain="abcdefghijklmnopqrstuvwxyz"
    string="${2// /}" && string=$(echo "$string" | tr -d '[:punct:]') && string="${string,,}"
    result=""

    for (( i=0; i<${#string}; i++ )); do
        if [[ "${string:i:1}" =~ [a-z] ]];then

            [[ "${1}" == "encode" ]] && (( i != 0 && i % 5 == 0 )) && result+=" "
            position=$(get_char_position "${string:i:1}")
            result+="${Plain:(-$position):1}"

        else result+="${string:i:1}"
        fi
    done
    echo "$result"
}

main "$@"
```

> - Call a function.
> - Some more experience with conditions.

*Other elegant solution*
```bash
main () {
    result=$( tr "abcdefghijklmnopqrstuvwxyz" "zyxwvutsrqponmlkjihgfedcba" <<< ${2,,} | tr -d " .," )
    [ "$1" == "encode" ] && result=$(fold -w5 <<< $result)
    echo $result
}
main "$@"
```

### **Exercice 14** - Reverse String 🧵
> Reverse a given string.

```bash
main () {
    (( ${#*} != 1 )) && echo "Usage: reverse_string.sh <string1>" && exit 1
    reversed=""
    for (( i=0; i<${#1}; i++)); do
        reversed+="${1:(-i-1):1}"
    done
    echo "$reversed"
}

main "$@"
```

*Other solution*
```bash
echo "$1" | rev
```

> `rev` : command to reverse lines character-wise. *(also works with files to reverse each line)*

### **Exercice 15** - Leap 📅
> Determine whether a given year is a leap year.

```bash
main () {
    (( ${#*} != 1 )) || [[ ! "$1" =~ ^[0-9]+$ ]] && echo "Usage: leap.sh <year>" && exit 1
    (($1 % 4 == 0)) && (( ( ($1 % 100 == 0) && ($1 % 400 == 0) ) || !($1 % 100 == 0) )) && echo "true" || echo "false"
}

main "$@"
```

> - Check if integer argument.
> - Some more experience with conditions.

*Other solutions*
- Better boolean expression :
```bash
(( year % 4 == 0 && (year % 100 != 0 || year % 400 == 0) ))
```
- Ternary operator of Boolean expressions :
```bash
(( year % 100 == 0 ? year % 400 == 0 : year % 4 == 0 ))
```
- External tools :
```bash
year=$1
next_day=$(date -d "$year-02-28 + 1 day" '+%d')
[[ $next_day == "29" ]] && echo true || echo false
```

***Which one to choose ?***
- The chain of Boolean expressions should be the most efficient, as it proceeds from the most likely to least likely conditions. It has a maximum of three checks. It is the most efficient approach when testing a year that is not evenly divisible by `100` and is not a leap year, since the most likely outcome is eliminated first.
- The ternary operator has a maximum of only two checks, but it starts from a less likely condition.
- Using external tools to do `datetime` addition may be considered a "cheat" for the exercise, and it will be slower than the other approaches.

### **Exercice 16** - Resistance Color Duo ⚡⚡
> What is the resistance value ?

```bash
main () {

    colors=("black" "brown" "red" "orange" "yellow" "green" "blue" "violet" "grey" "white")
    index1=-1
    index2=-1

    for (( i=0 ; i<${#colors[@]} ; i++));do
        if [[ "${colors[$i]}" == "$1" ]]; then index1=$i; fi
        if [[ "${colors[$i]}" == "$2" ]]; then index2=$i; fi
    done

    if [[ "$index1" -ne -1 && "$index2" -ne -1 ]]; then
        index=$(echo "$index1$index2" | sed 's/^0//')
        echo "$index"
    else
        echo "invalid color" && exit 1
    fi
}

main "$@"
```

> - Basic array manipulations.

*Other solution*  

```bash
declare -ir black=0 brown=1 red=2 orange=3 yellow=4 green=5 blue=6 violet=7 grey=8 white=9
[[ -z ${!1} || -z ${!2} ]] && echo "invalid color" && exit 1
echo $(( ${!1}*10 + ${!2} ))
```

### **Exercice 17** - Secret Handshake 🤝
> Secret handshake.

```bash
main () {

    (( ${#*} != 1 )) && echo "Usage: secret_handshake.sh <number1>" && exit 1
    ! (($1 >= 0 && $1 <= 31)) && echo "Usage: secret_handshake.sh <number1>" && exit 1
    
    binary=$(printf "%b" "$(echo "obase=2; $1" | bc)")
    actions=("wink" "double blink" "close your eyes" "jump" "reverse")
    todo=""

    for((i=0;i<${#binary};i++)); do
        if [[ "${binary:(-i-1):1}" == "1" ]];
        then
            [[ $todo == "" ]] && todo+="${actions[$i]}" || todo+=",${actions[$i]}"
        fi
    done

    [[ "$todo" =~ "reverse" ]] && todo="${todo/, reverse$//}" && todo=$(echo "$todo" | awk -F',' '{ for(i=NF-1; i>0; i--) printf "%s%s", $i, (i>1 ? "," : "")}')
    echo "$todo"
}

main "$@"
```

> - Binary transformation.
> - Using an array.
> - The command `${todo/, reverse$//}` is a [**parameter expansion**](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html), it look for the substring `", reverse` at the **end** *(`$`)* of the string and **removes** it *(`//`)*.

> How does `echo "$todo" | awk -F ...` work :
> 1. `echo "$todo"`: Outputs the current value of `$todo`.
> 2. `|`: The pipe sends the output of `echo "$todo"` to `awk` for further processing.
> 3. `awk -F','`: This tells `awk` to treat the comma `,` as the field separator. This splits the `$todo` string into separate fields (words) based on commas.
> 4. `{ for(i=NF-1; i>0; i--) printf "%s%s", $i, (i>1 ? "," : "") }`: This loop iterates over the fields in reverse order (starting from `NF-1`, which is the second-to-last field, and going down to 1):
>    	- **`NF`** is the **number of fields** in the string (based on commas).
>   	- The `printf` command prints each field in reverse order.
>   	- The `(i>1 ? "," : "")` part ensures that a comma is added **only between the words** (not at the end).

### **Exercice 18** - Darts 🎯
> Calculate the points scored in a single toss of a Darts game.

```bash
main () {
    (( ${#*} != 2 )) || ! [[ "$1" =~ ^-?[0-9]+(\.[0-9]+)?$ ]] || ! [[ "$2" =~ ^-?[0-9]+(\.[0-9]+)?$ ]] && echo "Usage: darts.sh <x> <y>" && exit 1

    squared=$(bc <<< "$1 * $1 + $2 * $2")
    dist=$(echo "scale=2; sqrt($squared)" | bc -l)

    if (( $(echo "$dist <= 1.0" |bc -l) )); then echo "10"
    elif (( $(echo "$dist <= 5.0" |bc -l) )); then echo "5"
    elif (( $(echo "$dist <= 10.0" |bc -l) )); then echo "1"
    else echo "0" 
    fi
}

main "$@"
```

> - Float operations.

*Other solution more compact*

```bash
die () { echo "$1"; exit 1; }
(( $# != 2 )) && die "Invalid arg count"
for i; do [[ $i = *[^[:digit:].-]* ]] && die "Non-numeric arg"; done
bc <<< "scale=4 
        x=$1 ; y=$2 ; d=sqrt(x^2 + y^2 )
        if (d <= 1) 10 else if (d <= 5) 5 else if (d <= 10) 1 else 0"
exit 0
```

### **Exercice 19** - D&D Character 🐉
> Write a random D&D character generator.

```bash
modifier () {
    number=$(( $1 - 10 ))
    number=$(echo "$number" | awk '{print ($1 < 0) ? int($1 / 2) - ($1 % 2 != 0) : int($1 / 2)}')
    echo "$number"
}

roll () {
    # Roll 4 dices and sums the 3 highest values.
    # I just sum all the rolls, keep the min value, and then substract the min value from the sum.
    SUM=0
    MIN=6
    for (( i=0 ; i<4;i++)); do 
        ROLL=$(echo $((1 + $RANDOM % 6)))
        SUM=$(( $ROLL + $SUM ))
        (( $ROLL < $MIN )) && MIN=$ROLL
    done
    echo "$(( $SUM - $MIN ))"
}


main () {
    if [[ "$1" == "modifier" ]]; then
        modifier $2
    elif [[ "$1" == "generate" ]]; then
        
        stats=()
        for ((i=0;i<6;i++)); do 
            stats=("${stats[@]}" $(roll))
        done
        MODIFIER=$(modifier ${stats[2]})
        hitpoints=$(( 10 + $MODIFIER ))
        printf "strength ${stats[0]}\ndexterity ${stats[1]}\nconstitution ${stats[2]}\nintelligence ${stats[3]}\nwisdom ${stats[4]}\ncharisma ${stats[5]}\nhitpoints $hitpoints\n"

    fi
}

main "$@"
```

> - Create & Use functions.
> - Generate a random number.
> - Round down a number.
> - ⚠️ `printf` vs `echo`. *(the latter automatically `\n`)*

### **Exercice 20** - Matching Brackets [{}]
> Given a string containing brackets `[]`, braces `{}`, parentheses `()`, or any combination thereof, verify that any and all pairs are matched and nested correctly.

```bash
main () {
    # We make a stack each time we open a bracket.
    # When there is a close bracket, we make sure it corresponds to the last opened, if not -> false
    # at the end if stack empty -> True ; else False
    WAITING_LIST=()

    for (( i=0 ; i<${#1}; i++ )); do

        [[ "${1:i:1}" == '(' ]] && WAITING_LIST=("${WAITING_LIST[@]}" ')')
        [[ "${1:i:1}" == '[' ]] && WAITING_LIST=("${WAITING_LIST[@]}" ']')
        [[ "${1:i:1}" == '{' ]] && WAITING_LIST=("${WAITING_LIST[@]}" '}')

        if [[ "${1:i:1}" == ')' || "${1:i:1}" == ']' || "${1:i:1}" == '}' ]]; then
            if [[ (( ${#WAITING_LIST} != 0 )) && "${1:i:1}" == "${WAITING_LIST[-1]}" ]]; then
                unset 'WAITING_LIST[${#WAITING_LIST[@]}-1]'
            else
                echo "false"
                exit 0
            fi
        fi

    done

    (( ${#WAITING_LIST[@]} == 0 )) && echo "true" || echo "false"
}

main "$@"
```

> - Pop element out of array.
> - More practice with conditions.

### **Exercice 21** - Proverb 🏰
> Given a list of inputs, generate the relevant proverb.

```bash
main () {
    
    arguments=${#*}

    (( arguments == 0 )) && echo "" && exit 0
    (( arguments == 1 )) && echo "And all for the want of a $1." && exit 0;

    for (( i=0; i<arguments-1; i++)); do  
        echo "For want of a ${*:$i+1:1} the ${*:$i+2:1} was lost."
    done

    echo "And all for the want of a $1."

}

main "$@"
```

> - Parsing list of arguments of arbitrary length.

*Other solution*
```bash
# There must be at least 2 positional parameters 
# to enter the loop:
#   `i` initialized to 1
#   `i < $#` test passes only if 2 or more parameters
for (( i=1, j=2 ; i < $# ; i++, j++ )); do
    echo "For want of a ${!i} the ${!j} was lost."
done
# And at least one parameter to print this:
[[ -n $1 ]] && echo "And all for the want of a $1." || :
```

### **Exercice 22** - Resistance Color Trio ⚡⚡⚡
> What is the resistance value ? Trio version.

```bash
main () {

    colors=("black" "brown" "red" "orange" "yellow" "green" "blue" "violet" "grey" "white")
    index1=-1
    index2=-1
    index3=-1

    for (( i=0 ; i<${#colors[@]} ; i++));do
        if [[ "${colors[$i]}" == "$1" ]]; then index1=$i; fi
        if [[ "${colors[$i]}" == "$2" ]]; then index2=$i; fi
        if [[ "${colors[$i]}" == "$3" ]]; then index3=$i; fi
    done

    if [[ "$index1" -ne -1 && "$index2" -ne -1 && "$index3" -ne -1 ]]; then
        zeros=$(( 10 ** index3))
        result=$(echo $index1$index2 | sed 's/^0//')
        result=$(( result * zeros ))

        [[ $result =~ 000000000$ ]] && echo "${result::-9} gigaohms" && exit 0
        [[ $result =~ 000000$ ]] && echo "${result::-6} megaohms" && exit 0
        [[ $result =~ 000$ ]] && echo "${result::-3} kiloohms" && exit 0
        echo "$result ohms"
    else
        echo "invalid color" && exit 1
    fi
}

main "$@"
```

> - Substring.
> - Regex.

### **Exercice 23** - Sieve 🗑️
> Implements the Sieve of Eratosthenes algorithm to find all prime numbers less than or equal to a given number.

```bash
main () {
    # Create a list to store marked numbers' positions.
    # If a number isn't marked, add it to the result and mark its multiples.
    range=$(( $1 + 1 ))
    zeros=$(printf '0%.0s' $(seq 1 $range))
    result=""

    if [[ "$1" -ge 2 ]]; then
        for (( i=2; i<range; i++ )); do
            if [[ "${zeros:i:1}" == "0" ]]; then
            
                # Loop to mark the multiples.
                j=$(( i * 2 ))
                while [[ $j -lt $range ]]; do
                    zeros="${zeros:0:j}1${zeros:j+1}"
                    j=$(( j + i ))
                done

                result+=" $i"
            fi
        done
        result="${result#"${result%%[![:space:]]*}"}"
    fi
    echo "$result"
}

main "$@"
```

> - Substring replacement.
> - `while` loop.
> - ⚠️ would be better to use arrays instead of rebuilding string each time in the `while` loop.

### **Exercice 24** - Grep 🔎
> Implement a simplified `grep` command, which supports searching for fixed strings.

```bash
main () {

    # Flags
    # -n : prepend line number and a colon
    # -i : case-insensitive comparison
    # -l : only output filenames with at least one matching line
    # -x : pattern matches exactly entire line
    # -v : invert program (collect line that fail to match)

    # Parse flags
    flag_n=0
    flag_i=0
    flag_l=0
    flag_x=0
    flag_v=0
    while getopts "nilxv" opt; do
        case "$opt" in
            n)
            flag_n=1
            ;;
            i)
            flag_i=1
            ;;
            l)
            flag_l=1
            ;;
            x)
            flag_x=1
            ;;
            v)
            flag_v=1
            ;;
            *)
            echo "Usage: $0 [-n] [-i] [-l] [-x] [-v]"
            exit 1
            ;;
        esac
    done

    # After processing flags, we process the remaining arguments
    # The one just after the flags is the pattern argument
    shift $((OPTIND - 1))
    pattern="$1"
    [[ "$flag_x" == "1" ]] && pattern="^$pattern\$" # -x : pattern matches exactly entire line

    shift
    for filename in "$@"; do
        # if multiple files, file prefix = file name + :
        (( ${#*} > 1 )) && file_prefix="$filename:" || file_prefix=""

        line_prefix="" # if flag -n, line prefix = $line_number + :
        line_number=1

        while IFS= read -r line; do
            line_to_match=$line # So not to change the line variable in case-insensitive comparison
            [[ "$flag_i" == "1" ]] && pattern=${pattern,,} && line_to_match=${line,,}

            if [[ ( "$flag_v" == "0" && "$line_to_match" =~ $pattern  ) || ( "$flag_v" == "1" && ! "$line_to_match" =~ $pattern  ) ]]; then
                [[ "$flag_n" == "1" ]] && line_prefix="$line_number:"
                [[ "$flag_l" == "1" ]] && printf '%s\n' "$filename" && break
                printf '%s%s\n' "$file_prefix$line_prefix" "$line"
            fi

            ((line_number+=1))
        done < "$filename"
    done
}

main "$@"
```

> - Parsing command line arguments using [`getopts`](https://stackoverflow.com/tags/getopts/info "https://stackoverflow.com/tags/getopts/info").
> - Read a file line by line.
> - Using `shift` to process remaining arguments.

### **Exercice 25** - Tournament ⚽
> Tally the results of a small football competition.

```bash
declare -A teams_stats

update_stats() {
    local team_name=$1
    local wins=$2
    local draws=$3
    local losses=$4
    local points=$5

    if [[ -z "${teams_stats["$team_name,wins"]}" ]]; then
        # Initialize stats if not already set
        teams_stats["$team_name,wins"]=0
        teams_stats["$team_name,draws"]=0
        teams_stats["$team_name,losses"]=0
        teams_stats["$team_name,points"]=0
        teams_stats["$team_name,matches_played"]=0
    fi

    teams_stats["$team_name,wins"]=$((teams_stats["$team_name,wins"] + wins))
    teams_stats["$team_name,draws"]=$((teams_stats["$team_name,draws"] + draws))
    teams_stats["$team_name,losses"]=$((teams_stats["$team_name,losses"] + losses))
    teams_stats["$team_name,points"]=$((teams_stats["$team_name,points"] + points))
    teams_stats["$team_name,matches_played"]=$((teams_stats["$team_name,matches_played"] + 1))
}

# Header
echo "Team                           | MP |  W |  D |  L |  P"

if [[ $# -eq 1 ]]; then
    input_file="$1"
else
    input_file="/dev/stdin"  # Default to standard input if no file argument
fi

while IFS= read -r line; do
    
    # skip empty lines
    if [[ -z "$line" ]]; then
        continue
    fi

    W=0
    D=0
    L=0
    IFS=';' read -r team1 team2 result <<< "$line"
    [[ $result == "win" ]] && team1_points=3 && team2_points=0 && W=1
    [[ $result == "draw" ]] && team1_points=1 && team2_points=1 && D=1
    [[ $result == "loss" ]] && team1_points=0 && team2_points=3 && L=1

    # (Name, W , D, L, P)
    update_stats "$team1" "$W" "$D" "$L" "$team1_points"
    update_stats "$team2" "$L" "$D" "$W" "$team2_points"

done < "$input_file"

for team in "${!teams_stats[@]}"; do
    
    if [[ "$team" == *",wins" ]]; then
        team_name="${team%%,*}"
        MP=${teams_stats["$team_name,matches_played"]}
        W=${teams_stats["$team_name,wins"]}
        D=${teams_stats["$team_name,draws"]}
        L=${teams_stats["$team_name,losses"]}
        P=${teams_stats["$team_name,points"]}

        # Use printf for formatted output
        printf "%-30s | %2d | %2d | %2d | %2d | %2d\n" "$team_name" "$MP" "$W" "$D" "$L" "$P"
    fi
done | sort -t'|' -k6,6nr -k2,2nr  # Sort by points, then by wins
```

> - Declare an associative array.
> - Key:Values manipulations. *(add and change values)*
> - Parse associative array.
> - Sort output using `sort`.

### **Exercice 26** - Bowling 🎳
> Score a bowling game.

```bash
results=()

roll () {
    (( $1 < 0 )) && echo "Negative roll is invalid" && exit 1
    (( $1 > 10 )) && echo "Pin count exceeds pins on the lane" && exit 1
    results+=("$1")
}

score () {

    final_score=0
    frame_counter=1
    frame_multiplier=1
    last_roll=0 # To check for spares.
    same_frame=false # To check for spares.
    spare_counter=0
    strike_counter=0
    double_strike=0
    bonus_expected=0

    for score in "${results[@]}"; do
        # Error if the game is already over.
        [[ $frame_counter -gt 10 ]] && [[ $bonus_expected == 0 ]] && echo "Cannot roll after game is over" && exit 1

        # Stop counting scores after the 10th frame, only bonuses are applied (from spares/strikes).
        [[ $frame_counter -gt 10 ]] && frame_multiplier=0
        
        # Score calculation
        (( final_score += score*frame_multiplier ))
        # # Handling Spares
        (( final_score += (spare_counter)*score ))
        # # Handling Strikes
        [[ $strike_counter -ne 0 ]] && ((final_score+=score))
        [[ $double_strike == 1 && $frame_counter -le 11 ]] && ((final_score+=score)) && double_strike=0

        # Resetting Counters
        spare_counter=0
        (( strike_counter-- )) || strike_counter=0
        (( bonus_expected-- )) || bonus_expected=0

        # If same frame, check if we spare.
        if [[ "$same_frame" == "true" ]]; then
            # Error if pin count > 10
            (( (score + last_roll) > 10 )) && echo "Pin count exceeds pins on the lane" && exit 1

            # Check for spare.
            # Warning : If last_score=0, and if score=10, it's a strike that needs to be counted, not a spare.
            if ((score + last_roll == 10)); then
                ((last_roll != 0)) && spare_counter=1 || strike_counter=2
            fi

            same_frame=false
            ((frame_counter++))
        else
            if [[ $score == 10 ]]; then
                [[ $strike_counter -ne 0 ]] && double_strike=1

                strike_counter=2
                ((frame_counter++))
            else
                same_frame=true # If first roll in a frame, and not a strike, then the next roll will be in the same frame.
            fi
        fi

        last_roll=$score

        # Handling Bonuses
        if [[ $frame_counter == 11 ]]; then
            [[ $spare_counter == 1 ]] && bonus_expected=1
            [[ $strike_counter == 2 ]] && bonus_expected=2
        fi
        
    done
    [[ $bonus_expected -gt 0 ]] && echo "Score cannot be taken until the end of the game" && exit 1
    [[ $frame_counter -lt 11 ]] && echo "Score cannot be taken until the end of the game" && exit 1
    echo "$final_score"
}

main () {
    (( ${#*} < 1 )) && echo "Score cannot be taken until the end of the game" && exit 1  
    for arg in "$@"; do
        roll "$arg"
    done
    score
}

main "$@"
```

> - Handling lots of conditions/use-cases.
> - I really like this expression `(( strike_counter-- )) || strike_counter=0`, which prevents decrementing into negative values.

### **Exercice 27** - OCR Numbers 🎫
> Given a 3 x 4 grid of pipes, underscores, and spaces, determine which number is represented, or whether it is garbled.

```bash
declare -A digit_map
lines=()

digit_map[" _ | ||_|   "]='0'
digit_map["     |  |   "]='1'
digit_map[" _  _||_    "]='2'
digit_map[" _  _| _|   "]='3'
digit_map["   |_|  |   "]='4'
digit_map[" _ |_  _|   "]='5'
digit_map[" _ |_ |_|   "]='6'
digit_map[" _   |  |   "]='7'
digit_map[" _ |_||_|   "]='8'
digit_map[" _ |_| _|   "]='9'

check_digit () {
    # Input  : array with four lines and three columns
    # Output : digit, if found in digit_map. else outputs '?'
    if [[ -z "${digit_map["$1"]}" ]]; then
        echo "?"
    else
        echo "${digit_map["$1"]}"
    fi
}

main () {
    # # Checking for correct input form.
    [[ -t 0 ]] || readarray -t lines

    if [ ${#lines[@]} -eq 0 ]; then
        echo ""
        exit 0
    fi

    num_rows=${#lines[@]}
    num_columns=${#lines[0]}

    # Validate number of rows and columns
    (( num_columns % 3 != 0 )) && echo "Number of input columns is not a multiple of three" && exit 1
    (( num_rows % 4 != 0 )) && echo "Number of input lines is not a multiple of four" && exit 1

    # Parsing lines to read the numbers.
    final=""

    # For each block of 4 lines
    for (( i=0; i<num_rows; i+=4 )); do
        sub_array=()
        [[ $i -gt 0 ]] && final+=","

        # For each line
        for (( k=i; k<i+4; k++ )); do
            line="${lines[$k]}"
            # For each line, we will divide it into substrings of lengths 3.
            # We will concatenate substrings at the same index from each line.

            # For each 3-character substring of the current line
            for (( j=0; j<${#line}; j+=3 )); do
                sub_string="${line:j:3}" # Extract substring of length 3
                sub_index=$(( j / 3 )) # Index in sub_array
                [[ -z "${sub_array[sub_index]}" ]] && sub_array[sub_index]="" # Initialize if empty.
                # Concatenate the current substring to the corresponding element in sub_array
                sub_array[sub_index]+="$sub_string"
            done
        done

        # Each element of the sub_array is a digit to be checked.
        for element in "${sub_array[@]}"; do
            final+="$(check_digit "$element")"
        done
    done
    
    echo "$final"
}

main "$@"
```

> - Substrings and array manipulation.
> - Parsing input text as a grid.

### **Exercice 28** - Clock 🕓
> Implement a clock that handles times without dates.

```bash
# usage: clock.sh h m [{+|-} delta]
# where:
#       h = an hour value
#       m = a minute value
# optional:
#       a time delta (in minutes) to apply to the initial clock value
#
# The clock script will output the clock value in %H:%M format

main () {

    (( ${#*} < 1 )) && echo "invalid arguments" && exit 1
    (( ${#*} > 4 )) && echo "invalid arguments" && exit 1

    # First two arguments should be numbers
    if ! [[ "$1" =~ ^-?[0-9]+$ ]] || ! [[ "$2" =~ ^-?[0-9]+$ ]]; then
        echo "invalid arguments"
        exit 1
    fi

    if [ $# -ge 3 ]; then
        # Third argument must be either + or -
        if [[ "$3" != "+" && "$3" != "-" ]]; then
            echo "invalid arguments"
            exit 1
        fi

        # Fourth argument must be a number if a third argument exists
        if [ $# -lt 4 ] || ! [[ "$4" =~ ^-?[0-9]+$ ]]; then
            echo "invalid arguments"
            exit 1
        fi
    fi

    hours=$1
    minutes=$2

    (( ${#*} > 2 )) && minutes=$(( minutes $3 $4 ))

    final_hours=$((  ( (minutes / 60 ) + hours) % 24 ))
    final_minutes=$(( minutes % 60 ))

    (( final_minutes < 0 )) && final_hours=$(( final_hours - 1 )) && final_minutes=$(( 60 + final_minutes ))
    (( final_hours < 0 )) && final_hours=$(( 24 + final_hours ))

    printf "%02d:%02d" "$final_hours" "$final_minutes"
}

main "$@"
```

> - Argument conditions.
> - Modulo.

### **Exercice 29** - Markdown 📄
> Refactor a Markdown parser.

```bash
while IFS= read -r line; do
    while true; do
        orig=$line
        if [[ $line =~ ^(.+)__(.*) ]]; then
            post=${BASH_REMATCH[2]};pre=${BASH_REMATCH[1]}
            if [[ $pre =~ ^(.*)__(.+) ]]; then
                printf -v line "%s<strong>%s</strong>%s"  "${BASH_REMATCH[1]}"  "${BASH_REMATCH[2]}"  "$post"
            fi
        fi
        [ "$line" != "$orig" ] || break
    done
    echo "$line" | grep '^\*' > /dev/null 2>&1
    if [ $? -eq 0 ]; then
        if [ X$inside_a_list != Xyes ]; then
            h="$h<ul>"
            inside_a_list=yes
        fi
        while [[ $line == *_*?_* ]]; do
            one=${line#*_}
            two=${one#*_}
            if [ ${#two} -lt ${#one} -a ${#one} -lt ${#line} ]; then
                line="${line%%_$one}<em>${one%%_$two}</em>$two"
            fi
        done
        h="$h<li>${line#??}</li>"
    else
        if [ X$inside_a_list = Xyes ]; then
            h="$h</ul>"
            inside_a_list=no
        fi
        n=`expr "$line" : "#\{1,\}"`
        if [ $n -gt 0 -a 7 -gt $n ]; then
            while [[ $line == *_*?_* ]]; do
                s=${line#*_}
                t=${s#*_}
                if [ ${#t} -lt ${#s} -a ${#s} -lt ${#line} ]; then
                    line="${line%%_$s}<em>${s%%_$t}</em>$t"
                fi
            done
            HEAD=${line:n}
            while [[ $HEAD == " "* ]]; do HEAD=${HEAD# }; done
            h="$h<h$n>$HEAD</h$n>"
        else
            grep '_..*_' <<<"$line" > /dev/null &&
                line=`echo "$line" | sed -E 's,_([^_]+)_,<em>\1</em>,g'`
            h="$h<p>$line</p>"
        fi
    fi
done < "$1"
if [ X$inside_a_list = Xyes ]; then
    h="$h</ul>"
fi
echo "$h"
```

> - Just corrected code readability.

### **Exercice 30** - Rectangles 🧮
> Count the rectangles in an ASCII diagram like the one below.

```text
   +--+
  ++  |
+-++--+
|  |  |
+--+--+
```
```bash
# Function to check for correct pairs of vertices.
potential_pairs () {
    local str=$1
    local col_index=$2
    local indexes=()
    for (( k=0; k<${#str}; k++)); do
        if [[ "${str:$k:1}" == "+" ]]; then
            real_index=$((k + col_index + 1))
            indexes+=("$real_index")
        elif [[ "${str:$k:1}" == "-" ]]; then
            continue
        else
            break
        fi
    done
    declare -p indexes
}

main () {
    [[ -t 0 ]] || readarray -t lines

    if [ ${#lines[@]} -eq 0 ]; then
        echo "0"
        exit 0
    fi

    num_rows=${#lines[@]}
    num_columns=${#lines[0]}

    declare -a current_rectangles
    declare -a new_rectangles

    final_result=0

    for (( i=0; i<num_rows; i++ )); do

    unset new_rectangles

        for (( j=0; j<num_columns-1; j++ )); do
            
            character="${lines[i]:j:1}"

            if [[ $character == "+" ]]; then
                eval "$(potential_pairs "${lines[i]:j+1}" $j)"
                for elem in "${indexes[@]}"; do
                    new_rectangles+=("$j $elem")
                done
            fi
        done

        # # # ====================
        # # # Computing Rectangles
        # # # ====================

        count=0

        # We check if the rectangles found in previous lines are completed, continue, or are interupted.
        rectangles_to_keep=()
        if [[ ${#current_rectangles[@]} -gt 0 ]]; then
            for pair in "${current_rectangles[@]}"; do
                IFS=' ' read -r index1 index2 <<< "$pair"
                char1="${lines[i]:index1:1}"
                char2="${lines[i]:index2:1}"
                # If the rectangle is completed, we add a count.
                if [[ "$char1" == "+" && "$char2" == "+" ]]; then
                    # We check that this pair is a correct pair, i.e not missing a side.
                    for elem in in "${new_rectangles[@]}"; do
                        [[ "$elem" == "$pair" ]] && ((count++)) && break
                    done
                    rectangles_to_keep+=("$pair")
                # If the rectangle is continuing, we keep it.
                elif { [[ "$char1" == "+" || "$char1" == "|" ]] && [[ "$char2" == "+" || "$char2" == "|" ]]; }; then
                    rectangles_to_keep+=("$pair")
                fi
            done
        fi

        ((final_result+=count))

        [[ ${#new_rectangles[@]} -gt 0 ]] && rectangles_to_keep+=("${new_rectangles[@]}")
        current_rectangles=("${rectangles_to_keep[@]}")

    done
    echo "$final_result"
}


main "$@"
```

> - Did a 1st solution with multiple associative arrays that didn't work well.
> - Associative arrays : conditions, parsing, and value assigning.
> - Arrays : conditions, parsing, and value assigning.
> - It's very annoying how it can be troublesome to assign the values of an array (or associative) to a new one.

### **Exercice 31** - House 🏠
> Recite the nursery rhyme 'This is the House that Jack Built'.

```bash
things=("house that Jack built." "malt" "rat" "cat" "dog" "cow with the crumpled horn" 
        "maiden all forlorn" "man all tattered and torn" "priest all shaven and shorn" 
        "rooster that crowed in the morn" "farmer sowing his corn" 
        "horse and the hound and the horn")

verbs=("lay in" "ate" "killed" "worried" "tossed" "milked" "kissed" "married" "woke" 
        "kept" "belonged to")

get_verse () {
    # Input : verse number x
    if [[ $1 == 1 ]]; then
        echo "This is the house that Jack built."
    else
        index=$(( $1 - 1 ))
        echo "This is the ${things[$index]}"
        for (( i=index-1; i>=0; i--)); do
            echo "that ${verbs[i]} the ${things[i]}"
        done
    fi
}

main () {
    
    if ! [[ $1 -ge 1 && $1 -le 12 && $2 -ge 1 && $2 -le 12 && $2 -ge $1 ]]; then
        echo "invalid"
        exit 1
    fi

    for (( j=$1; j<=$2; j++)); do
        get_verse $j
        echo ""
    done
}

main "$@"
```

*Better way to declare the two lists and conditions*
```bash
declare -a items that
items+=("house that Jack built."); that+=("")
items+=("malt"); that+=("lay in")
....
start=$1
end=$2
yeet() {
    printf '%s\n' "invalid input"
    exit 1
}
(( start <= 0 || end > 12 || start > end || end < start )) && yeet
```

### **Exercice 32** - Nucleotide Count 🧬
> Given a string representing a DNA sequence, count how many of each nucleotide is present.

```bash
check_valid () {
    input="$1"
    valid_dna="AGTC"
    invalid_characters="${input//[$valid_dna]/}"
    [[ -n $invalid_characters ]] && echo "Invalid nucleotide in strand" && exit 1
}

main () {
    nucleotides=(0 0 0 0) # A C G T
    sequence="$1"

    if [[ -n $sequence ]]; then
        check_valid "$sequence"
        ((nucleotides[0]+=$(echo "$sequence" | grep -o "A" | wc -l)))
        ((nucleotides[1]+=$(echo "$sequence" | grep -o "C" | wc -l)))
        ((nucleotides[2]+=$(echo "$sequence" | grep -o "G" | wc -l)))
        ((nucleotides[3]+=$(echo "$sequence" | grep -o "T" | wc -l)))
    fi
    
    printf "A: %d\nC: %d\nG: %d\nT: %d" "${nucleotides[0]}" "${nucleotides[1]}" "${nucleotides[2]}" "${nucleotides[3]}"
}
main "$@"
```

> - Using `grep`

### **Exercice 33** - Rotational Cipher 🌀
> Create an implementation of the rotational cipher, also sometimes called the Caesar cipher.

```bash
get_char_position() {
    # Get position of character in alphabet.
    local char="$1"
    char=$(echo "$char" | tr '[:upper:]' '[:lower:]')
    echo "$(( $(printf "%d" "'$char") - 97 ))"
}

main () {
    string="$1"
    key="$2"
    alphabet="abcdefghijklmnopqrstuvwxyz"
    result=""
    for (( i=0; i<${#string}; i++ )); do
        if [[ "${string:i:1}" =~ [A-Za-z] ]]; then
            position=$(get_char_position "${string:i:1}")
            position=$(( position + key ))
            position=$(( position % 26 ))
            toAdd="${alphabet:(position):1}"
            [[ "${string:i:1}" =~ [A-Z] ]] && toAdd="${toAdd^^}"
            result+="$toAdd"
        else result+="${string:i:1}"
        fi
    done
    echo "$result"
}

main "$@"
```

### **Exercice 34** - Binary Search 🔎
> Implement a binary search algorithm.

```bash
main () {
    to_find="$1"
    shift
    list=("$@")

    [[ ${#list[@]} -eq 0 ]] && echo "-1" && exit 0

    final_index=0
    not_found=1
    while [[ ${#list[@]} -gt 0 && $not_found -eq 1 ]]; do

        index=$(( ${#list[@]} / 2 ))
        element="${list[$index]}"

        if (( element == to_find )); then
            ((final_index+=index))
            not_found=0

        elif (( to_find < element )); then
            list=("${list[@]:0:$((index))}")

        elif (( element < to_find )); then
            list=("${list[@]:$((index+1))}")
            ((final_index+=index+1))
        fi

        [[ ${#list[@]} -eq 0 ]] && final_index=-1 && break
    done

    echo "$final_index"
}

main "$@"
```

> - Looked easy but was a bit harder than what I originally thought.
> - Read and slice array.
> - Keep meaningful index.

*Could be more readable using left, middle and right variables.*  
*Could also be made recursively.*  

### **Exercice 35** - Kindergaten Garden 🌱
> Given a diagram, determine which plants each child in the kindergarten class is responsible for.

```bash
children=("Alice" "Bob" "Charlie" "David" "Eve" "Fred" "Ginny" "Harriet"
          "Ileana" "Joseph" "Kincaid" "Larry")

declare -A plants

plants["V"]="violets"
plants["C"]="clover"
plants["R"]="radishes"
plants["G"]="grass"

get_child_index () {
    for i in "${!children[@]}"; do
        if [[ "${children[$i]}" == "$1" ]]; then
            echo "$i"
            break
        fi
    done
}

main () {

    diagram="$1"
    child="$2"

    diagram="${diagram//$'\n'/}"
    len="${#diagram}"

    index=$(get_child_index "$child")
    
    result="${diagram[*]:$((index*2)):2}"
    result+="${diagram[*]:$((len/2 + index*2)):2}"

    echo "${plants[${result:0:1}]} ${plants[${result:1:1}]} ${plants[${result:2:1}]} ${plants[${result:3:1}]}"
}

main "$@"
```

*Read-only associative array initialization*
```bash
declare -rA plants=(
    [G]=grass [C]=clover [R]=radishes [V]=violets
)
```

### **Exercice 36** - Robot Simulator 🤖
> Write a robot simulator.

```bash
directions=( "north" "east" "south" "west" )

process_command () {
    x="$1"
    y="$2"
    direction="$3"
    command="$4"

    if [[ "$command" == "R" ]]; then # Turn right
        for i in "${!directions[@]}"; do
            if [[ "${directions[$i]}" == "$direction" ]]; then
                new_direction_index=$((i + 1))
                new_direction_index=$((new_direction_index % 4))
                break
            fi
        done
        direction="${directions[$new_direction_index]}"

    elif [[ "$command" == "L" ]]; then # Turn left
        for i in "${!directions[@]}"; do
            if [[ "${directions[$i]}" == "$direction" ]]; then
                new_direction_index=$((i - 1))
                break
            fi
        done
        direction="${directions[$new_direction_index]}"

    elif [[ "$command" == "A" ]]; then # Advance
        [[ "$direction" == "north" ]] && ((y++))
        [[ "$direction" == "south" ]] && ((y--))
        [[ "$direction" == "east" ]] && ((x++))
        [[ "$direction" == "west" ]] && ((x--))
    fi
    echo "$x $y $direction" 
}

main () {

    x="${1:-0}"
    y="${2:-0}"
    direction="${3:-north}"

    [[ ! " ${directions[@]} " =~ " ${direction} " ]] && echo "invalid direction" && exit 1

    shift 3
    instructions="$@"

    if [[ -n $instructions ]]; then
        [[ ! "$instructions" =~ ^[LRA]+$ ]] && echo "invalid instruction" && exit 1
        for (( k=0; k<${#instructions}; k++ )); do
            read x y direction <<< $(process_command "$x" "$y" "$direction" "${instructions:k:1}")
        done
    fi

    echo "$x $y $direction"
}

main "$@"
```

### **Exercice 37** - Run-Length Encoding 🔠
> Implement run-length encoding and decoding.

```bash
main () {
    
    (( ${#*} != 2 )) &&  [[ "$1" =~ ^(decode|encode)$ ]] && echo "Usage: run_length_encoding.sh <encode/decode> <sentence1>" && exit 1

    string="$2"
    result=""

    if [[ "${1}" == "encode" ]]; then
        char=""
        count=0
        for (( i=0; i<${#string}; i++ )); do

            if [[ "${string:i:1}" == "$char" ]]; then
                ((count++))

            else
                (( count > 1 )) && result+="$count"
                result+="$char"

                char="${string:i:1}"
                count=1
            fi
        done
        # Adding last character
        (( count > 1 )) && result+="$count"
        result+="$char"
    fi

    if [[ "${1}" == "decode" ]]; then
        count=""
        for (( i=0; i<${#string}; i++ )); do
            char="${string:i:1}"

            if [[ "$char" =~ [0-9] ]]; then
                count+="$char"
            else
                [[ -n $count ]] && result+=$(printf "%${count}s" | tr " " "$char") || result+="$char"
                count=""
            fi
        done
    fi

    echo "$result"
}

main "$@"
```

> - Repeat a character x times.

### **Exercice 38** - Transpose 🔠
> Given an input text, output it transposed.

```bash
declare -a transposed

main () {

    row=0
    while IFS= read -r line; do
        for (( i=0; i<${#line}; i++ )); do
            char="${line:i:1}"

            spaces=""
            len=${#transposed[i]}
            missing=$(( row - len ))
            (( missing > 0 )) && spaces=$(printf "%${missing}s" | tr " " " ")

            transposed[i]+="$spaces$char"
        done
        ((row++))
    done

    for elem in "${transposed[@]}"; do
        echo "$elem"
    done
}

main "$@"
```

### **Exercice 39** - Yacht 🚤
> Score a single throw of dice in the game Yacht.

```bash
declare -A distinct

sum () {
    sum=0
    for elem in "${rolls[@]}"; do
        ((sum+=elem))
    done
    echo "$sum"
}

count () {
    for elem in "${rolls[@]}"; do
        [[ -n "${distinct["$elem"]}" ]] && ((distinct["$elem"]+=1)) || distinct["$elem"]=1 
    done
}

full_house () {
    fullhouse=0
    for key in "${!distinct[@]}"; do
        [[ "${distinct[$key]}" == "2" || "${distinct[$key]}" == "3" ]] && fullhouse=1
        break
    done
    [[ ${#distinct[@]} -eq 2 && "$fullhouse" == "1" ]] && sum || echo "0"
}

four_kind () {
    kind=0
    result=0
    for key in "${!distinct[@]}"; do
        (( ${distinct[$key]} >= 4 )) && kind=1 && result=$((key * 4))
    done
    [[ ${#distinct[@]} -le 2 && "$kind" == "1" ]] && echo "$result" || echo "0"
}

yacht () {
    [[ "${rolls[0]}" == "${rolls[1]}"
    && "${rolls[1]}" == "${rolls[2]}"
    && "${rolls[2]}" == "${rolls[3]}"
    && "${rolls[3]}" == "${rolls[4]}" ]] && echo "50" || echo "0"
}

sames () {
    same="$1"
    count=0
    for elem in "${rolls[@]}"; do
        (( elem == same )) && ((count+=same))
    done
    echo "$count"
}

main () {

    category="$1"
    shift
    rolls=("$@")

    if [[ "$category" == "yacht" ]]; then yacht
    elif [[ "$category" == "ones" ]]; then sames 1
    elif [[ "$category" == "twos" ]]; then sames 2
    elif [[ "$category" == "threes" ]]; then sames 3
    elif [[ "$category" == "fours" ]]; then sames 4
    elif [[ "$category" == "fives" ]]; then sames 5
    elif [[ "$category" == "sixes" ]]; then sames 6
    elif [[ "$category" == "full house" ]]; then { count; full_house;}
    elif [[ "$category" == "four of a kind" ]]; then { count; four_kind;}
    elif [[ "$category" == "little straight" ]]; then
        count
        [[ "${distinct[1]}" == "1" && "${distinct[2]}" == "1"
        && "${distinct[3]}" == "1" && "${distinct[4]}" == "1"
        && "${distinct[5]}" == "1" ]] && echo "30" || echo "0"
    elif [[ "$category" == "big straight" ]]; then
        count
        [[ "${distinct[6]}" == "1" && "${distinct[2]}" == "1"
        && "${distinct[3]}" == "1" && "${distinct[4]}" == "1"
        && "${distinct[5]}" == "1" ]] && echo "30" || echo "0"
    elif [[ "$category" == "choice" ]]; then sum
    fi
}

main "$@"
```

## 📁 **Ressources**

- [How to learn bash.](https://exercism.org/docs/tracks/bash/learning)  
- [Bash shortcuts for maximum productivity.](https://skorks.com/2009/09/bash-shortcuts-for-maximum-productivity/)  
- [Bash scripting cheatsheet.](https://devhints.io/bash)  
- [Good bash tutorials.](https://www.baeldung.com/linux/bash-variable-is-numeric)  