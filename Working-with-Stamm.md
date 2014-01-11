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