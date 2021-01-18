Name	: Kasturi Tarachand More
Email	: kmore4@binghamton.edu
BNumber	: B00816799

CS557 - Programming Assignment 2
Chord Distributed Hash Table

Programming Language: Python

————————————————————
How to run the code:
————————————————————

* To Compile the interface definition file
	$> bash
	$> export PATH=$PATH:/home/cs557-inst/local/bin

* Thrift command to compile this assignment’s IDL file to Python is as follows:
	$> cp /home/cs557-inst/pa2/chord.thrift ./
	$> thrift -gen py chord.thrift
	
* The files which need to be run are “server.py” and “nodes.txt”

* The file (node.txt) should contain a list of IP addresses and ports, in the format “<ip-address>:<port>”, of all of the running DHT nodes.
	128.226.114.206:9081
	128.226.114.206:9082
	128.226.114.206:9083
	128.226.114.206:9084

* The server executable will take a single command-line argument specifying the port where the Thrift service will listen for remote clients. For example:
	./server 9081
	./server 9082
	./server 9083
	./server 9084

* Start all the “<ip-address>:<port>” mentioned in nodes.txt using above command

* The initializer program takes filename as its only command line argument. To run the initializer:
	$> /home/cs557-inst/pa2/init nodes.txt

* To test the program, I have created 3 client files where client file is used to check implementation of readFile call to server and client1 & client2 are used to check implementation of writeFile call to server
	$> ./client1
	$> ./client

* Make sure the following things:
	-> You're in BASH shell and have the path "'/home/cs557-inst/thrift-0.13.0/lib/py/build/lib*'" appended to $PATH environment variable.
	-> The source code files have executable permission:
		$ chmod +x *.py

* If client gives error saying '#!/usr/bin/env python' then do following steps:
	->vi client
	->:set ff=unix
	->:wq

———————————————————
Sample outputs:
———————————————————

(1) writeFile with server that owns File:

	kmore4@remote06:~/DS/Assignment 2/Kasturi$ ./client1
	()
	writeFile() called..
	()
	kmore4@remote06:~/DS/Assignment 2/Kasturi$ ./client2
	()
	writeFile() called..
	()
	kmore4@remote06:~/DS/Assignment 2/Kasturi$


(2) writeFile with server that does not owns File:

	kmore4@remote06:~/DS/Assignment 2/Kasturi$ ./client1
	()
	SystemException(_message=u'This Server 128.226.114.206:9083 is not the owner of file abc.txt')


(3) readFile with server that owns File: (after 1st and 2nd writeFile calls)

	kmore4@remote06:~/DS/Assignment 2/Kasturi$ ./client
	readFile() called..
	('  FileName: ', u'abc.txt')
	('  Version: ', 0)
	('  Content: ', u'Hi.. I am Kasturi..!!!')
	()
	kmore4@remote06:~/DS/Assignment 2/Kasturi$ ./client2
	()
	writeFile() called..
	()
	kmore4@remote06:~/DS/Assignment 2/Kasturi$ ./client
	readFile() called..
	('  FileName: ', u'abc.txt')
	('  Version: ', 1)
	('  Content: ', u'New Content')


(4) readFile with server that does not owns File:

	kmore4@remote06:~/DS/Assignment 2/Kasturi$ ./client
	SystemException(_message=u'This Server 128.226.114.206 is not the owner of abc.txt')
