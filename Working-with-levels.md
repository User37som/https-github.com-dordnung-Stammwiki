This part of the wiki shows you how to use the level part of the API.

If you don't know what levels are you have to read: [**What are levels**](wiki/Introduction-into-the-API#what-are-levels)

## Level natives

There is not much to say about levels, so I show you the few levels natives.

- To get the number of defined levels, use the native `STAMM_GetLevelCount()`

- To get the number of points a client needs to get a level, use `STAMM_GetLevelPoints(level)`

- To get the number of a named level, use `STAMM_GetLevelNumber(const String:name[])`

- To get the named of a level, use `STAMM_GetLevelName(level, String:name[], maxlength)`

- To know whether the level is a private level, use `STAMM_IsLevelPrivate(level)`

---------
### [Go to the next Page](wiki/Colors-in-Stamm)