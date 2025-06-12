# Table: script

Table containing helper functions related to gta scripts.

## Functions (2)

### `register_looped(func)`

Registers a function that will be looped as a gta script.
**Example Usage:**
```lua
script.register_looped(function (script)
     -- sleep until next game frame
     script.yield()

     local ModelHash = joaat("adder")
     if not STREAMING.IS_MODEL_IN_CDIMAGE(ModelHash) then return end
     STREAMING.REQUEST_MODEL(ModelHash) -- Request the model
     while not STREAMING.HAS_MODEL_LOADED(ModelHash) do -- Waits for the model to load
         script:yield()
     end
     local myPed = PLAYER.PLAYER_PED_ID()
     local myCoords = ENTITY.GET_ENTITY_COORDS(myPed, true)
     -- Spawns a networked vehicle on your current coords
     local spawnedVehicle = VEHICLE.CREATE_VEHICLE(ModelHash, myCoords.x, myCoords.y, myCoords.z, ENTITY.GET_ENTITY_HEADING(myPed), true, false)
     -- removes model from game memory as we no longer need it
     STREAMING.SET_MODEL_AS_NO_LONGER_NEEDED(ModelHash)
     -- sleep for 2s
     script.sleep(2000)
     ENTITY.DELETE_ENTITY(spawnedVehicle)
end)
```

- **Parameters:**
  - `func` (function): function that will be executed in a forever loop.

**Example Usage:**
```lua
script.register_looped(func)
```

### `run_in_fiber(func)`

Executes a function once inside the fiber pool, you can call natives inside it and yield or sleep.
**Example Usage:**
```lua
script.run_in_fiber(function (script)
     -- sleep until next game frame
     script.yield()

     local ModelHash = joaat("adder")
     if not STREAMING.IS_MODEL_IN_CDIMAGE(ModelHash) then return end
     STREAMING.REQUEST_MODEL(ModelHash) -- Request the model
     while not STREAMING.HAS_MODEL_LOADED(ModelHash) do -- Waits for the model to load
         script:yield()
     end
     local myPed = PLAYER.PLAYER_PED_ID()
     local myCoords = ENTITY.GET_ENTITY_COORDS(myPed, true)
     -- Spawns a networked vehicle on your current coords
     local spawnedVehicle = VEHICLE.CREATE_VEHICLE(ModelHash, myCoords.x, myCoords.y, myCoords.z, ENTITY.GET_ENTITY_HEADING(myPed), true, false)
     -- removes model from game memory as we no longer need it
     STREAMING.SET_MODEL_AS_NO_LONGER_NEEDED(ModelHash)
     -- sleep for 2s
     script.sleep(2000)
     ENTITY.DELETE_ENTITY(spawnedVehicle)
end)
```

- **Parameters:**
  - `func` (function): function that will be executed once in the fiber pool.

**Example Usage:**
```lua
script.run_in_fiber(func)
```

### `execute_as_script(script_name, func)`

Executes a function once in desired script.
**Example Usage:**
```lua
script.execute_as_script("freemode", function (script)
     -- sleep until next game frame
     script.yield()

     local ModelHash = joaat("adder")
     if not STREAMING.IS_MODEL_IN_CDIMAGE(ModelHash) then return end
     STREAMING.REQUEST_MODEL(ModelHash) -- Request the model
     while not STREAMING.HAS_MODEL_LOADED(ModelHash) do -- Waits for the model to load
         script:yield()
     end
     local myPed = PLAYER.PLAYER_PED_ID()
     local myCoords = ENTITY.GET_ENTITY_COORDS(myPed, true)
     -- Spawns a networked vehicle on your current coords
     local spawnedVehicle = VEHICLE.CREATE_VEHICLE(ModelHash, myCoords.x, myCoords.y, myCoords.z, ENTITY.GET_ENTITY_HEADING(myPed), true, false)
     -- removes model from game memory as we no longer need it
     STREAMING.SET_MODEL_AS_NO_LONGER_NEEDED(ModelHash)
     -- sleep for 2s
     script.sleep(2000)
     ENTITY.DELETE_ENTITY(spawnedVehicle)
end)
```

- **Parameters:**
  - `script name` (string): name of script to excute script in.
  - `func` (function): function that will be executed once in the fiber pool.

**Example Usage:**
```lua
script.execute_as_script(script_name, func)
```

### `is_active(script_name)`

returns if script is active

- **Parameters:**
  - `func` (script_name):  name of script.
  - 
**Exemple Usage:**
```lua
if script.is_active("freemode") then
     log.info("freemode is active")
end
```


### `yield()`

Yield execution.

**Exemple Usage:**
```lua
script.yield()
```

### `sleep(ms)`

Sleep for the given amount of time, time is in milliseconds.

- **Parameters:**
  - `ms` (integer): The amount of time in milliseconds that we will sleep for.

**Exemple Usage:**
```lua
script.sleep(ms)
```

