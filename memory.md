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
log.info(string.format("Player ped pointer: 0x%X", pedPtr))
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
log.info(string.format("Allocated buffer: 0x%X", memory.get_ptr(buf)))

OR

local mem = memory.allocate(16)

memory.set_u32(mem, 1337)
local v = memory.get_u32(mem)
log.info("Value is: ", v)  -- should be 1337

memory.set_float(mem, 3.14)
local f = memory.get_float(mem)
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

### `pattern(label, pattern)`

- **Parameters:**
    - `label` (string): Name for Pattern.
    - `pattern` (string): pattern in string.

 - **Returns:**
  - `Address` returns scanned memory.

 - **Memory Class:**
  - memory.add(intptr_t)
  - memory.sub(intptr_t)
  - memory.rip()
    
  - memory.get_u8(address) -> uint8_t
  - memory.get_u16(address) -> uint16_t
  - memory.get_u32(address) -> uint32_t
  - memory.get_u64(address) -> uint64_t
  - memory.get_float(address) -> float
  - memory.get_ptr(address) -> uintptr_t
  - memory.get_bool(address) -> bool
    
  - memory.set_u8(address, uint8_t)
  - memory.set_u16(address, uint16_t)
  - memory.set_u32(address, uint32_t)
  - memory.set_u64(address, uint64_t)
  - memory.set_float(address, float)
  - memory.set_bool(address, bool)
    
  - memory.is_valid(address) -> bool
```lua
memory.set_u8(ptr, 0xFF)
memory.set_u16(ptr, 0xBEEF)
memory.set_u32(ptr, 12345)
memory.set_u64(ptr, 0xDEADBEEFCAFEBABE)
memory.set_float(ptr, 3.14159)
memory.set_bool(ptr, true)
```

**Example Usage:**
```lua
-- === 1) Scan for a pattern ===
local addr = memory.pattern("NPMLUA", "0F B6 05 ? ? ? ? 0A 05 ? ? ? ? 75 2A")
if memory.is_valid(addr) then
    log.info(string.format("Found pattern at: 0x%X", addr))

    local new_addr = memory.add(addr, 3)
    local ripped_addr = memory.rip(new_addr) -- dereference RIP displacement

    local bool_val = memory.get_bool(ripped_addr)
    log.info("Bool value at ripped address (0x" .. string.format("%X", ripped_addr) .. "): " .. tostring(bool_val))
end
```


**Example LUA:**
```lua
   -- === 1) Get player ped handle and pointer ===
local ped = PLAYER.PLAYER_PED_ID()
local pedPtr = memory.handle_to_ptr(ped)
log.info(string.format("[1] Player ped pointer: 0x%X", pedPtr))

-- === 2) Convert pointer back to handle ===
local handleAgain = memory.ptr_to_handle(pedPtr)
log.info(string.format("[2] Pointer back to handle: %d", handleAgain))

-- === 3) Allocate a buffer ===
local buf = memory.allocate(64)
log.info(string.format("[3] Allocated buffer: 0x%X", memory.get_ptr(buf)))

-- === 4) Write to it (if you have set_* bound) or read default ===
-- Here we just read: should be zero
local val = memory.get_u32(buf)
log.info(string.format("[4] Buffer initial u32: %d", val))

-- === 5) Pattern scan example ===
local pattern = memory.pattern("TestPattern", "72 C7 EB 02 31 C0 8B 0D")
if memory.is_valid(pattern) then
    local addr = memory.add(pattern, 0x1A):rip()
    local rippedaddr = memory.rip(addr)
    local patVal = memory:get_u32(rippedaddr)
    log.info(string.format("[5] Pattern scan value: 0x%X", patVal))
else
    log.info("[5] Pattern not found.")
end

-- === 6) Free the buffer ===
memory.free(buf)
log.info("[6] Buffer freed.")
```


### `byte_patch(label, pattern)`

- **Parameters:**
    - `address` (uintptr_t): address.
    - `{}` (array): array of bytes.

 - **Returns:**
  - `address` returns ready address [void*].

 - **Memory Class:**
  - memory.apply_patch(address)
  - memory.restore_patch(address)
    
```lua
local addr = memory.pattern("GCGP", "48 8B 54 C1 ? 4C 8B A9")
local patch_addr = memory.byte_patch(addr, { 0x90, 0x90, 0x90, 0x90, 0x90 })

function my_loop()
	script.yield()
    if not TASK.IS_PED_STILL(PLAYER.PLAYER_PED_ID()) then
       memory.apply_patch(patch_addr)
    else
	      memory.restore_patch(patch_addr)
    end
end

script.register_looped(my_loop)
```
