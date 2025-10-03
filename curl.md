# Table: menu

Table for creating options in ui. This uses the imgui bindings. 

## Functions (3)

### `on_draw(function)`

 creates a tab in scripting with lua name.

**Example Usage:**
```lua
menu.on_draw(function()
    if ImGui.BeginTabBar("my_tabs") then   -- starts tab bar

        -- Tab 1
        if ImGui.BeginTabItem("Tab 1") then
            ImGui.Text("This is inside Tab 1")

            -- Open a header block
            ImGui.ListHeader("Quick Actions", 180)
            for i = 1, 10 do
                if ImGui.Button("Button " .. i) then
                    log.info("Clicked Button " .. i)
                end
            end
            ImGui.EndListHeader()         -- close header block

            ImGui.EndTabItem()            -- close Tab 1
        end

    end
end)


```

### `on_draw_player(function)`

 creates a tab in players section with lua name.

**Example Usage:**
```lua
menu.on_draw_player(function()
    if ImGui.BeginTabBar("my_tabs") then   -- starts tab bar

        -- Tab 1
        if ImGui.BeginTabItem("Tab 1") then
            ImGui.Text("This is inside Tab 1")

            -- Open a header block
            ImGui.ListHeader("Quick Actions", 180)
            for i = 1, 10 do
                if ImGui.Button("Button " .. i) then
                    log.info("Clicked Button " .. i)
                end
            end
            ImGui.EndListHeader()         -- close header block

            ImGui.EndTabItem()            -- close Tab 1
        end

    end
end)


```

### `is_open()`

 Returns if UI is open.

- **Returns:**
  - `bool` A handle representing if UI is open.

**Example Usage:**
```lua
local isUIOpen = menu.is_open()
```
