---
title: Dunder in Python
date: 2024-12-10
---
Dunder (double underscore) methods, also known as "magic methods" or "special methods," provide Python objects with their functionality by overriding built-in behavior. Here’s a list of the most commonly used dunder methods in Python 3, categorized for easier understanding:

---

### **Initialization and Representation**
1. **`__init__(self, ...)`**  
   Called when initializing a new object.  
   ```python
   def __init__(self, name):
       self.name = name
   ```

2. **`__repr__(self)`**  
   Returns a developer-friendly string representation of the object, primarily for debugging.  
   ```python
   def __repr__(self):
       return f"ClassName({self.name!r})"
   ```

3. **`__str__(self)`**  
   Returns a user-friendly string representation of the object.  
   ```python
   def __str__(self):
       return f"Object named {self.name}"
   ```

4. **`__del__(self)`**  
   Called when an object is about to be destroyed (cleanup actions).  

---

### **Comparison and Ordering**
5. **`__eq__(self, other)`**  
   Defines behavior for equality (`==`).  

6. **`__ne__(self, other)`**  
   Defines behavior for inequality (`!=`).  

7. **`__lt__(self, other)`**  
   Defines behavior for less than (`<`).  

8. **`__le__(self, other)`**  
   Defines behavior for less than or equal (`<=`).  

9. **`__gt__(self, other)`**  
   Defines behavior for greater than (`>`).  

10. **`__ge__(self, other)`**  
    Defines behavior for greater than or equal (`>=`).  

---

### **Arithmetic Operations**
11. **`__add__(self, other)`**  
    Defines behavior for addition (`+`).  

12. **`__sub__(self, other)`**  
    Defines behavior for subtraction (`-`).  

13. **`__mul__(self, other)`**  
    Defines behavior for multiplication (`*`).  

14. **`__truediv__(self, other)`**  
    Defines behavior for division (`/`).  

15. **`__floordiv__(self, other)`**  
    Defines behavior for floor division (`//`).  

16. **`__mod__(self, other)`**  
    Defines behavior for modulo (`%`).  

17. **`__pow__(self, other)`**  
    Defines behavior for exponentiation (`**`).  

---

### **Container and Length**
18. **`__len__(self)`**  
    Returns the length of an object (e.g., in `len(obj)`).  

19. **`__getitem__(self, key)`**  
    Defines behavior for indexing (e.g., `obj[key]`).  

20. **`__setitem__(self, key, value)`**  
    Defines behavior for assigning to an index (e.g., `obj[key] = value`).  

21. **`__delitem__(self, key)`**  
    Defines behavior for deleting an index (e.g., `del obj[key]`).  

22. **`__iter__(self)`**  
    Returns an iterator for the object.  

23. **`__next__(self)`**  
    Returns the next item in an iterator.  

---

### **Context Management**
24. **`__enter__(self)`**  
    Called when entering a context using the `with` statement.  

25. **`__exit__(self, exc_type, exc_value, traceback)`**  
    Called when exiting a context.  

---

### **Callable and Attributes**
26. **`__call__(self, ...)`**  
    Makes an object callable like a function.  

27. **`__getattr__(self, name)`**  
    Defines behavior when an attribute is accessed that doesn't exist.  

28. **`__setattr__(self, name, value)`**  
    Defines behavior for assigning to an attribute.  

29. **`__delattr__(self, name)`**  
    Defines behavior for deleting an attribute.  

30. **`__dir__(self)`**  
    Defines the behavior of the `dir()` function for the object.  

---

### **Other Common Methods**
31. **`__hash__(self)`**  
    Defines behavior for hashing an object, used in sets or as dictionary keys.  

32. **`__bool__(self)`**  
    Defines behavior for truth-value testing (e.g., in `if obj:`).  

33. **`__contains__(self, item)`**  
    Defines behavior for the `in` keyword.  

34. **`__index__(self)`**  
    Called when an object needs to be treated as an integer index.  

---

These dunder methods make Python objects more intuitive and interoperable with built-in functionality. Overriding them carefully can help you design powerful, custom objects. 