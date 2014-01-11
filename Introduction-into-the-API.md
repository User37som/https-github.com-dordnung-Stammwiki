## General Introduction ##

Hey, welcome to the Stamm Developer Wiki. Great to see that you wanna use the API.
 
Let me tell you, it's easier to use the API as you thought.

Just read the next pages and learn how to work with it.


## Where to start ##

The API is divided in six parts. 

- [**The core part**](Working-with-stamm)
- [**The client part**](Working-with-clients)
- [**The color part**](Colors-in-Stamm)
- [**The level part**](Working-with-levels)
- [**The feature part**](Scripting-Features)
- [**The block part**](Scripting-Features)

You can use the core, client, color and level part without making a feature,
for the feature and block part you need to add a feature. 


## What are levels ##

Stamm supports currently up to 100 levels.

There are two kind of levels: Public and private ones. 

Public levels are achievable with points by every client, private levels are only for clients with specific admin flags.

Levels are configurated by the server admin in `cfg/stamm/StammLevels.txt`.

This is the default file:

	"StammLevels"
	{
		"bronze"
		{
			"name"      "Bronze"
			"points"    "500"
		}
		"silver"
		{
			"name"      "Silver"
			"points"    "1000"
		}
		"gold"
		{
			"name"      "Gold"
			"points"    "1500"
		}
		"platinum"
		{
			"name"      "Platinum"
			"points"    "2000"
		}
		"diamond"
		{
			"name"      "Diamond"
			"points"    "2500"
		}
		"god"
		{
			"name"      "God"
			"points"    "3000"
		}
		//"special"
		//{
		//  "name"      "Special"
		//  "flag"      "abt"
		//}
	}

It simply says, that you become `Bronze VIP with 500 points`, `Silver VIP with 1000 points`, and so on.

The last level (default disabled) is a private one, it uses instead of points a flag string.

So by default there are 6 levels. The first level always get the ID 1, the second one the ID 2, and so on. These IDs are unique, so you can use them later one.

To get more information about levels, read [**Working with levels**](Working-with-levels)



## What are blocks ##

Blocks are used to get information, about when a client should get your feature.
It have to be a .txt file, named like the basename of your feature and you need to put it in `cfg/stamm/levels`.

You can set up to 100 blocks in the file.

A block file looks like this:

	"LevelSettings"
	{
		"<name_of_the_block>"    "<level_of_the_block>"
		"<name_of_the_block2>"   "<level_of_the_block2>"
	}

The name have to be defined by yourself, it have to be unique and can be retrieved with the API.
The level have to be set by the server admin, it links the block with a specific level.

The block ID is the position number of a block in the block file, beginning from 1.
Example:

	"name1"      "Silver"      // This will be ID 1
	"name234"    "Gold"        // This will be ID 2
	"name9"      "Platinum"    // This will be ID 3

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

Here we have two blocks, one for the welcome message and one for the leave message.

If you have specific block name, you can use `STAMM_GetBlockOfName(const String:name[])` to retrieve the ID of the block. E.g. `STAMM_GetBlockOfName("leave")` would be return 2

If you have the ID of a block and you want the name, you can use `STAMM_GetBlockName(block=1, String:name[], maxlength)`, where block is the ID of the block.

You can retrieve the level ID of a specific block with the native `STAMM_GetBlockLevel(block=1)`.
For the block `name1` and the level settings from the first Page, `STAMM_GetBlockLevel(1)` would return 2, because Silver is the second level.

The last thing about blocks are the block descriptions.

Every block can have up to 100 descriptions. These descriptions are readable in the stamm menu by the client.
You can add descriptions with the native `STAMM_AddBlockDescription(block=1, const String:description[], any:...)`.

For the block `name1` and the level settings from the first Page, `STAMM_AddBlockDescription(1, "VIP's get a lot of stuff hehe")` would show the client, that he get a lot of stuff, when he becomes Silver VIP. This is because `name1` has the level Silver.