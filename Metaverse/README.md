# Metaverse Core

This package is at the core of all the modules. It provides module loading, logging, and a very basic import/export system.

# Installation

Import the `Metaverse` prefab into your scene. This object must be located in the root of your scene and must be named `Metaverse`.

Install `ObjectsModule` and include it as a built-in module. In the future, this will be included automatically or something.

Optionally, import the `Debugger` prefab and reference it in the Metaverse component if you want your users to be able to view logs in-game.

# Usage

Modules are loaded in the order specified (dependency resolution may be implemented in the future). Each module must follow the following convention:

```csharp
using Metaphira.Core;
using System;
using UdonSharp;
using UnityEngine;

public class YourModule : UdonSharpBehaviour
{
    [NonSerialized] public const string VERSION = "1.0.0";
    [NonSerialized] public bool INITIALIZED = false;

    private Metaverse metaverse;

    public void _Init()
    {
        metaverse = GameObject.Find("/Metaverse").GetComponent<Metaverse>();

        // perform other initialization here

        INITIALIZED = true;
    }
}
```

## API

The `Metaverse` core provides the following API functions:

### Import/Export

You can import/export arbitrary values to other modules for indirect use.

```csharp
public void _Init()
{
    GameObject someObject = (GameObject) metaverse._Import("OtherModule/SomeObject");

    metaverse._Export("MyModule/Secret", "foobar");
}
```

### Logging

You can log to both the Unity log as well as the in-game debugger (if enabled).

```csharp
private void handleRequest()
{
    metaverse._LogDebug(nameof(MyModule), $"handling request from {Networking.LocalPlayer.displayName}");
}
```

### Module Resolution

You can get a reference to any other loaded module.

```csharp
public void _Init()
{
    ObjectsModule objectsModule = (ObjectsModule) metaverse._GetModule(nameof(ObjectsModule));
}
```
