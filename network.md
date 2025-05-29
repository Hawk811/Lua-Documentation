# Table: network

Table containing helper functions for network related features.

## Functions (10)

### `trigger_script_event(bitset, _args)`

Call trigger_script_event (TSE)

- **Parameters:**
  - `bitset` (integer)
  - `_args` (table)

**Example Usage:**
```lua
network.trigger_script_event(bitset, _args)
```

### `get_selected_player()`

- **Returns:**
  - `integer`: Returns the index of the currently selected player in the GUI.

**Example Usage:**
```lua
integer = network.get_selected_player()
```


### `force_script_host(script_name)`

Try to force ourself to be host for the given GTA Script.

- **Parameters:**
  - `script_name` (string): Name of the script

**Example Usage:**
```lua
network.force_script_host(script_name)
```

