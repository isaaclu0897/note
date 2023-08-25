#how-to , #java , #remote , #debug

Remote debugging is a powerful feature that allows you to debug a [[Java]] program running on a remote machine, using an Integrated Development Environment ([[IDE]]) such as [[Eclipse]].

Remote debugging is a feature in Java that enables you to connect to a running Java application on a remote machine and debug it. It allows you to resolve issues in the code without having to physically access the machine where the application is running.

This article explains what remote debugging is, when to use it, and provides step-by-step instructions on how to use it.

### When to Use Remote Debugging?

Remote debugging is great for troubleshooting issues that are difficult to reproduce locally. However, it should be used with caution as it may affect the performance of remote applications.

Remote debugging is suitable for the following as below:
1. **Different network**: When you need to diagnose problems on a remote host, **especially when the host is not within your physical network environment**.
2. **Difficult to reproduce**: Remote debugging is a useful tool when the problem occurs only in specific scenarios.
3. **Stage area verification**: Use remote debugging in the stage area to verify the operation of the code before deployment, and find out the root cause of problem.

What you need to know is that remote debugging can be dangerous in a production area, so please make sure your remote debugging operations have minimal impact on running applications to avoid affecting user experience and system performance.
→ 簡單地說就是正式區不要用就對惹

### How to Use Remote Debug in Java with Eclipse

To use remote debugging quickly, follow these steps:

1. Run the remote Java application with the debug options.
2. Configure destination settings to attach to the remote.
### Step by Step

Follow these step-by-step instructions to use remote debugging in Java:

#### Run the remote Java application with the debug options.
1. Start the remote Java application with the debug options. Use the following command to start the Java application, it will enable listen on remote port 8000:
```
# java
java -Xdebug -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n <className>

# jar
java -Xdebug -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n <jarFile>
```

* suspend
	* y, the JVM will wait until debugger is attached
	* n, the JVM will starts execution right away.
#### Configure destination settings to attach to the remote
1. Open Eclipse and create a new Debug Configuration by selecting "Remote Java Application" from the Debug Configurations dialog.
2. Configure the Debug Configuration with the remote host and port.
3. Click the "Debug" button to connect to the remote application and start debugging.
4. You can now set breakpoints, inspect variables, and step through the code just as if you were debugging a local Java application.

Note: If you need to debug a remote application that is running on a different network, you may need to check your firewall settings to allow incoming connections on the debug port.

By following these steps, you can easily debug a Java program running on a remote machine using an IDE such as Eclipse.

### Reference

> [Java Application Remote Debugging](https://www.baeldung.com/java-application-remote-debugging)
> [JAVA的Remote Debug With Tomcat](https://akuma1.pixnet.net/blog/post/265919554-debug%E6%8A%80%E5%B7%A7%E7%B3%BB%E5%88%97%E4%B9%8B%E5%85%AD----java%E7%9A%84remote-debug-with-tomcat)
> []()
> 