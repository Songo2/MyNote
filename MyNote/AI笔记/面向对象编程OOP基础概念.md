# 面向对象编程（OOP）基础概念

创建时间：2026-05-07 13:24

# 面向对象编程（OOP）

面向对象编程是一种编程范式，它使用“对象”来设计软件。对象是类的实例，类是创建对象的蓝图。OOP 的核心概念包括封装、继承、多态和抽象。

## 核心概念

### 1. 类（Class）
类是创建对象的蓝图。它定义了对象的属性和方法。

```python
class Car:
    def __init__(self, make, model):
        self.make = make
        self.model = model

    def drive(self):
        print(f"{self.make} {self.model} is driving.")
```

### 2. 对象（Object）
对象是类的实例。每个对象都有自己的状态和行为。

```python
my_car = Car("Toyota", "Corolla")
my_car.drive()
```

### 3. 封装（Encapsulation）
封装是将数据和代码封装在一起，并隐藏内部实现细节。

```python
class Person:
    def __init__(self, name):
        self.name = name

    def get_name(self):
        return self.name

person = Person("Alice")
print(person.get_name())
```

### 4. 继承（Inheritance）
继承允许一个类继承另一个类的属性和方法。

```python
class ElectricCar(Car):
    def __init__(self, make, model, battery):
        super().__init__(make, model)
        self.battery = battery

    def drive(self):
        print(f"{self.make} {self.model} with {self.battery} kWh battery is driving.")
```

### 5. 多态（Polymorphism）
多态允许不同类的对象对同一方法做出不同的响应。

```python
def show(car):
    car.drive()

my_car = Car("Toyota", "Corolla")
my_electric_car = ElectricCar("Tesla", "Model S", 75)

show(my_car)
show(my_electric_car)
```

### 6. 抽象类（Abstract Class）
抽象类是不能实例化的类，通常用于作为基类。

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def make_sound(self):
        pass

class Dog(Animal):
    def make_sound(self):
        print("Woof!")

dog = Dog()
dog.make_sound()
```

## 总结
面向对象编程通过类和对象的概念，使代码更易于理解和维护。封装、继承、多态和抽象是 OOP 的核心原则，帮助开发者构建模块化、可扩展的系统。