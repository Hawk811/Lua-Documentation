# Table: script_events

Table containing helper functions related to gta script events.

## Functions (2)

### `on_event(func)`

- **Parameters:**
  - `func` (function(sender id, event_index, args)).

**Example Usage:**
```lua
ScriptEventIndex = {
    Bounty = 1517551547
    -- more
}


local bounty_protection_enabled = true
script_events.on_event(function(sender_id, event_index, args)
    if not bounty_protection_enabled then
        return true -- skip protection, allow event
    end

    if event_index == ScriptEventIndex.Bounty then
        local target = args[1]
        local amount = args[3]

        if target == PLAYER.PLAYER_ID() then
            if amount >= 10000 then
                notification.show("Blocked 10k+ bounty from Player " .. tostring(sender_id))
            else
                notification.show("Blocked bounty from Player " .. tostring(sender_id))
            end
            return false
        end
    end

    return true
end)
```
