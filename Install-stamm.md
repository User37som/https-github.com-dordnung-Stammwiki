Hey, welcome to the **Stamm Server Admin Wiki**. Great to see that you wanna use Stamm.

Just read the next pages and **learn how to use Stamm.**


# Setup levels

Stamm supports currently **up to 100 levels**.

There are two kind of levels: **Public and private ones**. 

Public levels are **achievable by every client with points**, private levels are only for clients with **specific admin flags**.

A public level has the following structure:

	// You need this name for the feature level settings, it must be unique
	"<name>"
	{
		// This is the name of your level. The Players see this name!
		"name"		"<levelname>"
	
		// This defines, how much points a player need to get this level
		"points"	"<points>"
	}

And private level has the following structure:

	// You need this name for the feature level settings, it must be unique
	"<name>"
	{
		// This is the name of your level. The Players see this name!
		"name"		"<levelname>"

		// This defines the flag a player need to access this private level
		"flag"	"<adminflag>"
	}


You can **configure the levels** in `cfg/stamm/StammLevels.txt`.

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

You can **change this file**, with the structures from above, **as you like.**

So if you only want two levels, named **Urban and City** at 1000 and 2000 points, than use:

	"StammLevels"
	{
		"urbanlevel"
		{
			"name"      "Urban"
			"points"    "1000"
		}

		"citylevel"
		{
			"name"      "City"
			"points"    "2000"
		}
	}

And so on.

## Configure the database

You can use **SQLite or MySQL** to save the database stuff.     
If you use SQLite, than you don't have to do anything on the database file.

If you use MySQL than create a `stamm_sql` entry in the `addons/sourcemod/config/database.cfg` file:

	"stamm_sql"
	{
		"driver"			"mysql"
		"host"				"YOUR MYSQL HOST"
		"database"			"YOUR MYSQL DATABASE NAME"
		"user"				"YOUR MYSQL USERNAME"
		"pass"				"YOUR MYSQL PASSWORD"
	}

Just edit the **host, database, user and pass** fields with your data.    
Notice: The MySQL database **must be an external database!**


## Set config and upload

As the last step open `cfg/stamm/stamm_config.cfg` and edit the settings as you like!

	// GENERAL SETTINGS
	
	
	
	// Stamm Tag to use in Chat. Use this for a CSGO Server
	// -
	// Default: "{lightgreen}[ {green}Stamm {lightgreen}]"
	stamm_tag "{lightgreen}[ {green}Stamm {lightgreen}]"
	
	
	// Stamm Tag to use for CSS, DODS and TF2 with morecolors support. This will overwrite the stamm_tag cvar.
	// -
	// Default: "{strange}[ {mediumseagreen}Stamm {strange}]"
	stamm_tag_morecolors "{strange}[ {mediumseagreen}Stamm {strange}]"
	
	
	// How to get Points, 1=kills, 2=rounds, 3=time, 4=kills&rounds, 5=kills&time, 6=rounds&time, 7=kills&rounds&time
	// -
	// Default: "1"
	stamm_vip_type "1"
	
	
	// If you set points for time: How much minutes are one point?
	// -
	// Default: "1"
	stamm_time_point "1"
	
	
	// If you have more than one Server, type here your Server number in, e.g. 1. Server = 1. This will be append to the table name
	// -
	// Default: "1"
	stamm_serverid "1"
	
	
	// Your Stamm Table Name. It appends '_<serverid>' at the end!
	// -
	// Default: "STAMM_DB"
	stamm_table_name "STAMM_DB"
	
	
	// 1 = Give less Players more Points, with factor: ((max players on your server) - (current players)) / 4, 0 = disable
	// -
	// Default: "0"
	stamm_extrapoints "0"
	
	
	// Flags a player needs to access the stamm admin menu (see addons/sourcemod/configs/admin_levels.cfg for all flags)
	// -
	// Default: "bt"
	stamm_adminflag "bt"
	
	
	// Flags a player needs to get instantly highest VIP (see addons/sourcemod/configs/admin_levels.cfg for all flags), 0 = Off
	// -
	// Default: "0"
	stamm_oflag "0"
	
	
	// x = Days until a inactive player gets deleted, 0 = Off
	// -
	// Default: "0"
	stamm_delete "0"
	
	
	// x = Days until a inactive player starts losing points, 0 = Off
	// -
	// Default: "0"
	stamm_delete_points "0"
	
	
	// x = Points a player loses for being inactive
	// -
	// Default: "2"
	stamm_delete_points_count "2"
	
	
	// x = Interval in hours, after being inactive, in which a player will losing the specific points
	// -
	// Default: "24"
	stamm_delete_points_interval "24"
	
	
	// Shows every x Seconds all Players their Points (480 = 8 minutes), 0 = Off
	// -
	// Default: "480"
	stamm_showpoints "480"
	
	
	// Info Message Interval in seconds (300 = 5 minutes), 0 = Off
	// -
	// Default: "300"
	stamm_infotime "300"
	
	
	// Path to the level up sound, beginning after sound/, 0 = Off
	// -
	// Default: "stamm/lvlup.mp3"
	stamm_lvl_up_sound "stamm/lvlup.mp3"
	
	
	// Number of Players, which have to be on the Server, to count points
	// -
	// Default: "0"
	stamm_min_player "0"
	
	
	// 1 = When a Player join, he see his points, 0 = OFF
	// -
	// Default: "1"
	stamm_join_show "1"
	
	
	// 1 = All see the players points, 0 = only the player, who write it in the chat
	// -
	// Default: "1"
	stamm_see_text "1"
	
	
	// 1 = Use levelname in chat instead of term "VIP", 0 = Use term "VIP"
	// -
	// Default: "0"
	stamm_striptag "0"
	
	
	// 1 = Player sees a menu when typing stamm command, 0 = Just a chat message
	// -
	// Default: "0"
	stamm_usemenu "0"
	
	
	// 1 = Players see a notify when they get points through kill/round/time, 0 = Disable
	// -
	// Default: "1"
	stamm_text_on_points "1"
	
	
	// 1 = Auto Update Stamm and it's features (Needs the Auto Updater), 0 = Off
	// -
	// Default: "1"
	stamm_autoupdate "1"
	
	
	// (Only TF2) 1 = Show points always on HUD, 0 = Off
	// -
	// Default: "1"
	stamm_hudtext "1"
	
	
	// 1 = Log in an extra File lot of information(Enable this if you have problems!), 0=disable
	// -
	// Default: "0"
	stamm_debug "0"
	
	
	
	
	// COMMAND SETTINGS (add sm_ for a sourcemod console command, it adds automatically ! or / instead of sm_ for chat use)
	
	
	
	// Command to see current points
	// -
	// Default: "sm_stamm"
	stamm_texttowrite "sm_stamm"
	
	
	// Command for Admin Menu
	// -
	// Default: "sm_sadmin"
	stamm_admin_menu "sm_sadmin"
	
	
	// Command to see infos about stamm
	// -
	// Default: "sm_sinfo"
	stamm_info_cmd "sm_sinfo"
	
	
	// Command to put ones features on/off
	// -
	// Default: "sm_schange"
	stamm_change_cmd "sm_schange"
	
	
	// Command for VIP Top 10
	// -
	// Default: "sm_slist"
	stamm_viplist "sm_slist"
	
	
	// Command for VIP Rank
	// -
	// Default: "sm_srank"
	stamm_viprank "sm_srank"

Finally upload all files and restart your server.    
Now you are finished with the core Stamm plugin.


## Report Bugs

If you have a bug than you can report it either on the sourcemod forum or here in Github.

To fix a bug i need the `sourcemod/logs` folder!


---------
### [Go to the next Page](Console-Commands)