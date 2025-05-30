# Table: network

Table containing helper functions for network related features.

## Functions (10)

### `trigger_script_event(bitset, _args)`

Call trigger_script_event (TSE)

- **Parameters:**
  - `event_group` (integer): Usually 1 for host group.
  - `args` (table): A Lua table containing the raw argument values (e.g., integers).
  - `bitset` (integer): Bitmask of target players (e.g., 1 << player_id).
  - `event_id` (integer): The script event ID (typically same as args[0]).

**Example Usage:**
```lua
local target = network.get_selected_player()
local bitset = 1 << target

local args = {
     -503325966,
    PLAYER.PLAYER_ID(),
    bitset,
    0, 0, 0, 0, 0, 0, 0
}

network.trigger_script_event(1, args, bitset,  -503325966)
```

### `get_selected_player()`

- **Returns:**
  - `integer`: Returns the index of the currently selected player in the GUI.

**Example Usage:**
```lua
playerID = network.get_selected_player()
```


### `force_script_host(script_name)`

Try to force ourself to be host for the given GTA Script.

- **Parameters:**
  - `script_name` (string): Name of the script

**Example Usage:**
```lua
network.force_script_host(script_name)
```

