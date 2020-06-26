# Shell
Shell cheatsheet (most should work in both Bash and Zsh).


## Redirections
```
cmd > file              # write stdout to file
cmd >> file             # append stdout to file
cmd 2&> file            # stderr to file (/dev/null)
cmd &> file             # stdout+stderr to file
cmd 2&>1 > file         # stdout+stderr to file
cmd 2&>1 | tee file     # stdout+stderr to console and file
cmd < file              # feed stdin from file
```

## Variables
#### Special
```
$?                      # exit status of last command
$!                      # PID of last background command
$$                      # PID of shell
$0                      # filename of shell script
```

#### Default values
```
${var:-Test}            # $var or "Test" if $var is unset/null
${var:=Test}            # set $var to "Test" it if unset/null
${var:+Test}            # yield "Test" if $val is set and not null
${var:?Error message}   # print "Error message" and exit if $val unset/null
```

#### Length
```
${#var}                 # length of variable
```

#### Slicing
```
${var:FROM:LENGTH}
${var:2}          st    # from 2 to end
${var:0:2}        Te    # 2 characters from 0
${var:0:-1}       Tes   # from 0 to length-1
${var:(-1)}       t     # form length-1 to end
${var:(-3):2}     es    # 2 characters from length-3
```

#### Substitution
```
${var#PREFIX}           # remove shortest matching preffix
${var##PREFIX}          # remove longest matching preffix
${var%SUFFIX}           # remove shortest matching suffix
${var%%SUFFIX}          # remove longest matching suffix
${var/FROM/TO}          # replace first FROM with TO
${var//FROM/TO}         # replace all FROMs with TOs
${var/#FROM/TO}         # replace prefix FROM with TO
${var/%FROM/TO}         # replace suffix FROM with TO
${var,}                 # lowercase first character
${var,,}                # lowercase all characters
${var^}                 # uppercase first character
${var^^}                # uppercase all characters
```


## Conditions
#### Basic
```
[ -z STRING ]           # empty string
[ -n STRING ]           # non-empty string
[ STRING == STRING ]    # string equality (==, !=)
[ STRING ~= REGEX ]     # regular expression match
[ NUM -eq NUM ]         # number equality (eq, ne, lt, gt, le, ge)
```

#### Files
```
[ -e FILE ]             # exists
[ -r FILE ]             # readable
[ -w FILE ]             # writable
[ -x FILE ]             # executable
[ -s FILE ]             # size > 0 bytes
[ -f FILE ]             # file
[ -d FILE ]             # directory
[ -h FILE ]             # symlink
[ FILE1 -ef FILE2 ]     # FILE1 and FILE2 are same file
[ FILE1 -nt FILE2 ]     # FILE1 is newer than FILE2
[ FILE1 -ot FILE2 ]     # FILE1 is older than FILE2
```


## Loops
#### Loop over files
```
for I in /path/* ; do
  echo $I               # /path/file
done
```

#### Loop over range
```
for I in {FROM..TO} ; do
  echo $I
done

for I in {FROM..TO..STEP} ; do
  echo $I
done
```

#### Loop over lines in file
```
cat file | while read I ; do
  echo $I
done
```
