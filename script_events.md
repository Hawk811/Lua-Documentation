# Table: script_events

Table containing helper functions related to gta script events.

## Functions (2)

### `on_event(func)`

- **Parameters:**
  - `func` (function(sender id, event_index, args)).

**Example Usage:**
```lua
script_events.on_event(function(sender_id, event_index, args)
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
