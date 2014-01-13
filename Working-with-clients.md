This part of the wiki shows you how to use the client part of the API.


## How to get client information

There are a few natives and forwards to retrieve information about clients.

#### Information to know whether a client is valid or not:

- Forward `STAMM_OnClientReady(client)`

	This forward will be executed, after a client joined and is fully initialized by Stamm.

	Here you can be sure to use all client natives.
	Use this instead of forwards like OnClientConnected.

- Native `STAMM_IsClientValid(client)`

	This native return true when a client is fully loaded by Stamm.
	Use this if you are unsure, whether you can use client natives or not.

#### Other forwards and natives for clients:

- Forward `STAMM_OnClientBecomeVip(client, oldlevel, newlevel)`

	This forward will be executed, after a client reaches a new level.
	
	Parameter oldlevel is the old level of the client and newlevel the new level.
	The new level can also be less than the oldlevel.

- Forward `STAMM_OnSaveClient(client)`

	This forward will be executed, after a client was saved to the database.

- Native `STAMM_GetClientLevel(client)`

	This native return the level of the client.

	For more information about levels read: [What are levels](wiki/Introduction-into-the-API#what-are-levels)

- Native `STAMM_IsClientAdmin(client)`

	This native return whether the client is a admin in Stamm or not.


## How to control points of clients

First of all you can use the native `STAMM_GetClientPoints(client)` to get the number of points a client have.

Then you can use a few natives to change these points.

- You can add points with the native `STAMM_AddClientPoints(client, points)`

- You can delete points with the native `STAMM_DelClientPoints(client, points)`

- And you can just set points with the native `STAMM_SetClientPoints(client, points)`


If you wanna know when the client get new points, then you can take the forward `STAMM_OnClientGetPoints(client, points)`.

This will execute when the client get new points.
Parameter `points` is not the new points number of the client, it is the number of points he got.

You can also prevent the client of getting points, or change the number of points he get.

For this there is the forward `STAMM_OnClientGetPoints_PRE(client, &points)`.

You can change the parameter `points`, to change the number of points he get, or return `Plugin_Handled`, to prevent the client of getting points.

---------
### [Go to the next Page](wiki/Working-with-levels)