# Atlas Enhanced Lua API

Welcome to the **Atlas Enhanced Lua API** documentation!  
This project provides powerful scripting capabilities for modding, debugging, and customizing your GTA V experience using Lua.

---

## 📦 Modules Included

Each `.md` file documents a module in the Lua API:

| File              | Description                                 |
|-------------------|---------------------------------------------|
| `network.md`      | Networking utilities (TSE, host forcing, etc.) |
| `notification.md` | Display notifications to the screen         |
| `script.md`       | Register looped or timed Lua functions      |
| `logger.md`       | Logging utilities                           |
| `gui.md`          | GUI window control                          |
| `vector3.md`      | 3D vector type (vec3) with `x`, `y`, `z`    |
| `globals.md`      | Access to global script variables           |
| `locals.md`       | Access to local script variables            |
| `memory.md`       | Read/write raw game memory                  |
| `natives.txt`     | List of known native functions              |

---

## ✅ Example Usage

### Create a new menu and add options:

```lua
mainMenu = menu.add_menu("example", "Example Menu")

mainMenu:add_action("Say Hello", function()
    log.info("Hello from Lua!")
end)

mainMenu:add_toggle("God Mode", false, function(state)
    ENTITY.SET_ENTITY_INVINCIBLE(PLAYER.PLAYER_PED_ID(), state)
end)

mainMenu:add_int("Wanted Level", 0, 0, 5, 1, function(val)
    if val == 0 then
        PLAYER.CLEAR_PLAYER_WANTED_LEVEL(PLAYER.PLAYER_ID())
    else
        PLAYER.SET_PLAYER_WANTED_LEVEL(PLAYER.PLAYER_ID(), val, 0)
        PLAYER.SET_PLAYER_WANTED_LEVEL_NOW(PLAYER.PLAYER_ID(), 0)
    end
end)

mainMenu:add_float("Gravity", 9.8, 0.0, 20.0, 0.1, function(val)
    log.info("Gravity set to " .. val)
end)
