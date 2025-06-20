# Table: util

## Functions (1)

### `is_key_pressed(key)`

returns is key pressed.
 
- **Parameters:**
  - `key` (int): id for key.

- **Returns:**
  - `bool` .

**Example Usage:**
```lua
if util.is_key_pressed(0x41) then -- 'A' key
    log.info("A is pressed")
end
```

### `joaat(name)`

returns is key pressed.
 
- **Parameters:**
  - `name` (string): name to convert to hash.

- **Returns:**
  - `uint32_t` . return hash

**Example Usage:**
```lua
local freemode_hash = util.joaat("freemode") 
```
