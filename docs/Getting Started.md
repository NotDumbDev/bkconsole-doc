# Getting Started

## Setup

Once you've downloaded **BKConsole**, follow the steps below to get it to work:

1. Create a **Script** under `ServerScriptService`.
2. Require the BKConsole module.
3. Initialize BKConsole using `BKConsole.init(admins)`, where `admins` is a table of user IDs for users allowed to access BKConsole.

### Example Setup

```luau
local Players = game:GetService("Players")
local BKConsole = require(path.to.bkconsole)

-- User IDs of players who can use BKConsole
local admins = {
	1234567890
}

Players.PlayerAdded:Connect(function(player: Player)
	-- Wait for the player's character to load
	player.CharacterAdded:Connect(function()
		BKConsole.init(admins)
	end)
end)
```
!!! note
    Replace path.to.bkconsole with the actual path to your BKConsole module.

!!! info
    The init function returns either "Success" or "Fail". if you want, you can bind these to additional functions, for example: registering the commands after the init is done.

## Setting an activation key
To open or close BKConsole, you need to bind an activation key. This key can either be an `Enum.KeyCode` or a `string`.

=== "Using Enum.Keycode"

    ```luau
        Players.PlayerAdded:Connect(function(player: Player)
            player.CharacterAdded:Connect(function()
                BKConsole.init(admins)
                BKConsole.setActivationKey(Enum.Keycode.F2) -- With Enum.Keycode
            end)
        end)
    ```
=== "Using a String"

    ```luau
        Players.PlayerAdded:Connect(function(player: Player)
            player.CharacterAdded:Connect(function()
                BKConsole.init(admins)
                BKConsole.setActivationKey("F2") -- With a String
            end)
        end)
    ```

!!!info
    When using a string, make sure the case matches exactly with the corresponding Enum name.

    - BKConsole.setActivationKey("f2") - Incorrect :octicons-x-circle-fill-12:
    - BKConsole.setActivationKey("F2") - Correct :octicons-check-16:

    You can update the activation key at any time during runtime.
    

## Registering a command
BKConsole comes with a few built-in commands, but they might not cover all your needs. To create custom commands, use the BKConsole.registerCommand() function.

### Commad Example

```luau
local Players = game:GetService("Players")

-- Define expected arguments for autocomplete and type checking
local arguments = {
    ["kick"] = {
        { name = "kickPlayer", type = "string" },
        { name = "reason", type = "string" },
    }
}

BKConsole.registerCommand("Kick", "Kicks a player.", arguments["kick"], function(player: Player, kickPlayer: string, reason: string) 
    -- player must ALWAYS be the first argument in the function.
	local target = Players:FindFirstChild(kickPlayer)
	if target then
		target:Kick(reason)
	end
end, "Successfully kicked player.")
```

Click [here](API.md#registercommand) to learn the registerCommand function more in depth.

!!!info
    If you want autocomplete support, you must provide a table of argument definitions. This tells BKConsole what argument types to expect. If you don't need autocomplete, you can pass nil instead.

## Running a command using a script

!!!info
    You can also run commands via a script and its fairly easy. To run a command using a script, use
    BKConsole.runCommand() and pass the required paramaters.

### Usage Example
```luau
BKConsole.runCommand("Kick", {"Roblox", "Broke RP Rule Nr3201 Paragraph 2."}, player)
```

Click [here](API.md#runcommand) to learn the runCommand function more in depth.