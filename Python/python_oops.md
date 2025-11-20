### **OOP Cheat Sheet**

#### 1. **Basic Concepts**

- **Class**: Blueprint for creating objects. Defines a datatype by bundling data (attributes) and methods (functions).
    
    ```python
    class Car:
        def __init__(self, brand, model):
            self.brand = brand
            self.model = model
    ```
    
- **Object**: Instance of a class.
    
    ```python
    my_car = Car("Toyota", "Corolla")
    ```
    

#### 2. **Key Principles**

- **Encapsulation**: Bundling data and methods that operate on the data within one unit (class). Protects the data from outside interference.
    
    ```python
    class Car:
        def __init__(self, brand):
            self.__brand = brand  # Private attribute
        def get_brand(self):
            return self.__brand
    ```
    
- **Abstraction**: Hiding complex implementation details and showing only the necessary features.
    
    ```python
    class Car:
        def start_engine(self):  # Public method
            self.__engage_fuel_system()  # Private method
    ```
    
- **Inheritance**: A way to form new classes using classes that have already been defined.
    
    ```python
    class ElectricCar(Car):  # Inherits from Car
        def charge_battery(self):
            pass
    ```
    
- **Polymorphism**: Allows objects to be treated as instances of their parent class, even if they belong to child classes.
    
    ```python
    class Car:
        def drive(self):
            print("Driving a car")
    class Truck(Car):
        def drive(self):
            print("Driving a truck")
    
    vehicle = Truck()
    vehicle.drive()  # Output: Driving a truck
    ```
    

#### 3. **Special Methods**

- **`__init__`**: Constructor method called when an instance is created.
- **`__str__`**: Defines the string representation of the object.
- **`__repr__`**: Provides an official string representation of the object.
- **`__len__`**: Allows object to respond to `len()` function.
    
    ```python
    class Book:
        def __init__(self, title, pages):
            self.title = title
            self.pages = pages
        def __len__(self):
            return self.pages
    ```
    

#### 4. **Access Modifiers**

- **Public**: Accessible from outside the class.
- **Private (`__attribute`)**: Accessible only within the class.
- **Protected (`_attribute`)**: Accessible within the class and its subclasses.

#### 5. **Class vs. Instance Variables**

- **Class Variable**: Shared across all instances.
    
    ```python
    class Car:
        wheels = 4  # Class variable
    ```
    
- **Instance Variable**: Unique to each instance.
    
    ```python
    class Car:
        def __init__(self, brand):
            self.brand = brand  # Instance variable
    ```
    

#### 6. **Class and Static Methods**

- **Class Method (`@classmethod`)**: A method that works with the class, not the instance.
- **Static Method (`@staticmethod`)**: A method that doesn't modify class or instance data.
    
    ```python
    class Math:
        @staticmethod
        def add(a, b):
            return a + b
    ```
    

#### 7. **Inheritance Types**

- **Single Inheritance**: One subclass inherits from one superclass.
- **Multiple Inheritance**: One subclass inherits from multiple superclasses.
- **Multilevel Inheritance**: A class is derived from another derived class.
- **Hierarchical Inheritance**: Multiple classes inherit from a single base class.

#### 8. **Composition vs. Inheritance**

- **Composition**: A "has-a" relationship (objects within other objects).
    
    ```python
    class Engine:
        pass
    class Car:
        def __init__(self):
            self.engine = Engine()  # Car has an engine
    ```
    
- **Inheritance**: An "is-a" relationship.