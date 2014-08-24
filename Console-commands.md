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

- `stamm_load_feature <basename>`    
	**Loads a Stamm feature** in the `plugins/stamm` folder.

- `stamm_unload_feature <basename>`    
	**Unloads a Stamm feature** in the `plugins/stamm` folder.

- `stamm_reload_feature <basename>`    
	**Reloads a Stamm feature** in the `plugins/stamm` folder.

- `stamm_list_feature`    
	Prints a **list of all features.**

### Database Commands

- `stamm_convert_db <mysql>`    
	If parameter `mysql` is 1 it converts the database **from mysql to sqlite.**    
	If parameter `mysql` is 0 it converts the database **from sqlite to mysql**.    


---------
### [Go to the next Page](How-to-install-a-Feature)