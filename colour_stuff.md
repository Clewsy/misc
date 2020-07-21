
# Example of coloured prompt:
```shell
$ vim ~/.bashrc
```
Edit PS1 definition.
```shell
PS1 = "\[\033[1;31m\]\u:\w\$\[\033[0m\] "
#      ^^^^^^^     ^^                    Begin/end ANSI escape
#             ^^^^^                      "light red foreground"
#                    ^^^^^^^             Your original prompt
#                           ^^^^^^^^^^^  Reset color back to default foreground
#
```

# Another Example
This gives user and host in yellow, '@', ':' and working dir in red, prompt '$' reset to white.
```shell
PS1='${debian_chroot:+($debian_chroot)}\[\033[01;33m\]\u\[\033[01;31m\]@\[\033[01;33m\]\h\[\033[01;31m\]:\w\[\033[00m\]\$ '
```

# Colours:
```shell
txtblk='\e[0;30m' # Black - Regular
txtred='\e[0;31m' # Red
txtgrn='\e[0;32m' # Green
txtylw='\e[0;33m' # Yellow
txtblu='\e[0;34m' # Blue
txtpur='\e[0;35m' # Purple
txtcyn='\e[0;36m' # Cyan
txtwht='\e[0;37m' # White
bldblk='\e[1;30m' # Black - Bold
bldred='\e[1;31m' # Red
bldgrn='\e[1;32m' # Green
bldylw='\e[1;33m' # Yellow
bldblu='\e[1;34m' # Blue
bldpur='\e[1;35m' # Purple
bldcyn='\e[1;36m' # Cyan
bldwht='\e[1;37m' # White
unkblk='\e[4;30m' # Black - Underline
undred='\e[4;31m' # Red
undgrn='\e[4;32m' # Green
undylw='\e[4;33m' # Yellow
undblu='\e[4;34m' # Blue
undpur='\e[4;35m' # Purple
undcyn='\e[4;36m' # Cyan
undwht='\e[4;37m' # White
bakblk='\e[40m'   # Black - Background
bakred='\e[41m'   # Red
bakgrn='\e[42m'   # Green
bakylw='\e[43m'   # Yellow
bakblu='\e[44m'   # Blue
bakpur='\e[45m'   # Purple
bakcyn='\e[46m'   # Cyan
bakwht='\e[47m'   # White
txtrst='\e[0m'    # Text Reset
```

# Function to demo colours:
```shell
function colorgrid( )
{
    iter=16
    while [ $iter -lt 52 ]
    do
        second=$[$iter+36]
        third=$[$second+36]
        four=$[$third+36]
        five=$[$four+36]
        six=$[$five+36]
        seven=$[$six+36]
        if [ $seven -gt 250 ];then seven=$[$seven-251]; fi

        echo -en "\033[38;5;$(echo $iter)m█ "
        printf "%03d" $iter
        echo -en "   \033[38;5;$(echo $second)m█ "
        printf "%03d" $second
        echo -en "   \033[38;5;$(echo $third)m█ "
        printf "%03d" $third
        echo -en "   \033[38;5;$(echo $four)m█ "
        printf "%03d" $four
        echo -en "   \033[38;5;$(echo $five)m█ "
        printf "%03d" $five
        echo -en "   \033[38;5;$(echo $six)m█ "
        printf "%03d" $six
        echo -en "   \033[38;5;$(echo $seven)m█ "
        printf "%03d" $seven

        iter=$[$iter+1]
        printf '\r\n'
    done
}
```

# Create coloured "image" that is printable in the terminal
1. Need to install viu to convert image file: https://github.com/atanunq/viu/releases
2. Create a cat-able file (use -t to preserve transparency in png files).
```shell
$ viu -t image.png > image.txt
```
3. This text file will have literal escape codes (hex value 0x1B).  Need to convert to "\033" for use in bash scripting.
```shell
$ viu -t image.png | sed 's/x1b\[/\x5c\x30\x33\x33\[/g' > image.txt
```
Note 'g' in the sed expression to capture all instances of ox1B in a line instead of just the first.
Also note, echo-ing output txt file like this:
```shell
$ echo -e $(cat image.txt)
```
will not properly show newlines.  Modify viu / sed command to add in newlines:
```shell
$ viu -t image.png | sed 's/\x1b\[/\x5c\x30\x33\x33\[/g' | sed 's/$/\\n/' > image.txt
```
I.e. at end of line ('$') add newline ("\n").

4. Can now print from bash script:
```shell
$ echo -e $(cat image.txt)
```

5. For use in /etc/update-motd.d/99-image motd generation script, limit width to 80.  I,e, use:
```shell
$ viu -t image.png -w 80 | sed 's/\x1b\[/\x5c\x30\x33\x33\[/g' > motd_image
```

# Reference:
https://en.wikipedia.org/wiki/ANSI_escape_code#Colors

