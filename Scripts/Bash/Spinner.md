# Spinner
#Bash #Scripts

credits:
[Shell Script Spinner Animation Tutorial](https://www.youtube.com/watch?v=93i8txD0H3Q&t=276s)

## Basic spinner

```bash
#!/bin/bash

spinner=( 0oooo o0ooo oo0oo ooo0o oooo0 )

spin(){
	while [ 1 ]
	do
		for i in ${spinner[@]}
		do
			echo -ne "\r$i"
			sleep 0.2
		done
	done
}

spin
```

## Spinner with a process
```bash
#!/bin/bash

spinner=( 0oooo o0ooo oo0oo ooo0o oooo0 )

copy(){
    echo "Copying files..."
	spin &
	pid=$!

    # Emulates a process that takes some time
    # i.e. copying a file
	for i in `seq 1 10`
	do
		sleep 1
	done

	# stop the spin
	kill $pid
	#Clean up the output	
	echo ""
}

spin(){
	while [ 1 ]
	do
		for i in ${spinner[@]}
		do
			echo -ne "\r$i"
			sleep 0.2
		done
	done
}

copy
```

## Slight different version of the spinner

```bash
#!/bin/bash

spinner=( '|' '/' '-' '\' )

copy(){
    echo "Copying files"
	spin &
	pid=$!

    # Emulates a process that takes some time
    # i.e. copying a file
	for i in `seq 1 10`
	do
		sleep 1
	done

	# stop the spin
	kill $pid
	#Clean up the output	
	echo ""
}

spin(){
	while [ 1 ]
	do
		for i in ${spinner[@]}
		do
			echo -ne "\r$i"
			sleep 0.2
		done
	done
}

copy
```


## Dotted spinner
```bash

copy(){
    echo -n "Copying files"
	spin &
	pid=$!

    # Emulates a process that takes some time
    # i.e. copying a file
	for i in `seq 1 10`
	do
		sleep 1
	done

	# stop the spin
	kill $pid
	#Clean up the output	
	echo ""
}

spin(){
	while [ 1 ]
	do
		for i in ${spinner[@]}
		do
			echo -ne "."
			sleep 0.2
		done
	done
}
```