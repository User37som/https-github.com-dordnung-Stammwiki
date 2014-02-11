Now I'll show you how you can install a feature.


## Setup block file

Blocks are used to get information about when a client should get a feature (**Not all features have block files!**).    
You find the block file of a level in `cfg/stamm/levels`.    
It has the **same name like the feature**.

A block file looks like this:

	"LevelSettings"
	{
		"<name_of_the_block>"    "<level_of_the_block>"
		"<name_of_the_block2>"   "<level_of_the_block2>"
	}

What a block means you have to read in the feature description.    
You only have to set the level of the blocks.

Example:
	"LevelSettings"
	{
		"name1"      "Silver"      // This is for all silver VIP's
		"name234"    "Gold"        // This is for all gold VIP's
		"name9"      "God"         // This is for all VIP's higher than Gold
	}

There are also features with unlimited blocks.    
There you can add as much blocks as you want and each block is better than the block before.


## Set config and upload

If the feature has a config, than configure it.    
You may find it in `cfg/stamm/features`.
Upload all files to your server and load the feature.    

---------
### [Go to the next Page](Current-Feature-List)
