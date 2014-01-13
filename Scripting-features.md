This part of the wiki shows you how to make a feature for Stamm.


## What are blocks

Blocks are used to get information, about when a client should get your feature.
It have to be a .txt file, named like the base-name of your feature and you need to put it in `cfg/stamm/levels`.

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

Here we have two blocks, one for the welcome message and one for the leave message.

If you have specific block name, you can use `STAMM_GetBlockOfName(const String:name[])` to retrieve the ID of the block. E.g. `STAMM_GetBlockOfName("leave")` would be return 2.

If you have the ID of a block and you want the name, you can use `STAMM_GetBlockName(block=1, String:name[], maxlength)`, where block is the ID of the block.

You can retrieve the level ID of a specific block with the native `STAMM_GetBlockLevel(block=1)`.
For the block `name1` and the level settings from the first Page, `STAMM_GetBlockLevel(1)` would return 2, because Silver is the second level.

On top of this there are block descriptions, to let clients know about what happen with what block.

Every block can have up to 100 descriptions. These descriptions are readable in the Stamm menu by the client.
You can add descriptions with the native `STAMM_AddBlockDescription(block=1, const String:description[], any:...)`.

For the block `name1` and the level settings from the first Page, `STAMM_AddBlockDescription(1, "VIP's get a lot of stuff hehe")` would show the client, that he get a lot of stuff, when he becomes Silver VIP. This is because `name1` has the level Silver.

And the last thing about blocks is how to get the block a client is in.

For this there is the native `STAMM_GetClientBlock(client)`. It will return the highest block a client is in.
So in the example, if the client is a Platinum VIP, `STAMM_GetClientBlock(client)` will return 2, because the third block is only for God VIP's, but the second block is for Gold VIP's, and Platinum is higher (or equal) then Gold, so block 2 is the highest block.

You need this especially for [**Features with dynamic blocks**](Scripting-Features#features-with-dynamic-blocks).