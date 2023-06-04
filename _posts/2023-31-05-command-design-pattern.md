---
layout: post
title: "Command Design Pattern"
date: 2023-05-31 20:00:00 +0300
author: semih
comments: true
lang: en
lang-ref: command-design-pattern
categories: [design-patterns]
tags: [design-patterns]
published: true
---
**Command Design Pattern** is a behavioral design pattern that turns a request(action or operation) into a stand-alone object that contains all information about the request.

The command design pattern wraps the objects that performs user requests. In this way, the same code structure can be used again and again. Each process to be performed on the command pattern is wrapped as an object.
There may be different command objects which has already implemented. The object to be processed is sent to the command object as a parameter and various are given to it.

As a benefit of creating commands as objects, they can also be taught to undo their actions when desired. As a result, Redo(Redo)/Undo(Undo) operations can be performed and a macro feature can be created.

---

The Command pattern involves the following key components:
- **Command:** This is an interface or an abstract class that declares an execute() method. This method defines the operation to be performed.
- **Concrete** Command: These are the implementations of the Command interface. Each concrete command encapsulates a specific request and binds it to a receiver by invoking the corresponding operation on the receiver.
- **Receiver:** This is the object that performs the actual operation when a command is executed. The receiver knows how to carry out the request.
- **Invoker:** The invoker is responsible for initiating the execution of the command. It holds a reference to a command object and can execute the command by calling its execute() method.
- **Client:** The client is responsible for creating the command objects, setting their receivers, and associating them with invokers.

```java
// Step 1: Create the Command interface
interface Command {
    void execute();
}

// Step 2: Create Concrete Command classes
class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.turnOn();
    }
}

class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.turnOff();
    }
}

class LightChangeColorCommand implements Command {
  private Light light;

  public LightChangeColorCommand(Light light) {
    this.light = light;
  }

  public void execute() {
    light.changeColor();
  }
}

// Step 3: Create the Receiver class
class Light {
    public void turnOn() {
        System.out.println("Light is on");
    }

    public void turnOff() {
        System.out.println("Light is off");
    }

    public void changeColor() {
      System.out.println("Light color has been changed");
    }
}

// Step 4: Create the Invoker class
class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}

// Step 5: Create the Client class
class Client {
    public static void main(String[] args) {
        // Create the receiver
        Light light = new Light();

        // Create the commands
        LightOnCommand lightOnCommand = new LightOnCommand(light);
        LightOffCommand lightOffCommand = new LightOffCommand(light);
        LightChangeColorCommand lightChangeColorCommand = new LightChangeColorCommand(light);

        // Create the invoker
        RemoteControl remoteControl = new RemoteControl();

        // Set the commands in the invoker
        remoteControl.setCommand(lightOnCommand);

        // Press the button to turn on the light
        remoteControl.pressButton();

        // Set a different command in the invoker
        remoteControl.setCommand(lightOffCommand);

        // Press the button to turn off the light
        remoteControl.pressButton();

        // Set a different command in the invoker
        remoteControl.setCommand(lightChangeColorCommand);

        // Press the button to change color the light
        remoteControl.pressButton();
    }
}
```

> Command and Strategy patterns are both behavioral design patterns. They may look similar because you can use both to parameterize an object with some action. However, they serve different purposes and have distinct intents.
The Strategy pattern is about dynamically selecting and switching algorithms, while the Command pattern is about encapsulating and decoupling requests as objects.

### Fields of Usage

---
The Command pattern can be applied in various fields, including:

1. **User Interfaces:** The Command pattern is commonly used in GUI frameworks and applications to handle user actions and operations. Each user action is encapsulated as a command object, allowing the application to manage and execute them as needed.
2. **Transactional Systems:** The Command pattern is suitable for implementing transactional systems, where a series of actions need to be executed or rolled back as a single atomic unit. Each command object represents an individual action, and the transactional manager orchestrates their execution.
3. **Menu Systems and Keyboard Shortcuts:** Applications that involve menus and keyboard shortcuts can utilize the Command pattern. Each menu item or shortcut can be associated with a command object, which performs the corresponding action when invoked.
4. **Multi-level Undo/Redo:** The Command pattern facilitates implementing undo and redo functionality in applications. By keeping a history of executed commands, you can easily revert or reapply them to achieve undo and redo operations.
5. **Task Scheduling and Job Queues:** In systems that require scheduling and queuing of tasks or jobs, the Command pattern can be employed. Each task or job can be encapsulated as a command object, allowing the system to schedule, prioritize, and execute them accordingly.
6. **Remote Procedure Calls (RPC) and Networking:** The Command pattern can be utilized in distributed systems, especially for implementing Remote Procedure Calls (RPC). The command object carries the necessary data and logic required to invoke remote methods or perform operations on remote systems.

These are just a few examples of the fields of usage for the Command pattern. Its flexibility and ability to encapsulate requests make it applicable in various scenarios where loose coupling, extensibility, and flexibility are desired.

---

I have tried to summarize it in its simple form. I hope it has been an example you can apply to your specific scenarios.
