local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

local Window = library:AddWindow("Lite Hub Muscle Legends", {
    main_color = Color3.fromRGB(41, 74, 122),
    min_size = Vector2.new(450, 340),
    toggle_key = Enum.KeyCode.RightShift,
    can_resize = true,
})

-- Variables
local autoPushupsEnabled = false
local autoSitupsEnabled = false
local autoWeightEnabled = false
local autoHandstandsEnabled = false


-- Function to toggle Auto Pushups
function AutoPushups()
    spawn(function()
        while autoPushupsEnabled do
            local player = game.Players.LocalPlayer
            local pushupsTool = player.Backpack:FindFirstChild("Pushups") or player.Character:FindFirstChild("Pushups")
            
            if pushupsTool then
                player.Character.Humanoid:EquipTool(pushupsTool)
                pushupsTool:Activate()
            end
            wait(0.1)
        end
    end)
end

-- Function to toggle Auto Situps
function AutoSitups()
    spawn(function()
        while autoSitupsEnabled do
            local player = game.Players.LocalPlayer
            local situpsTool = player.Backpack:FindFirstChild("Situps") or player.Character:FindFirstChild("Situps")
            
            if situpsTool then
                player.Character.Humanoid:EquipTool(situpsTool)
                situpsTool:Activate()
            end
            wait(0.1)
        end
    end)
end

-- Function to toggle Auto Weight
function AutoWeight()
    spawn(function()
        while autoWeightEnabled do
            local player = game.Players.LocalPlayer
            local weightTool = player.Backpack:FindFirstChild("Weight") or player.Character:FindFirstChild("Weight")
            
            if weightTool then
                player.Character.Humanoid:EquipTool(weightTool)
                weightTool:Activate()
            end
            wait(0.1)
        end
    end)
end

-- Function to toggle Auto Handstands
function AutoHandstands()
    spawn(function()
        while autoHandstandsEnabled do
            local player = game.Players.LocalPlayer
            local handstandsTool = player.Backpack:FindFirstChild("Handstands") or player.Character:FindFirstChild("Handstands")
            
            if handstandsTool then
                player.Character.Humanoid:EquipTool(handstandsTool)
                handstandsTool:Activate()
            end
            wait(0.1)
        end
    end)
end






local Auto Farm = Window:AddTab("Auto Farm")

-- Toggle for Pushups
Auto Farm:AddSwitch("Pushups", false, function(state)
    autoPushupsEnabled = value
        if value then
            AutoPushups()
        end
end)

Auto Farm:AddSwitch("Situps", false, function(state)
    autoSitupsEnabled = value
        if value then
            AutoSitups()
        end
end)

Auto Farm:AddSwitch("Weight", false, function(state)
    autoWeightEnabled = value
        if value then
            AutoWeight()
        end
end)

Auto Farm:AddSwitch("Handstands", false, function(state)
    autoHandstandsEnabled = value
        if value then
            AutoHandstands()
        end
end)


