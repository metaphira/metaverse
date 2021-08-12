# World Update Module

This module allows you to determine when the current player is on
a different version than other players in the instance. 

# Installation
Import the prefab and reference it in the Metaverse. You should put the prefab
at the top of your scene, because VRChat networking assigns IDs top to bottom.
This ensures that future changes to your world won't break Udon sync for this component
(which would defeat the entire purpose of this module).

# Usage
Specify the version of the world as an integer value. For example, `YYYYMMDDPP`
where `YYYY` is the year, `MM` is the month, `DD` is the day, and `PP` is the patch
number for that day. Create a new UdonBehaviour to receive callbacks from the module
if you want to notify your players with something custom.

## API

This module emits the following events:

### OnReceivedRemoteVersion

This function is called when not all players in the same instance
are running the same version. This could mean that a different player joined with
a newer version, or the current player joined an old instance.

```cs
// don't change these variable names
[NonSerialized] public int inLocalVersion;
[NonSerialized] public int inRemoteVersion;
[NonSerialized] public VRCPlayerApi inSender;

// this function is called if another player in this instance is running a different version of the world than the current player
public void _OnReceivedRemoteVersion()
{
    Debug.Log($"received version update localVersion={inLocalVersion} remoteVersion={inRemoteVersion} sender={inSender.displayName}:{inSender.playerId}");
}
```

### OnRemoteVersionTimedOut
This function is called when the current player couldn't retrieve a remote version.
This most likely means that you made some major changes to the world in a way which
broke Udon sync entirely. You should probably warn the player that nothing is expected
to work properly.

```cs
public void _OnRemoteVersionTimedOut()
{
    Debug.Log("remote version timed out");
}
```
