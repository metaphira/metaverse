# Objects Module

This module provides various data structures that would be nice to have in Udon except they're not exposed.

# Installation

Import the prefab anywhere and reference it in the Metaverse as a built-in module.

# Usage

## Object List
A list data structure that supports dynamic resizing. Supports arbitrary objects.

```cs
ObjectsModule objectsModule = /* ... */;

ObjectList list = objectsModule.NewObjectList();
list._Add("a");
list._Add("b");
list._Contains("b");
list._Contains("c");
list._RemoveByVal("a");
```

## Object/Object Map
A map data structure that supports arbitrary objects as keys and values. Very simple
hashmap implementation underneath to provide better performance than the naive implementation
of two arrays.

```cs
ObjectsModule objectsModule = /* ... */;

ObjectObjectMap map = objectsModule.NewObjectObjectMap();
map._Put("a", 5);
map._Put("b", 6);
map._Get("b");
map._Get("c");
map._Remove("a");
```