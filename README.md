# Overview
This is a multithread framework for creating and managing service classes. The framework consists of four main files: singleton_meta.py, service.py and application.py.

## `singleton_meta.py`
The SingletonMeta class in this file is a metaclass for creating singleton classes.

## `service.py`
The Service class in this file is a base class for creating service classes.
A service class is a class that runs in its own thread and provides a certain service or functionality. The Service class has an OnCreate, OnAsyncEvent, and OnRun method that can be overridden by child classes to provide the desired functionality. The Service class also has methods for starting and stopping the service, and for sending messages to other services.

## `application.py`
The Application class in this file is a singleton class for managing a group of service classes. It has methods for adding service classes, starting and stopping all the services, and getting the name of the application and a specific service.

# Usage
To use this framework, create a child class of the Service class and override the OnCreate, OnAsyncEvent, and OnRun methods to provide the desired functionality. Then, create an instance of the Application class and add the service class using the Add method. Finally, start the application using the Start method. The service will run in its own thread and provide the desired functionality.

To stop the service, call the Stop method on the Application instance. This will stop all the services running under the application.

# Example
Here is an example of how to use this framework to create a simple service that prints "Hello, World!" every 5 seconds:
```
from system.service import Service

class HelloWorldService(Service):
    def OnCreate(self):
        print("Hello, World!")
        return 5  # run every 5 seconds

    def OnAsyncEvent(self, source, data):
        pass  # not handling async events

    def OnRun(self):
        print("Hello, World!")
        return 5  # run every 5 seconds

# create an instance of the Application class
app = Application()

# add the HelloWorldService to the application
app.Add("hello_world", HelloWorldService())

# start the application and the HelloWorldService
app.Start()

# Do something
# Meanwhile, the service will now run in its own thread and print "Hello, World!" every 5 seconds

# to stop the service, call the Stop method on the application instance
app.Stop()
```
