This part of the wiki shows you how to use the core part of the API.


## How to get Stamm information

There are few natives and forwards to retrieve information about Stamm stuff

#### Information to know whether Stamm is loaded or not:

- Stock `STAMM_IsAvailable()`    
	This stock checks whether the Stamm library exists or not.    
	If it's not available, then all natives are unavailable.  

- Forward `STAMM_OnReady()`   
	This forward will be execute when Stamm is fully loaded.    
	Here you can be sure to use any Stamm native.

- Native `STAMM_IsLoaded()`    
	This native return true, whenn Stamm is fully loaded.    
	Use this if you are unsure, whether you can use stamm stuff or not.

#### Get important config values:

- Native `STAMM_GetType()`    
		This native returns how a client can collect points.    
		The return is a value of the StammType enum.    
		So: `KILLS`, `ROUNDS`, `TIME`, `KILLS_ROUNDS`, `KILLS_TIME`, `ROUNDS_TIME`, `KILLS_ROUNDS_TIME`

- Native `STAMM_GetGame()`  
		This native returns the game Stamm is running on.    
		The return is a value if the StammGame enum.
		So: `GameOTHER`, `GameCSS`, `GameCSGO`, `GameTF2`, `GameDOD`

- Native `STAMM_AutoUpdate()`  
		This native returns whether the server admin wants auto updates on Stamm and his features.    
		You can use this to auto update your feature.

- Native `STAMM_GetTag(String:tag[], maxlength)`  
		This native returns the Tag the server admin wants for chat messages.


## How to control happy hour

Happy hour give all clients on the server more points for a specific time.

There are two forwards, to get inform about when happy hour starts or ends.

The forward `STAMM_OnHappyHourStart(time, factor)` will be fired when the happy hour starts.
The parameter time is the Runtime of the happy hour in seconds, the parameter factor is the multiplication factor for the Stamm points.

The forward `STAMM_OnHappyHourEnd()` will be fired when the happy hour ends.

And two natives, to start or end the happy hour.

The native `STAMM_StartHappyHour(time, factor)` will activate the happy hour.
The parameter time is the Runtime of the happy hour in seconds, the parameter factor is the multiplication factor for the Stamm points.

The native `STAMM_EndHappyHour()` will end the happy hour.


## Loading/Unloading features

You can load and unload Stamm features with the natives `STAMM_LoadFeature(Handle:plugin)` and `STAMM_UnloadFeature(Handle:plugin)`.

They will return -1 when the feature is already loaded/unloaded, 0 when the features is invalid, 1 when the command succeeded.

## Adding commands

To give the client a overview over all commands, Stamm has a menu with a list of all Stamm specific commands.

You simply can add a command by using the native `STAMM_AddCommand(const String:command[], const String:name[], any:...)`.

Parameter command is the real command and name a description of the command.


## How to write to logs

Stamm has an own log system with two files. One file for common logs and one for debug stuff.

You can write to the Stamm logs by using the native `STAMM_WriteToLog(bool:debug, const String:fmt[], any:...)`.

The Parameter debug defines, whether to write to the debug file or not.