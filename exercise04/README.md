# Exercise Sheet 4

In this exercise sheet you will practice interprocess communication with pipes. 

# Task 1

Imagine a complex system consisting of multiple servers: a database server, a middle-ware server, and a web server. These servers log different information by using named pipes (FIFO). In order to print the output generated by any of these servers you decide to create your own service. This service will read from any of the aforementioned FIFOs (read only when something is available) and will print the information on the standard output. 

For this task your goal is to simulate the database server, middle-ware server, and web sever as well as to implement the requested logging service. 

First of all, you need to create 3 named pipes, each of them representing one of the aforementined servers. 

Each of the servers should be simulated by a process running forever in an endless loop. Within the loop, every 2 to 7 seconds (randomly selected) a message should be logged on the corresponding FIFO. You may choose the message content, but keep your messages shorter than `PIPE_BUF` bytes to ensure atomic writes.

The logging service will open the three FIFOs and wait for input on all of them using `select()`. Each received message in any of these pipes should be consumed by the service and printed on the standard output. Assume that this service will also run forever in an endless loop. 

An example of how the output will be shown could be:

    [web] message 1 from web server
    [middle-ware] message 1 from middle-ware server
    [middle-ware] message 2 from middle-ware server
    [web] message 2 from web server
    [database] message 1 from database
    [middle-ware] message 3 from middle-ware server


# Task 2

Create a program that implements the execution of the command `ls | grep <keyword>`. To implement this behaviour, your program is required to create a process that executes the command `ls`. Create another process that executes the command `grep keyword`. Communicate between both processes by using an unnamed pipe. 
This assignment **requires** that you explicitly use `fork()`, `pipe()`, and `dup()/dup2()`. You can use the `execl*` family of functions to execute the `ls` and `grep` commands.

# Task 3

Adjust your implementation of Task 1 to use **message queues** for communication instead of named pipes.

What are the advantages and disadvantages of message queues compared to named pipes?
