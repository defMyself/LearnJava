# Python3 反射

**反射：根据字符串动态的判断，调用，添加，修改，删除类或类的实例化对象中的方法或属性**

反射的四种方法

* `hasattr()` : 通过字符串来判断类或类里的实例化对象有没有与字符串相同的属性或方法
* `getattr()`：调用属性或方法
* `setattr()`： 添加属性或方法
* `delattr()`： 删除属性或方法

```python
class student(object):
    def __init__(self, name):
        self.name = name;
        
    def study(self):
        print("%s in the room study "%self.name)
  

stuobj = student("shanghai")

def run(self):
    print("%s play game-0-0"%self.name)
    
 
str = input("input str:")
if hasattr(stuobj, str):
    '''
    '''
```

