Hey, welcome to the Stamm Developer Wiki. Great to see that you wanna use the API.
 
Let me tell you: It's easier to use the API as you thought.

Just read the next pages and learn how to work with it.


## Where to start

The API is divided in six parts. 

- [**The core part**](Working-with-Stamm)
- [**The client part**](Working-with-clients)
- [**The color part**](Colors-in-Stamm)
- [**The level part**](Working-with-levels)
- [**The feature part**](Scripting-Features)
- [**The block part**](Scripting-Features#what-are-blocks)

You can use the core, client, color and level part without making a feature,
for the feature and block part you need to add a feature. 


## What are levels

Stamm supports currently up to 100 levels.

There are two kind of levels: Public and private ones. 

Public levels are achievable with points by every client, private levels are only for clients with specific admin flags.

Levels are configured by the server admin in `cfg/stamm/StammLevels.txt`.

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

It simply says, that you become Bronze VIP with `500 points`, Silver VIP with `1000 points`, and so on.

Here is the last level (default disabled) a private one, it uses a flag string instead of points.

So by default there are 6 levels. The first level always get the ID 1, the second one the ID 2, and so on. These IDs are unique, so you can use them later one.

To get more information about levels, read [**Working with levels**](Working-with-levels).


---------
### [Go to the next Page](Working-with-Stamm)