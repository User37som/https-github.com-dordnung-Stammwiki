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

- Native `STAMM_GetType()`  