# Make
GNU Make cheatsheet.

## Rules
```
target: prereq... | order-only-prereq...
    recipes
```


## Special Targets and Prerequisities
#### Targets
```
.PHONY: prereq...       # run prereqs unconditionally
.SUFFIXES: s...         # list of suffixes to check for in suffix rules
.DEFAULT:               # used when given target is not found
```

#### Prerequisities
```
: .IGNORE               # ignore errors
: .SILENT               # don't output anything
: .PRECIOUS             # don't delete target and intermediate files
```


## Variables
```
var =                   # set value
var :=                  # set (recursively expand value)
var ::=                 # set (non-recursively expand value)
var +=                  # append value
var ?=                  # set value only if var is not set yet
override var [:,::,+,?]= # override command line set var assignment
private var [:,::,+,?]= # don't inherit var in prereqs
export                  # export all variables to child processes
export var              # export var to child process
undefine var            # undefine
```

## Automatic Variables
```
$@                      # name of target
$<                      # name of first prereq
$^                      # space-delimited names of all prereqs (no dupes)
$+                      # space-delimited names of all prereqs
$*                      # implicit rule stem
$%                      # name of target member name
```
NOTE: To extract directory or filename use `$(@D)` or `$(@F)` (for all above).


## Functions
#### Files and Directories
```
$(abspath str...)       # get canonical name (no ., .., symlinks) of each str
$(realpath str...)      # get canonical name (no ., .., //) of each str
$(basename str...)      # extract all but suffix of each str
$(dir str...)           # get directory (before last /) part of each str
$(notdir str...)        # get file part (after last /) of each str
$(addprefix p, str...)  # add prefix p to each str
$(addsuffix s, str...)  # add suffix s to each str
$(wildcard p)           # get existing file names that match p
```

#### Strings
```
$(subst f, t, str)      # replace f with t in str
$(patsubst p, r, str)   # replace words matching p with r in str
$(var:p=r)              # replace words matching p with r in var
$(strip str)            # strip leading/trailing whitespaces from str
$(filter p..., str)     # get words from str that match any of p
$(filter-out p..., str) # get words from str that do not match any of p
$(sort list)            # sort list in lexical order (remove dupes)
$(join l1, l2)          # join lists l1 and l2
$(words str)            # get number of words in str
$(word n str)           # get n-th word of str, empty if out of bounds
```

#### Conditionals and Loops
```
$(if c,t,f)             # evaluate c; if non-empty evaluate t else f
$(foreach v, l, str)    # for each word v in l evaluate str
```

#### Misc
```
$(shell cmd)            # run cmd in sub-shell, return output
$(file m, f, str)       # open file f in mode m and write str into it
$(call v, pN...)        # evaluate v substituting {N}s by pNs
```

#### Output
```
$(error msg...)         # output fatal error msg
$(warning msg...)       # output warning msg
$(info msg...)          # output info msg
```
