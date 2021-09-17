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

## Factory Pattern

### Description 

The Factory Method pattern is widely used in any code. It's useful when you need to provide a lot of flexibility in your code. Factory methods are recognized by creation their methods that create objects from "concrete" classes (something that is not an abstract class).

### Example
```cs
using System;
using System.Collection.Generic;

namespace Program
{
    class Program
    {
        static void Main()
        {
            List<Creator> creators = new List<Creator>();
            creators.Add(new ConcreteCreatorA());
            creators.Add(new ConcreteCreatorB());
            foreach (Creator creator in creators)
            {
                Product product = creator.FactoryPattern();
                Console.WriteLine("Created {0}", product.GetType().Name);
            }
            Console.ReadLine();
        }
    }

    abstract class Product
    {
    }

    class ConcreteProductA : Product
    {
    }

    class ConcreteProductB : Product
    {
    }

    abstract class Creator
    {
        public abstract Product FactoryPattern();
    }

    class ConcreteCreatorA : Creator
    {
        public override Product FactoryPattern()
        {
            return new ConcreteProductA();
        }
    }

    class ConcreteCreatorB : Creator
    {
        public override Product FactoryPattern()
        {
            return new ConcreteProductB();
        }
    }
}
```

## State Pattern

### Description

State pattern is recognized by methods that change their behaviour based on that methods parent class's state. State methods change the current state of a class based on that current state and an action. e.g.

```cs
if Door.IsOpen and Person.IsPushing
  then
    return The door is already open
else if Door.IsClosed and Person.IsPushing
  then
    return The door is now open
else if Door.IsClosed and Person.NotPushing
  then
    return The door is closed
// And so on.
```

### Example

```cs
using System;

namespace Program
{
    public class Program
    {
        public static void Main(string[] args)
        {

            var context = new Context(new ConcreteStateA());

            for (int i = 0; i < length; i++)
            {    
                context.DoContext();
            }

            Console.ReadKey();
        }
    }
    public abstract class State
    {
        public abstract void SetContext(Context context);
    }
    public class ConcreteStateA : State
    {
        public override void SetContext(Context context)
        {
            context.State = new ConcreteStateB();
        }
    }
    public class ConcreteStateB : State
    {
        public override void SetContext(Context context)
        {
            context.State = new ConcreteStateA();
        }
    }
    public class Context
    {
        State state;

        public Context(State state)
        {
            this.State = state;
        }

        public State State
        {
            get { return state; }
            set
            {
                state = value;
                Console.WriteLine("State: " + state.GetType().Name);
            }
        }
        public void DoContext()
        {
            state.SetContext(this);
        }
    }
}
```

## Composition (inheritance)

### Description

Composition allows a class to contain an object instance of another class. This implements better encapsulation than inheritance and is better because any change to the back-end class (class instance inside the class) generally does not interfere with the front-end class and cause it to break. For more information, refer to (this)[https://en.wikipedia.org/wiki/Inception]

### Example 
```cs
using System;

namespace Program
{
    public class Program
    {
        public static void Main(string[] args)
        {
            SecondClass cool_class = new SecondClass();

            cool_class.MyMethod();
        }
    }
    public class FirstClass
    {
        public string property { get; set; }

        public void FirstMethod()
        {
            Console.WriteLine("Implementation!");
        }
    }

    public class SecondClass
    {
        private FirstClass firstClass = new FirstClass();
        public string ClassProperty { get; set; }

        public void MyMethod()
        {
            Console.WriteLine("Yarr! I am the second class which is composed of the first class 🏴‍☠️🦜");
            firstClass.FirstMethod();
        }
    }
}
```
