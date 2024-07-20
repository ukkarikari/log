# log
very simple and rudimentary logging function for my .bashrc

## usage

add a new line to your log
```
$ log i am doing this right now
```
see last 5 logs 
```
$ log -ls
```
see all logs
```
$ log -less
```
undo the last line you added 
```
$ log undo
```

## usage example
```
$ log fixed something
 [2024-07-20 15:17] fixed something
$ log fixed something else
 [2024-07-20 15:17] fixed something
 [2024-07-20 15:18] fixed something else
$ log -undo
 [2024-07-20 15:17] fixed something
 -- last log deleted --
```

## installation
add this to your .bashrc
```
log() {
	local arg="$1"
	shift

	if [ "$arg" = "-undo" ]; then

		sed -i '$d' $HOME/log-file
		tail -n 5 $HOME/log-file
		echo " -- last log deleted --"

	elif [ "$arg" = "-ls" ]; then
		tail -n 5 $HOME/log-file
	
	elif [ "$arg" = "-less" ]; then
		less +G $HOME/log-file

	else
		local timestamp="$(date '+%Y-%m-%d %H:%M')"
		local msg="$*"

		echo " [$timestamp] $arg $msg" >> $HOME/log-file
		tail -n 5 $HOME/log-file
	fi
}
```
to recognize the function in your existing session
```
$ source ~/.bashrc
```
