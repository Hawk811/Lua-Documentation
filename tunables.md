# Table: tunables

Table containing functions for manipulating gta script globals.

## Functions (9)

### `get_int(hash)`

Retrieves an int tunables value.

- **Parameters:**
  - `hash` (integer): index of the tunables

- **Returns:**
  - `integer`: value of the tunables

**Example Usage:**
```lua
integer = tunables.get_int(hash)
```

### `get_float(hash)`

Retrieves a float tunables value.

- **Parameters:**
  - `hash` (integer): index of the tunables

- **Returns:**
  - `float`: value of the tunables

**Example Usage:**
```lua
float = tunables.get_float(hash)
```

### `get_string(hash)`

Retrieves a string tunables value.

- **Parameters:**
  - `hash` (integer): index of the tunables

- **Returns:**
  - `string`: value of the tunables

**Example Usage:**
```lua
string = tunables.get_string(hash)
```

### `set_int(hash, val)`

Sets an int tunables value.

- **Parameters:**
  - `hash` (integer): index of the tunables
  - `val` (integer): new value for the tunables

**Example Usage:**
```lua
tunables.set_int(hash, val)
```

### `set_float(hash, val)`

Sets a float tunables value.

- **Parameters:**
  - `hash` (integer): index of the tunables
  - `val` (float): new value for the tunables

**Example Usage:**
```lua
tunables.set_float(hash, val)
```

### `set_string(hash, str)`

Sets a string tunables value.

- **Parameters:**
  - `hash` (integer): index of the tunables
  - `str` (string): new value for the tunables

**Example Usage:**
```lua
tunables.set_string(hash, str)
```

