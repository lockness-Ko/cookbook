# C# Cookbook

## Classes/Objects

### Description

Classes and objects are a fundamental part of OOP, they allow for mass instantiation of the same thing with slight differences and quick customization and always lead to cleaner code. 

### Example

```cs
using System;

namespace Tutorial {
  class Thing1 {
    private string name;
    
    public Thing1(string name) {
      this.name = name;
    }
    
    public string getName() {
      return this.name;
    }
  }
  
  class Thing2 {
    private int age;
    
    public Thing1(int age) {
      this.age = age;
    }
    
    public int getAge() {
      return this.age;
    }
  }
  
  class Program {
    public static void Main(string[] args) {
      Console.WriteLine("Welcome to my cool program!");
      
      var Object1 = new Thing1("John");
      Thing2 Object2 = new Thing2(23);
      
      Console.WriteLine("Hello! My name is "+Thing1.getName()+" and my age is "+Thing2.getAge().ToString());
    }
  }
}
```

## Class Inheritance

### Description

Class inheritance is extremely useful for creating multiple different types of the same object, e.g.
 - User classes:

```cs
Abstract user()

Class admin() Inherits user, has super cool privileges
Class pleb() Inherits user, has regular boring privileges
```

In this case there is a `user` abstract class, an `admin` class which inherits the `user` class and a `pleb` class which also inherits the `user` class except, the `admin` has super cool privileges and the `pleb` does not. They both might have command function such as:
```cs
Abstract user() { 
  doSomething(thing) {}
  getPaid() {}
}

admin() {
  override doSomething(thing) { do(thing, with super cool privileges) }
  override getPaid() { more money }
}

pleb() {
  override doSomething(thing) { do(thing, with regular, un-cool privileges) }
  override getPaid() { less money }
}
```

### Example
```cs
using System;
using System.Collections.Generic;

namespace Tutorial {
  abstract class user {
    public abstract void doSomething();
  }
  
  class admin : user {
    public override void doSomething() {
      Console.WriteLine("I have super cool privileges")
    }
  }
  
  class pleb : user {
    public override void doSomething() {
      Console.WriteLine("I do not have super cool privileges :'(")
    }
  }
  
  class Program {
    public static void Main(string[] args) {
      List<user> users = new List<user>();
      
      users.Add(new admin());
      users.Add(new pleb());
      
      foreach(var _user in users) {
        _user.doSomething();
      }
      
      // The final thing will print out:
      /*
        I have super cool privileges
        I do not have super cool privileges :'(
      */
    }
  }
}
```
