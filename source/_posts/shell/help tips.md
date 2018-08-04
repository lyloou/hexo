## help tips
```sh
#!/bin/bash

help(){
cat << HELP
usage: dd ddk 
example: 'wowo wowo'
HELP
exit 0
}

if [[ $1 == "" || $1 == "-h" ]]; then
	echo 'what?'
	help
fi

if [[ $1 != "" ]]; then
	echo $1
fi

echo -e "\033]0;$1\007"
```

## read from terminal
```sh
echo input your name:
read name
echo your name is ${name}
```