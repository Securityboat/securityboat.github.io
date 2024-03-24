# **Bash Scripting**

## **Iterate over a file <a href="#iterate-over-a-file" id="iterate-over-a-file"></a>**

This script will iterate over a file and echo out every single line:

```
#!/bin/bash​for line in $(cat file.txt);do    echo $linedone
```

Another way of writing is this:

```
#!/bin/bash​while read p; do    echo  $pdone 
```

## **For-loops <a href="#for-loops" id="for-loops"></a>**

```
#!/bin/bash​for ((i = 0; i < 10; i++)); do    echo $idone
```

Another way to write this is by using the program `seq`. Seq is pretty much like `range()` in python. So it can be used like this:

```
#!/bin/bash​for x in `seq 1 100`; do    echo $xdone
```

## **If statement <a href="#if-statement" id="if-statement"></a>**

`$1` here represent the first argument.

```
​if [ "$1" == "" ]; then    echo "This happens"fi
```

## **If/Else <a href="#ifelse" id="ifelse"></a>**

```
#!/bin/bash​if [ "$1" == "" ]; then    echo "This happens"else    echo "Something else happens"fi
```

## **Command line arguments <a href="#command-line-arguments" id="command-line-arguments"></a>**

Command line arguments are represented like this

This is the first command line argument.

## **Daemonize an execution <a href="#daemonize-an-execution" id="daemonize-an-execution"></a>**

If you do a ping-sweep with host the command will take about a second to complete. And if you run that against 255 hosts I will take a long time to complete. To avoid this we can just deamonize every execution to make it faster. We use the `&` to daemonize it.

```
#!/bin/bash​for ip in $(cat ips.txt); do    ping -c 1 $ip &done
```

## **Use the output of command <a href="#use-the-output-of-command" id="use-the-output-of-command"></a>**

It has happened to me several times that I want to input the output of a command into a new command, for example:

I search for a file, find three, and take the last line, which is a path. Now I want to cat that path:

```
#!/bin/bash​locate 646.c | tail -n 1
```

This can be done like this:

```
#!/bin/bash​cat $(locate 646.c | tail -n 1)
```
