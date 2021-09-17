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
