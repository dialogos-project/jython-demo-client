# DialogOS Client in Java

This repository illustrates how to implement a client for [DialogOS](https://github.com/dialogos-project/dialogos) in [Jython](http://www.jython.org/). This allows developers who are more proficient in Python than in Java to also implement DialogOS clients.

The client is extremely basic: It simply outputs whatever string is sent to it from DialogOS to the console. Run it as follows:

```
gradlew runClient
```

Then set up a connection to the client in DialogOS (Dialog -> Devices), using one of the following two options:

* CLT Connector (Fixed Server) with server name "localhost" and port 8888.
* CLT Connector (Rendezvous) with service name "Jython demo client" and server "localhost"

## Implementing your own client in Jython

To implement your own Jython-based client, first adapt `build.gradle` to your needs. The main change you will need to make here is to set the file name in the `runClient` task to the name of your own Jython script. If you want to add Java libraries as dependencies, add them to the `dependencies` block as `jython(group:..., name:..., version:...)`. If you want to add Python libraries as dependencies, follow the instructions from the [gradle-jython plugin](https://github.com/rzabini/gradle-jython) (I have not tried this myself yet).

Then write your own version of `client.py`. Implement your own class that is derived from the `Client` class from DialogOS. See the documentation of that class. You can then create an object of your class and call its `open` method to start the client and wait for connections from DialogOS.

You can set the port on which your client listens for connections in the argument to the `open` method. You set the service name for the Rendezvous connector by changing the value that is returned by your `getName` method.

