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
-- Main menus
local mainExample = menu.add_menu("Example", "Example Menu")
local mainExample2 = menu.add_menu("Example2", "Example Menu 2")

-- mainExample entries
menu.add_action(mainExample, "Say Hello", function()
    log.info("Hello from Example!")
end)

menu.add_toggle(mainExample, "God Mode", false, function(state)
    ENTITY.SET_ENTITY_INVINCIBLE(PLAYER.PLAYER_PED_ID(), state)
end)

menu.add_int(mainExample, "Wanted Level", 0, 0, 5, 1, function(val)
    if val == 0 then
        PLAYER.CLEAR_PLAYER_WANTED_LEVEL(PLAYER.PLAYER_ID())
	 PLAYER.SET_MAX_WANTED_LEVEL(0)
	MISC.SET_FAKE_WANTED_LEVEL(0)
    else
	 PLAYER.SET_PLAYER_WANTED_LEVEL(PLAYER.PLAYER_ID(), val, 0)
	 PLAYER.SET_MAX_WANTED_LEVEL(5)
        PLAYER.SET_PLAYER_WANTED_LEVEL_NOW(PLAYER.PLAYER_ID(), 0)
	MISC.SET_FAKE_WANTED_LEVEL(0)
    end
end)

menu.add_toggle(mainExample, "Police Ignore", false, function(state)
    PLAYER.SET_POLICE_IGNORE_PLAYER(PLAYER.PLAYER_ID(), state)
end)

menu.add_float(mainExample, "Gravity", 9.8, 0.0, 20.0, 0.1, function(val)
    log.info("Gravity set to " .. val)
end)

-- mainExample2 entries
menu.add_action(mainExample2, "Say Hello", function()
    log.info("Hello from Example2!")
end)

menu.add_action(mainExample2, "Force Script Host", function()
    network.force_script_host("freemode")
end)

-- Loop toggle state
local loop_toggle = true

function my_loop()
    if loop_toggle then
        notification.show("Loop is running")
        script.sleep(3000)
    end
end

script.register_looped(my_loop)

-- Submenu for settings
local settingsMenu = menu.add_submenu(mainExample, "Settings")

menu.add_toggle(settingsMenu, "Enable Loop", true, function(state)
    loop_toggle = state
end)

