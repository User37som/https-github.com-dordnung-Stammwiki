This part of the wiki shows you **how to make a feature** for Stamm.


## What are blocks

Blocks are used to get information, about when a client should get your feature.    
It have to be a .txt file, named like **the basename of your feature** and you need to put it in `cfg/stamm/levels`.

You can set **up to 100 blocks** in the file.

A block file looks like this:

	"LevelSettings"
	{
		"<name_of_the_block>"    "<level_of_the_block>"
		"<name_of_the_block2>"   "<level_of_the_block2>"
	}

The name have to be defined by yourself, it have to be **unique** and can be retrieved with the API.    
The level have to be set by the server admin, it links the block with a specific level.

The **block ID** is the **position number** of a block in the block file, **beginning from 1**.

Example:

	"name1"      "Silver"      // This will be ID 1
	"name234"    "Gold"        // This will be ID 2
	"name9"      "God"         // This will be ID 3

If you only have one block, you can just work with the ID 1.


Here are two examples of block files:

	"LevelSettings"
	{
		// Level to get colored smokes
		"level"         "Bronze"
	}

Here we only have one block, the name `level` is just a place holder, we will just use the ID 1 later one.

	"LevelSettings"
	{
		// Level to get a Welcome Message, -1 to Disable.
		"welcome"       "Bronze"
		
		// Level to get a Leave Message, -1 to Disable.
		"leave"         "Silver"
	}

Here we have **two blocks**, one for the **welcome message** and one for the **leave message**.

If you have a **specific block name**, you can use `STAMM_GetBlockOfName(const String:name[])` to **retrieve the ID** of the block. E.g. `STAMM_GetBlockOfName("leave")` would be return 2.

If you have the ID of a block and you want the name, you can use `STAMM_GetBlockName(block=1, String:name[], maxlength)`, where block is the ID of the block.

You can retrieve the **level ID of a specific block** with the native `STAMM_GetBlockLevel(block=1)`.    
For the block `name1` and the level settings from the first Page, `STAMM_GetBlockLevel(1)` would return 2, because Silver is the second level.

On top of this there are **block descriptions**, to let clients know about what happen with what block.

Every block can have **unlimited descriptions**. These descriptions are readable in the Stamm menu by the client.    
You can **push descriptions to an array** in the forward `STAMM_OnClientRequestFeatureInfo(client, block, &Handle:array)`.

For the block `name1` and the level settings from the first Page, `PushArrayString(array, "VIP's get a lot of stuff hehe")` would show the client, that **he get a lot of stuff**, when he becomes Silver VIP. This is because `name1` has the level Silver.

And the last thing about blocks is **how to get the block a client is in**.

For this there is the native `STAMM_GetClientBlock(client)`. It will return the **highest block a client is in**.    
So in the example, if the client is a Platinum VIP, `STAMM_GetClientBlock(client)` will return **2**, because the third block is only for God VIP's, but the second block is for Gold VIP's, and Platinum is higher (or equal) then Gold, so **block 2 is the highest block**.

You need this especially for [**Features with dynamic blocks**](Scripting-Features#features-with-dynamic-blocks).


## How features work

After you add a feature it will be listed in the Stamm plugin.

Stamm will **search for the blocks file** and will parse all blocks.

Also the database get a new column in the database to remember whether the client activate the feature or not.

Finally the `STAMM_OnFeatureLoaded` forward will be called. 


## How to create a feature


#### Create the blocks file:

First of all **create a block file with the basename of your feature**.    
If your features name for e.g. is `sample_feature.smx` create a file `sample_feature.txt` in the folder `cfg/stamm/levels`.

Paste in:

	"LevelSettings"
	{

	}

Now you can define your blocks between the brackets.

In this example we want to define two blocks, one for a connect message and one for a player death message.    
So we add them between the brackets:

	"LevelSettings"
	{
		"connect-message"    "Bronze"
		"death-message"      "Gold"
	}

As a default we define here level Bronze for the connect message and level Gold for the death message.    
Later one the server admin can change this to its own config.


#### Create the phrase file:

To sort the phrases, Stamm has its own sub-folder in the translations folder.    
If you create a feature, please use the `translations/stamm` folder, then you also can use the stock `STAMM_LoadTranslation()`.

Also **name the phrase file like the blocks file**, so create again a `sample_feature.txt` and move it to `translations/stamm`.

Here we need some information to notice the client about the feature, of which more later.

So we paste in:

	"Phrases"
	{
		"GetConnectMessage"
		{
			"en"		"When you connect, all players will notice"
			"de"		"Wenn du joinst, wird das jeder sehen"
		}
	
		"GetDeathMessage"
		{
			"en"		"When you die all, players will notice"
			"de"		"Wenn du stirbst, wird das jeder sehen"
		}
	}


#### Finally write the .sp file:

Now we create a new .sp file (**remember that it have to be the same name like the name of the block and translations file**).    

Then we include `sourcemod` and `stamm`:

```c++
#include <sourcemod>
#include <stamm>
```

**When all plugins are loaded we can add the feature**.    
But first of all we **check whether Stamm is loaded or not**, therefore we use the native `STAMM_IsAvailable()`:

```c++
public OnAllPluginsLoaded()
{
	if (!STAMM_IsAvailable()) 
	{
		SetFailState("Can't Load Feature, Stamm is not installed!");
	}
}
```

After that we can **load our translations and add the feature**.    
To load the translation we use `STAMM_LoadTranslation()` and to add a feature `STAMM_RegisterFeature(const String:name[], bool:allowChange=true, bool:standard=true)`:

```c++
public OnAllPluginsLoaded()
{
	if (!STAMM_IsAvailable()) 
	{
		SetFailState("Can't Load Feature, Stamm is not installed!");
	}

	STAMM_LoadTranslation();
	STAMM_RegisterFeature("VIP Connect-/Death Messages");
}
```

The parameter of `STAMM_RegisterFeature` is the name of the feature.    
We could also decide if the **feature is default enabled or not** and if the **user can disable the feature**.

The next step is to listen to `STAMM_OnFeatureLoaded`:

```c++
public STAMM_OnFeatureLoaded(const String:basename[])
{

}
```

There we will **read out the block ID's** and check if they are valid:

```c++
public STAMM_OnFeatureLoaded(const String:basename[])
{
	new iBlockConnect = STAMM_GetBlockOfName("connect-message");
	new iBlockDeath = STAMM_GetBlockOfName("death-message");

	if (iBlockConnect == -1 && iBlockDeath == -1)
	{
		SetFailState("Feature couldn't found any block!");
	}
}
```

After this we **add the descriptions of the blocks**.    
We need this to let the clients know that they can achieve the feature.

```c++
public STAMM_OnClientRequestFeatureInfo(client, block, &Handle:array)
{
	decl String:fmt[256];
	
	if (block == STAMM_GetBlockOfName("connect-message"))
	{
		Format(fmt, sizeof(fmt), "%T", "GetConnectMessage", client);
		
		PushArrayString(array, fmt);
	}

	if (block == STAMM_GetBlockOfName("death-message"))
	{
		Format(fmt, sizeof(fmt), "%T", "GetDeathMessage", client);
		
		PushArrayString(array, fmt);
	}
}
```

With the block file above it will notice the client that he **get a connect message on level bronze** and the **death message on level gold**.

For the connect message we use the forward `STAMM_OnClientReady`

```c++
public STAMM_OnClientReady(client)
{

}
```

Here we have to check whether the client can use the feature or not.    
For this we can use the native `STAMM_HaveClientFeature(client, block=1)`, this native checks if the **clients level is high enough** and if the **client wants the feature, so he doesn't disabled it**.    
To write to the players we use our stock `STAMM_PrintToChatAll`:

```c++
public STAMM_OnClientReady(client)
{
	new iBlockConnect = STAMM_GetBlockOfName("connect-message");

	if (STAMM_HaveClientFeature(client, iBlockConnect))
	{
		STAMM_PrintToChatAll("VIP-Player {green}%N joint the server! {red}Yeah!", client);
	}
}
```

The same we do for the death message (We need to hook the death event before).    

```c++
public OnPluginStart()
{
	HookEvent("player_death", eventPlayerDeath);
}

public Action:eventPlayerDeath(Handle:event, const String:name[], bool:dontBroadcast)
{
	new client = GetClientOfUserId(GetEventInt(event, "userid"));

	if (STAMM_IsClientValid(client))
	{
		new iBlockDeath = STAMM_GetBlockOfName("death-message");

		if (STAMM_HaveClientFeature(client, iBlockDeath))
		{
			STAMM_PrintToChatAll("VIP-Player {green}%N died! {red}Oh no ):", client);
		}
	}
}
```

This is now the complete feature:

```c++
#include <sourcemod>
#include <stamm>

public OnPluginStart()
{
	HookEvent("player_death", eventPlayerDeath);
}

public OnAllPluginsLoaded()
{
	if (!STAMM_IsAvailable()) 
	{
		SetFailState("Can't Load Feature, Stamm is not installed!");
	}

	STAMM_LoadTranslation();
	STAMM_RegisterFeature("VIP Connect-/Death Messages");
}

public STAMM_OnFeatureLoaded(const String:basename[])
{
	new iBlockConnect = STAMM_GetBlockOfName("connect-message");
	new iBlockDeath = STAMM_GetBlockOfName("death-message");

	if (iBlockConnect == -1 && iBlockDeath == -1)
	{
		SetFailState("Feature couldn't found any block!");
	}
}

public STAMM_OnClientRequestFeatureInfo(client, block, &Handle:array)
{
	decl String:fmt[256];
	
	if (block == STAMM_GetBlockOfName("connect-message"))
	{
		Format(fmt, sizeof(fmt), "%T", "GetConnectMessage", client);
		
		PushArrayString(array, fmt);
	}

	if (block == STAMM_GetBlockOfName("death-message"))
	{
		Format(fmt, sizeof(fmt), "%T", "GetDeathMessage", client);
		
		PushArrayString(array, fmt);
	}
}

public STAMM_OnClientReady(client)
{
	new iBlockConnect = STAMM_GetBlockOfName("connect-message");

	if (STAMM_HaveClientFeature(client, iBlockConnect))
	{
		STAMM_PrintToChatAll("VIP-Player {green}%N joint the server! {red}Yeah!", client);
	}
}

public Action:eventPlayerDeath(Handle:event, const String:name[], bool:dontBroadcast)
{
	new client = GetClientOfUserId(GetEventInt(event, "userid"));

	if (STAMM_IsClientValid(client))
	{
		new iBlockDeath = STAMM_GetBlockOfName("death-message");

		if (STAMM_HaveClientFeature(client, iBlockDeath))
		{
			STAMM_PrintToChatAll("VIP-Player {green}%N died! {red}Oh no ):", client);
		}
	}
}
```

That's it! **Compile the plugin** and move it to `plugins/stamm`.    
Now **upload all your files** (plugin, translation, block file) and load the feature.


## Features with dynamic blocks

A cool feature are dynamic blocks, so the server admin can create **unlimited blocks** and **each block is better** than the block before.   
Here we want to give VIP's more HP on spawn. Per block the player get 10 percent more!
 
First of all we create a new blocks file:

	"LevelSettings"
	{
		"1"    "Bronze"
		"2"    "Silver"
		"3"    "God"
	}

and a new phrase file:

	"Phrases"
	{
		"GetMoreHpOnSpawn"
		{
			"#format"	"{1:i}"
			"en"		"Get every round {1} Percent more HP"
			"de"		"Bekomme jede Runde {1} Percent mehr HP"
		}
	}

Then we create a new .sp file and hook the spawn event:

```c++
public OnPluginStart()
{
	HookEvent("player_spawn", eventPlayerSpawn);
}
```

also we add the feature:

```c++
public OnAllPluginsLoaded()
{
	if (!STAMM_IsAvailable()) 
	{
		SetFailState("Can't Load Feature, Stamm is not installed!");
	}

	STAMM_LoadTranslation();
	STAMM_RegisterFeature("VIP More HP On Spawn");
}
```

To add the description we need to **set for all blocks a description**:

```c++
public STAMM_OnClientRequestFeatureInfo(client, block, &Handle:array)
{
	decl String:fmt[256];
	
	Format(fmt, sizeof(fmt), "%T", "GetMoreHpOnSpawn", client, (block * 10));
		
	PushArrayString(array, fmt);
}
```

With this code we add a description for the **first block with 10 percent and for (here the second) with 20 percent**, and so on.    
But the server admin can also add more blocks, for e.g:

	"LevelSettings"
	{
		"1"    "Bronze"
		"2"    "Silver"
		"3"    "Platinum"
		"4"    "God"
	}

Now if the client spawn we give him more HP.    
To **get the highest block the client is in**, we use the `STAMM_GetClientBlock` native:

```c++
public PlayerSpawn(Handle:event, String:name[], bool:dontBroadcast)
{
	new client = GetClientOfUserId(GetEventInt(event, "userid"));
	
	if (STAMM_IsClientValid(client))
	{
		if (IsPlayerAlive(client)) 
		{
			new clientBlock = STAMM_GetClientBlock(client);
		
			if (clientBlock > 0)
			{
				new newHP = GetClientHealth(client) + GetClientHealth(client) * (clientBlock / 10);

				SetEntityHealth(client, newHP);
			}
		}
	}
}
```

If the client is in block 2 and has 100 HP, newHp is:    
`100 + 100 * (2 / 10) = 100 + 100 * 0.2 = 100 + 20 = 120`


## Other Stuff

At the end i will show you the **last remaining forwards and natives**.

- **Forward** `STAMM_OnClientChangedFeature(client, bool:turnedOn, bool:isShop)`   
	This forward will be called, when a client turned your feature on or off.    
	The last parameter `isShop` is currently disabled!

- **Native** `STAMM_WantClientFeature(client)`    
	This native return true when the client wants your feature, otherwise false.

- **Native** `STAMM_IsMyFeature(const String:basename[])`    
	This native you can use to check if a given basename is your feature or not.

- **Native** `STAMM_GetBasename(String:basename[], maxlength)`    
	This native will give you the basename of your feature.


**That's it, we're finished :)**