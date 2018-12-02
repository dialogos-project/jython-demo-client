# DialogOS Client in Jython

This repository illustrates how to implement a client for [DialogOS](https://github.com/dialogos-project/dialogos) in [Jython](http://www.jython.org/). This allows developers who are more proficient in Python than in Java to also implement DialogOS clients.

The client is extremely basic: It simply outputs whatever string is sent to it from DialogOS to the console. To see how to send values back to DialogOS, check the [documentation on clients](https://github.com/dialogos-project/dialogos/wiki/Clients) in the DialogOS Wiki and the [Echo Client](https://github.com/dialogos-project/dialogos-echo-client).


## Running the client

To run the client, you will need the following:

* An up-to-date version of [Jython](http://www.jython.org/downloads.html); at the time of writing, this is 2.7.0. This document assumes that `jython` is in your PATH, so you can simply call it as `jython` on the command line. Otherwise, replace `jython` below with its absolute pathname.
* The DialogOS client library, which you can [download here](https://github.com/dialogos-project/dialogos/releases/download/2.0.3/dialogos-client-2.0.3.jar). This document assumes that you save the file as `dialogos-client-2.0.3.jar` in your current directory; you can also put it somewhere else, and will then have to adjust the paths below as needed.

Run the client as follows:

```
jython -Dpython.path=dialogos-client-2.0.3.jar client.py
```

After a moment, this should print the following message to the console:

```
new state: CONNECTING
```


## Connecting to the client from DialogOS

You can set up a connection to the client in DialogOS (Dialog -> Devices), using one of the following two options:

* CLT Connector (Fixed Server) with server name "localhost" and port 8888.
* CLT Connector (Rendezvous) with service name "Jython demo client" and server "localhost"

When DialogOS starts executing the dialog, it will then connect to the client.


## Implementing your own client in Jython

Implementing your own Jython-based client amounts to implementing your own version of `client.py`, which should implement a class that is derived from the `Client` class from DialogOS. See the documentation of that class. You can then create an object of your class and call its `open` method to start the client and wait for connections from DialogOS. See the [Wiki page on (Java) clients](https://github.com/dialogos-project/dialogos/wiki/Clients) and the [documentation of the Client class](https://jitpack.io/com/github/dialogos-project/dialogos/dialogos/-SNAPSHOT/javadoc/com/clt/dialog/client/Client.html) for details.

You can set the port on which your client listens for connections in the argument to the `open` method. You set the service name for the Rendezvous connector by changing the value that is returned by your `getName` method.

You can use all Java libraries and many Python libraries in your client. This works as follows:

* To use a Java library, download the Jar file and add it to the classpath (by adding it to the `-Dpython.path` argument, see above).
* To use a Python library, install it with `pip install <library>` as you would using Python. **Important:** Make sure that you use the `pip` that came with Jython, not the `pip` for your regular version of Python.

Note that Jython supports [many, but not all Python libraries](http://www.jython.org/faq3.html) due to architectural limitations.

