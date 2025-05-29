# Submenu

**Example Usage:**

```lua
missionsTab = gui.add_submenu("My Lua Submenu")
missionsTab:add_button("Click me", function ()
    logger.info("You clicked!")
end)
```
