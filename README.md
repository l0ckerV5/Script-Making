# Script-Making
**Tutorial/Templates**

> User Whitelist System

```
local usernames= {
	"Player Name",
	"Player Name" -- Username of the Whitelisted Players
}

game.Players.PlayerAdded:Connect(function(plr)
	for i, v in pairs(usernames) do
		if v == plr.Name then
			print("Whitelisted")
		else
			print("Not whitelisted")
			plr:Kick("Not whitelisted") -- Kick message.
		end
	end
end)
```

> Game Whitelist

```
local validGameId = 12345678910 --Change this to your game ID

local function kickPlayer(player, message)
    player:Kick(message)
end

if game.PlaceId == validGameId then
    Put your script here
else
    game.Players.PlayerAdded:Connect(function(player)
        kickPlayer(player, "Invalid Game")
    end)

    for _, player in ipairs(game.Players:GetPlayers()) do
        kickPlayer(player, "Invalid Game")
    end
end
```

> Clothing Changer

```
local SHIRT_ID = 123456789  --Replace this with your shirts ID
local PANTS_ID = 987654321  --Replace this with your shirts ID

local function changeShirt(character)
    local shirt = character:FindFirstChildOfClass("Shirt")
    if shirt then
        shirt.ShirtTemplate = "rbxassetid://" .. SHIRT_ID
    else
        local newShirt = Instance.new("Shirt")
        newShirt.ShirtTemplate = "rbxassetid://" .. SHIRT_ID
        newShirt.Parent = character
    end
end

local function changePants(character)
    local pants = character:FindFirstChildOfClass("Pants")
    if pants then
        pants.PantsTemplate = "rbxassetid://" .. PANTS_ID
    else
        local newPants = Instance.new("Pants")
        newPants.PantsTemplate = "rbxassetid://" .. PANTS_ID
        newPants.Parent = character
    end
end

local function onCharacterAdded(character)
    changeShirt(character)
    changePants(character)
end

local function onPlayerAdded(player)
   player.CharacterAdded:Connect(onCharacterAdded)
end

game.Players.PlayerAdded:Connect(onPlayerAdded)

for _, player in ipairs(game.Players:GetPlayers()) do
    onPlayerAdded(player)
end
```

> Position Grabber
This sends a notification of your roblox character's position

```
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

local iconUrl = "http://www.roblox.com/asset/?id=6023426925"

local function sendPositionNotification()
    local position = character.PrimaryPart.Position
    local message = string.format("Your current position is: X: %.2f, Y: %.2f, Z: %.2f", position.X, position.Y, position.Z)
    
    game.StarterGui:SetCore("SendNotification", {
        Title = "Player Position",
        Text = message,
        Icon = iconUrl,
        Duration = 10
    })
end

sendPositionNotification()

while true do
    wait(10)
    sendPositionNotification()
end
```
