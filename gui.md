# Table: menu

Table for creating and managing UI menus and submenus.

## Functions (1)

### `add_menu(name, title)`

 Create a new menu and return a submenu ID (integer handle).
 
- **Parameters:**
  - `name` (string): Internal identifier.
  - `title` (string): Title shown in the UI.

- **Returns:**
  - `int` A handle representing the submenu.

**Example Usage:**
```lua
mainMenu = menu.add_menu("main", "My Main Menu")
```

### `add_submenu(parent_id, name)`

 Create and attach a child submenu to the current submenu.

- **Parameters:**
  - `parent_id` (int): Handle of the parent submenu.
  - `name` (string): Name of the child submenu.

- **Returns:**
  - `int` A new submenu handle.
 
**Example Usage:**
```lua
settingsMenu = menu.add_submenu(mainMenu, "Settings")
```

### `add_action(label, callback)`

  Add a clickable action/button to the submenu.

- **Parameters:**
  - `label` (string): Text shown in the UI.
  - `callback` (function): Function to execute when clicked.
 
**Example Usage:**
```lua
 menu.add_action(mainMenu, "Say Hello", function()
        log.info("Hello from Lua")
    end)
```

### `add_toggle(label, value, callback?)`

 Add a toggle (checkbox) to the submenu.

- **Parameters:**
    - `label` (string): Display name of the toggle.
    - `value` (boolean): Initial toggle state (true or false).
    - `callback` (function, optional): Called when toggled with the new state.
 
**Example Usage:**
```lua
 menu.add_toggle(mainMenu, "God Mode", false, function(enabled)
        ENTITY.SET_ENTITY_INVINCIBLE(PLAYER.PLAYER_PED_ID(), enabled)
    end)
```


### `add_int(label, value, min, max, step, callback?)`

  Add an integer slider to the submenu.

- **Parameters:**
    - `label` (string): Display name.
    - `value` (integer): Initial value.
    - `min` (integer): Minimum value.
    - `max` (integer): Maximum value.
    - `step` (integer): Step between values.
    - `callback` (function, optional): Called when value is changed.
 
**Example Usage:**
```lua
   menu.add_int(mainMenu, "Speed", 50, 0, 100, 5, function(val)
        log.info("Speed set to: " .. val)
    end)
```


### `add_float(label, value, min, max, step, callback?)`

    Add a float slider to the submenu.

- **Parameters:**
    - `label` (string): Display name.
    - `value` (float): Initial value.
    - `min` (float): Minimum value.
    - `max` (float): Maximum value.
    - `step` (float): Step between values.
    - `callback` (function, optional): Called when value is changed.
 
**Example Usage:**
```lua
   menu.add_float(mainMenu, "Gravity", 9.8, 0.0, 20.0, 0.1, function(val)
        log.info("Gravity set to: " .. val)
    end)
```
