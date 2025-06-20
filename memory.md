# Table: memory

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
local pedPtr = memory.handle_to_ptr(playerPed)
log.info(string.format("Player ped pointer: 0x%X", pedPtr:get_ptr()))
```

### `ptr_to_handle(ptr)`

- **Parameters:**
  - `ptr`: ptr of entity.

- **Returns:**
  - `handle` A handle representing the entity.

**Example Usage:**
```lua
local handle = memory.ptr_to_handle(pedPtr)
log.info("Handle: " .. handle)
```


### `allocate(size)`

 Create and attach a child submenu to the current submenu.

- **Parameters:**
  - `size` (int): size of buffer.

- **Returns:**
  - `buffer` returns buffer.
 
**Example Usage:**
```lua
local buf = memory.allocate(128)
log.info(string.format("Allocated buffer: 0x%X", buf:get_ptr()))

OR

local mem = memory.allocate(16)

mem:set_u32(1337)
local v = mem:get_u32()
log.info("Value is: ", v)  -- should be 1337

mem:set_float(3.14)
local f = mem:get_float()
log.info("Float is: ", f)

memory.free(mem)
```

### `free(buffer)`

  Add a clickable action/button to the submenu.

- **Parameters:**
  - `buffer` (memory): buffer allocated.
 
**Example Usage:**
```lua
memory.free(buf)
log.info("Buffer freed.")
```

### `pattern(label, pattern):scan()`

- **Parameters:**
    - `label` (string): Name for Pattern.
    - `pattern` (string): pattern in string.

 - **Returns:**
  - `memory type class` returns scanned memory.

 - **Memory Class:**
  - add(intptr_t)
  - sub(intptr_t)
  - rip()
    
  - get_u8() -> uint8_t
  - get_u16() -> uint16_t
  - get_u32() -> uint32_t
  - get_u64() -> uint64_t
  - get_float() -> float
  - get_ptr() -> uintptr_t
    
  - set_u8(uint8_t)
  - set_u16(uint16_t)
  - set_u32(uint32_t)
  - set_u64(uint64_t)
  - set_float(float)
    
  - is_valid() -> bool
```lua
ptr:set_u8(0xFF)
ptr:set_u16(0xBEEF)
ptr:set_u32(12345)
ptr:set_u64(0xDEADBEEFCAFEBABE)
ptr:set_float(3.14159)
```

**Example Usage:**
```lua
-- === 1) Scan for a pattern ===
local p = memory.pattern("MyPattern", "72 C7 EB 02 31 C0 8B 0D"):scan()

if p:is_valid() then
    -- === 2) Compute the final address ===
    local ripTarget = p:add(0x1A):rip()

    -- === 3) Read the original value ===
    local original = ripTarget:get_u32()
    log.info(string.format("Original u32: 0x%X", original))

    -- === 4) Write a new value ===
    ripTarget:set_u32(1337)
    log.info("Set new u32: 1337")

    -- === 5) Verify that it changed ===
    local updated = ripTarget:get_u32()
    log.info(string.format("Updated u32: 0x%X", updated))
else
    log.info("Pattern not found.")
end
```


**Example LUA:**
```lua
   -- === 1) Get player ped handle and pointer ===
local ped = PLAYER.PLAYER_PED_ID()
local pedPtr = memory.handle_to_ptr(ped)
print(string.format("[1] Player ped pointer: 0x%X", pedPtr:get_ptr()))

-- === 2) Convert pointer back to handle ===
local handleAgain = memory.ptr_to_handle(pedPtr)
print(string.format("[2] Pointer back to handle: %d", handleAgain))

-- === 3) Allocate a buffer ===
local buf = memory.allocate(64)
print(string.format("[3] Allocated buffer: 0x%X", buf:get_ptr()))

-- === 4) Write to it (if you have set_* bound) or read default ===
-- Here we just read: should be zero
local val = buf:get_u32()
print(string.format("[4] Buffer initial u32: %d", val))

-- === 5) Pattern scan example ===
local pattern = memory.pattern("TestPattern", "72 C7 EB 02 31 C0 8B 0D")
local match = pattern:scan()
if match:is_valid() then
    local addr = match:add(0x1A):rip()
    local patVal = addr:get_u32()
    print(string.format("[5] Pattern scan value: 0x%X", patVal))
else
    print("[5] Pattern not found.")
end

-- === 6) Free the buffer ===
memory.free(buf)
print("[6] Buffer freed.")
```
