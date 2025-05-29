# Table: menu

Table for creating and managing UI menus and submenus.

## Functions (1)

### `add_menu(name, title)`

 Create a new menu and return a SubMenu object to add options into.
 
- **Parameters:**
  - `add_menu` (string, string): Name_id, Title of the tab to get.

- **Returns:**
  - `submenu`: A tab instance which corresponds to the submenu in the GUI.

**Example Usage:**
```lua
mainMenu = menu.add_menu("main", "My Main Menu")
```


# Table: SubMenu

Represents a submenu returned by menu.add_menu. Allows chaining menu options into a specific section.

## Functions (5)

### `add_submenu(name)`

 Create and attach a child submenu to the current submenu.

- **Parameters:**
  - `add_submenu` (string): Name of the child submenu.

- **Returns:**
  - `SubMenu`: A new submenu object.
 
**Example Usage:**
```lua
settingsMenu = mainMenu:add_submenu("Settings")
```

### `add_action(label, callback)`

  Add a clickable action/button to the submenu.

- **Parameters:**
  - `label` (string): Text shown in the UI.
  - `callback` (function): Function to execute when clicked.
 
**Example Usage:**
```lua
 mainMenu:add_action("Say Hello", function()
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
  mainMenu:add_toggle("God Mode", false, function(enabled)
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
  mainMenu:add_int("Speed", 50, 0, 100, 5, function(val)
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
  mainMenu:add_float("Gravity", 9.8, 0.0, 20.0, 0.1, function(val)
        log.info("Gravity set to: " .. val)
    end)
```
