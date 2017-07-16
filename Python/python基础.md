python基础
---
## [python内置api](https://docs.python.org/3/library/functions.html)
- [x] 1.在`python`中`dict`相当于一个`HashMap`
    - [x] (1).使用`dict['name']`可直接获取到`value`，但是如果没有这个`key`会报错
    - [x] (2).使用`dict.get('name',-1)`不存在返回指定第二个参数值，没有参数返回`none`
    - [x] (3).使用`dict.pop('name')`删除`key-value`
- [x] 2.在`python`中`set`相当于是一个无重复的`list`,使用方法
    ``` python
        s = set([1,2,3,4,5])
    ```
- [x] 3.`list`切片，当只取`list`部分连续内容，一般用`for`循环去解决或直接输入，`python`中可直接使用`listp[0-3]`这样直接取值，这个功能叫`切片`
