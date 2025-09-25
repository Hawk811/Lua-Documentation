# Table: Memory

Table for memory scanning.

## Functions (1)

### `handle_to_ptr(handle)`

 Create a new menu and return a submenu ID (integer handle).
 
- **Parameters:**
  - `handle`: Internal identifier.

- **Returns:**
  - `ptr` A handle of entity.

**Example Usage:**
```lua
local playerPed = PLAYER.PLAYER_PED_ID()
local pedPtr = Memory.handle_to_ptr(playerPed)
log.info(string.format("Player ped pointer: 0x%X", pedPtr))
```

### `ptr_to_handle(ptr)`

- **Parameters:**
  - `ptr`: ptr of entity.

- **Returns:**
  - `handle` A handle representing the entity.

**Example Usage:**
```lua
local handle = Memory.ptr_to_handle(pedPtr)
log.info("Handle: " .. handle)
```

### `allocate(size)`

  Add a clickable action/button to the submenu.

- **Parameters:**
  - `size` (integer): Number of bytes to allocate.

 - **Returns:**
  - `intptr_t`: Pointer to the newly allocated memory block.
    
**Example Usage:**
```lua
local buf = Memory.allocate(64)
log.info("Allocated buffer at: 0x" .. string.format("%X", buf))
```


### `free(buffer)`

  Add a clickable action/button to the submenu.

- **Parameters:**
  - `buffer` (memory): buffer allocated.
 
**Example Usage:**
```lua
Memory.free(buf)
log.info("Buffer freed.")
```

### `Scan(label, pattern)`

- **Parameters:**
    - `label` (string): Name for Pattern.
    - `pattern` (string): pattern in string.

 - **Returns:**
  - `Handle` returns scanned memory Handle.

 - **Memory Class:**
  - .Add(int)
  - .Sub(int)
  - .Rip()
  - .Raw - Returns raw address
  - .get_u8() -> uint8_t
  - .get_u16() -> uint16_t
  - .get_u32() -> uint32_t
  - .get_u64() -> uint64_t
  - .get_float() -> float
  - .get_ptr() -> uintptr_t
  - .get_bool() -> bool
    
  - .set_u8(uint8_t)
  - .set_u16(uint16_t)
  - .set_u32(uint32_t)
  - .set_u64(uint64_t)
  - .set_float(float)
  - .set_bool(bool)
    
  - .is_valid() -> bool
```lua
  Memory.Scan("NEM2", "4C 8B 05 ? ? ? ? 44 0F B7 CA", function(addr)
  local rip_target = addr.Add(3).Rip() 
  log.info(string.format("address of global: 0x%X", rip_target.Raw))
  end)
```


### `BytePatch(label, pattern)`

 - **BytePatch Class:**
.Add(Raw Address, {table})
- .Apply()
- .Restore()
- .Toggle(bool)
- .is_valid() - returns bool

- **Parameters:**
    - `address` (uintptr_t): address.
    - `{}` (array): array of bytes.

 - **Returns:**
  - `Handle` returns BytePatch handle.
    
```lua
Test_Patch = nil
toggleStumble = false
Memory.Scan("CDSS", "56 57 53 48 81 EC ? ? ? ? 44 0F 29 94 24 ? ? ? ? 44 0F 29 4C 24 ? 44 0F 29 44 24 ? 0F 29 7C 24 ? 0F 29 74 24 ? 89 D3",
  function(r0_5947)
    log.info(string.format("address of global: 0x%X", r0_5947.Raw))
    Test_Patch = BytePatch.Add(r0_5947.Raw, { 0xB0, 0x00, 0xC3 })
  end
)

ImGui.register_draw(function()
   if ImGui.Begin("Test Window", menu.is_open()) then

 		value, pressed =ImGui.Checkbox("Test", value)
 		if pressed then
			if Test_Patch and Test_Patch.is_valid() then
            		Test_Patch.Toggle(value)
            		log.info("Patch toggled: " .. tostring(value))
        	end
		end

        ImGui.End()
    end
end)

```
