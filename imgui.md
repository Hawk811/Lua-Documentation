# Table: imgui

All functions parameters run in script fiber

### `register_draw(imgui_function)`

- **Parameters:**
  - `imgui_function` (imgui)
    
**Example Usage:**
```lua
imgui.register_draw(function()
	local bg_r, bg_g, bg_b, bg_a = 0,  0, 0, 255  -- out of 255
	local window_flags = imgui.flags.NoTitleBar + imgui.flags.NoResize
	imgui.push_style_color(imgui.col.WindowBg, bg_r, bg_g, bg_b, bg_a)
   	if imgui.begin_window("Lua Panel", 400, 300, window_flags) then

        	imgui.text("Text Render")
        	imgui.end_window()
    	end
	imgui.pop_style_color(1)
end)

```

### `begin_window(title, x, y, flags)`

- **Parameters:**
  - `title` (string)
  - `x` (float)
  - `y` (float)
  - `flags` (integer)
    
**Example Usage:**
```lua
local window_flags = imgui.flags.NoTitleBar + imgui.flags.NoResize
imgui.begin_window("Lua Panel", 300, 200, window_flags)
```

### `end_child()`
    
**Example Usage:**
```lua
imgui.end_child()
```

### `text(data)`

- **Parameters:**
  - `data` (string)

**Example Usage:**
```lua
imgui.text("text")
```

### `button(label)`

- **Parameters:**
  - `label ` (string)

**Example Usage:**
```lua
imgui.button("Click me")
```

### `checkbox(label, value, function)`

- **Parameters:**
  - `label` (string)
  - `value` (boolean)
  - `function` (function)

**Example Usage:**
```lua
my_toggle = imgui.checkbox("Enable Feature 2", my_toggle, function(my_toggle) log.info("test: " .. tostring(my_toggle)) end)
OR
imgui.checkbox("Enable Feature", my_toggle, function(val) my_toggle = val log.info("test: " .. tostring(val)) end)
```

### `slider_float(label, value, min, max, function)`

- **Parameters:**
  - `label` (string)
  - `value` (float)
  - `min` (float)
  - `max` (float)
  - `function` (function)

**Example Usage:**
```lua
 my_value = imgui.slider_float("Adjust Value", my_value, 0.0, 1.0, function(v)
            log.info("Slider value changed: " .. tostring(v))
        end)
```

### `slider_int(label, value, min, max, function)`

- **Parameters:**
  - `label` (string)
  - `value` (int)
  - `min` (int)
  - `max` (int)
  - `function` (function)

**Example Usage:**
```lua
 my_value = imgui.slider_int("Adjust Value", my_value, 0.0, 10, function(v)
            log.info("Slider value changed: " .. tostring(v))
        end)
```

### `combo(label, current_item, items, function)`

- **Parameters:**
  - `label` (string)
  - `current_item` (int)
  - `items` (table of strings)
  - `function` (function)

**Example Usage:**
```lua
current_option = imgui.combo("Select Option", current_option, options, function(index)
            log.info("Selected index: " .. index .. ", value: " .. options[index + 1])
        end)
```

### `separator()`

**Example Usage:**
```lua
imgui.separator()
```

### `same_line()`

**Example Usage:**
```lua
imgui.same_line()
```


### `push_style_color(style_enum, r, g, b, a)`

- **Parameters:**
  - `style_enum` (integer)
  - `r` (integer)
  - `g` (integer)
  - `b` (integer)
  - `a` (integer)

**Example Usage:**
```lua
imgui.push_style_color(ImGuiCol_WindowBg, 30, 30, 30, 255)
```

### `pop_style_color(count)`

- **Parameters:**
  - `count` (integer)

**Example Usage:**
```lua
imgui.pop_style_color(1)
```


**Example Code:**
```lua
-- Persistent states
local my_toggle = false
local my_value = 0.5
local slider_val = 5
local current_option = 0
local options = { "Option A", "Option B", "Option C" }

local bg_r, bg_g, bg_b, bg_a = 0,  0, 0, 255  -- out of 255
local window_flags = imgui.flags.NoTitleBar + imgui.flags.NoResize

imgui.register_draw(function()	
	imgui.push_style_color(imgui.col.WindowBg, bg_r, bg_g, bg_b, bg_a)
   if imgui.begin_window("Lua Panel", 400, 300, window_flags) then

        imgui.text("Text Render")

        -- Toggle (update local state)
	my_toggle = imgui.checkbox("Enable Feature 2", my_toggle, function(my_toggle) log.info("test: " .. tostring(my_toggle)) end)
	
	-- float 
	 my_value = imgui.slider_float("Adjust Value", my_value, 0.0, 1.0, function(v)
            log.info("Slider value changed: " .. tostring(v))
        end)
	
	-- int 
	 slider_val = imgui.slider_int("Int Slider", slider_val, 0, 10, function(v)
            log.info("Slider changed to: " .. v)
        end)
	
	-- combo 
 	 current_option = imgui.combo("Select Option", current_option, options, function(index)
            log.info("Selected index: " .. index .. ", value: " .. options[index + 1])
        end)

        -- Button
        imgui.button("Confirm", function()
            log.info("Selected: " .. my_options[my_selected + 1])
        end)

        imgui.end_window()
    end
	 imgui.pop_style_color(1)
end)

```

**Flags and Colors**
```lua
Flags:

NoTitleBar: ImGuiWindowFlags_NoTitleBar
NoResize: ImGuiWindowFlags_NoResize
NoMove: ImGuiWindowFlags_NoMove
NoScrollbar: ImGuiWindowFlags_NoScrollbar
NoScrollWithMouse: ImGuiWindowFlags_NoScrollWithMouse
NoCollapse: ImGuiWindowFlags_NoCollapse
AlwaysAutoResize: ImGuiWindowFlags_AlwaysAutoResize
NoBackground: ImGuiWindowFlags_NoBackground
NoSavedSettings: ImGuiWindowFlags_NoSavedSettings
NoMouseInputs: ImGuiWindowFlags_NoMouseInputs

Usage
local window_flags = imgui.flags.NoTitleBar + imgui.flags.NoResize

Colors:

Text: ImGuiCol_Text
TextDisabled: ImGuiCol_TextDisabled
WindowBg: ImGuiCol_WindowBg
ChildBg: ImGuiCol_ChildBg
PopupBg: ImGuiCol_PopupBg
Border: ImGuiCol_Border
BorderShadow: ImGuiCol_BorderShadow
FrameBg: ImGuiCol_FrameBg
FrameBgHovered: ImGuiCol_FrameBgHovered
FrameBgActive: ImGuiCol_FrameBgActive
TitleBg: ImGuiCol_TitleBg
TitleBgActive: ImGuiCol_TitleBgActive
TitleBgCollapsed: ImGuiCol_TitleBgCollapsed
MenuBarBg: ImGuiCol_MenuBarBg
ScrollbarBg: ImGuiCol_ScrollbarBg
ScrollbarGrab: ImGuiCol_ScrollbarGrab
ScrollbarGrabHovered: ImGuiCol_ScrollbarGrabHovered
ScrollbarGrabActive: ImGuiCol_ScrollbarGrabActive
CheckMark: ImGuiCol_CheckMark
SliderGrab: ImGuiCol_SliderGrab
SliderGrabActive: ImGuiCol_SliderGrabActive
Button: ImGuiCol_Button
ButtonHovered: ImGuiCol_ButtonHovered
ButtonActive: ImGuiCol_ButtonActive
Header: ImGuiCol_Header
HeaderHovered: ImGuiCol_HeaderHovered
HeaderActive: ImGuiCol_HeaderActive
Separator: ImGuiCol_Separator
SeparatorHovered: ImGuiCol_SeparatorHovered
SeparatorActive: ImGuiCol_SeparatorActive
ResizeGrip: ImGuiCol_ResizeGrip
ResizeGripHovered: ImGuiCol_ResizeGripHovered
ResizeGripActive: ImGuiCol_ResizeGripActive
Tab: ImGuiCol_Tab
TabHovered: ImGuiCol_TabHovered
TabActive: ImGuiCol_TabActive
TabUnfocused: ImGuiCol_TabUnfocused
TabUnfocusedActive: ImGuiCol_TabUnfocusedActive
PlotLines: ImGuiCol_PlotLines
PlotLinesHovered: ImGuiCol_PlotLinesHovered
PlotHistogram: ImGuiCol_PlotHistogram
PlotHistogramHovered: ImGuiCol_PlotHistogramHovered
TextSelectedBg: ImGuiCol_TextSelectedBg
ModalWindowDimBg: ImGuiCol_ModalWindowDimBg
DragDropTarget: ImGuiCol_DragDropTarget

Usage
imgui.push_style_color(imgui.col.WindowBg, bg_r, bg_g, bg_b, bg_a)
```
