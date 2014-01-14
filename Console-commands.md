There are a few commands to **use on the console:**

### Happy Hour Commands

- `stamm_start_happyhour <time> <factor>`    
	This **starts the happy hour.**    
	**Time is the runtime** in seconds, **factor the multiplication factor** for the points.

- `stamm_stop_happyhour`    
	This **stops the happy hour.**

### Point Commands

- `stamm_set_points <userid|steamid> <points>`    
	**Sets the Stamm points** of a player.    
    You can use a userid or a steamid.

- `stamm_add_points <userid|steamid> <points>`    
	**Adds Stamm points** to the Stamm points of a player.    
    You can use a userid or a steamid.

- `stamm_del_points <userid|steamid> <points>`    
	**Deletes Stamm points** from the Stamm points of a player.   
    You can use a userid or a steamid.

### Feature Commands

- `stamm_feature_load <basename>`    
	**Loads a Stamm feature** in the `plugins/stamm` folder.

- `stamm_feature_unload <basename>`    
	**Unloads a Stamm feature** in the `plugins/stamm` folder.

- `stamm_feature_reload <basename>`    
	**Reloads a Stamm feature** in the `plugins/stamm` folder.

- `stamm_feature_list`    
	Prints a **list of all features.**

### Database Commands

- `stamm_convert_db <mysql>`    
	If parameter `mysql` is 1 its converts the database **from mysql to sqlite.**    
	If parameter `mysql` is 0 its converts the database from **sqlite to mysql**.    