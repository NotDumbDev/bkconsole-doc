## **.init()**

!!!description
    Initializes BKConsole.

!!!paramater
    [Admins: {number}](API.md#init, "A table of user IDs.")

!!!returns
    "Success"
    "Fail"
    "Wrong_context"

### Usage:
```luau
local admins = {
    134567890
}

BKConsole.init(admins)
```

## **.setActivationKey()**

!!!description
    Sets the Open or Close key for BKConsole.

!!!paramater
    [activationKey: string? | Enum.Keycode?](API.md#setactivationkey, "Either a string or a Enum Item.")

### Usage:
```luau
BKConsole.setActivationKey("F2")
--or
BKConsole.setActivationKey(Enum.Keycode.F2)
```

## **.registerCommand()**

!!!description
    Registers a command.

!!!paramater
    [commandName: string](API.md#registercommand, "The name of the command")

    [description: string](API.md#registercommand, "The description of the command")

    [arguments: {}?](API.md#registercommand, "The arguments of the command (For autocompletion).") `OPTIONAL`

    [callback: (any) -> () ](API.md#registercommand, "The actual arguments of the command.")
    
    [onRanMessage: string](API.md#registercommand, "A message which will run after the command has ran, replacing the default text.") `OPTIONAL`


### Usage:
```luau
local arguments = {
    ["kick"] = {
        { name = "kickPlayer", type = "string" },
        { name = "reason", type = "string" },
    }
}

BKConsole.registerCommand("Kick", "Kicks a player.", arguments["kick"], function(player: Player, kickPlayer: string, reason: string) 
	local target = Players:FindFirstChild(kickPlayer)
	if target then
		target:Kick(reason)
	end
end, "Successfully kicked player.")
```

## **.runCommand()**

!!!description
    Runs a registered command.

!!!paramater
    [commandName: string](API.md#runcommand, "The name of the command")

    [arguments: {}?](API.md#runCommand, "The arguments of the command (Do not pass a Player as the first argument!).")

    [player: Player](API.md#runCommand, "The player who executed the command.")

!!!returns
    "Success"
    "Fail"
    "Unknown"


### Usage:
```luau
BKConsole.runCommand("Kick", {"Roblox", "Broke RP Rule Nr3201 Paragraph 2."}, player)
```