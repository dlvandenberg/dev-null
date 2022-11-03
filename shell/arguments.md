# Positional arguments
To specify arguments which are parsed based on their position in the argument list, use `$0` to `$9`. 

## Example
Script: 
`greetings.sh`
```bash
#!/bin/bash

name=$1
age=$2

echo "Hello $name! You are $age years old."
```

Calling the script:
```bash
$ ./greetings.sh Dennis 33

Hello Dennis! You are 33 years old.
```

The order of the given arguments matter! 

# Optional arguments (flags)
To support optional arguments, or _flags_, you can use the built-in `getopts` function.

## Example
```bash
while getopts "vfhb:" option ; do
	case "$option" in
		f)
			echo "force flag is set"
			;;
		b)
			branch=$OPTARG
			echo "branch flag is set with $branch"
			;;
		v)
			VERBOSE=1
			;;
		h | ?)
			_print_usage
			exit 0
			;;
	esac
done

shift $((OPTIND -1))
```


## Usage
The usage of `getopts` is:
```bash
getopts <optstring> <name>
```
Where:
- `optstring` is a string containing the possible flags. If a flag requires an argument, it is denoted by placing a colon (`:`) after the flag letter. **The argument must be given directly after the flag, separated by a space**.
	-  The argument value can be retrieved using the built-in `$OPTARG` variable.
- `name` is the name of the variable that will get the value of the parsed argument option. This changes throughout the `while` loop.

To determine the parsed flag, a [[case]] statement is used. 

After parsing the arguments, the following line will shift the position of the argument parser to right after the given flags: 
```bash
shift $((OPTIND -1))
```
