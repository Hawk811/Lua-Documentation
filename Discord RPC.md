# Table: discord

Table containing functions for custom disocrd RPC in Menu.

## Functions (3)

### `init(app_id)`

Initializes the RPC with your Application ID

- **Parameters:**
  - `app_id` (int)

**Example Usage:**
```lua
discord.init("123456789012345678") -- Replace with your App ID
```

### `update_presence(details, state)`

Add the desired text to the RPC

- **Parameters:**
  - `details` (string)
  - `state` (string)

**Example Usage:**
```lua
discord.update_presence("Modding GTA V", "In Free Mode") -- Replace with your App ID
```

### `shutdown()`

Shutsdown the RPC.

**Example Usage:**
```lua
discord.shutdown()
```
