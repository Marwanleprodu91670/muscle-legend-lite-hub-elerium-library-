local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

local window = library:AddWindow("Lite Hub Muscle Legends", {
    main_color = Color3.fromRGB(41, 74, 122),
    min_size = Vector2.new(450, 340),
    toggle_key = Enum.KeyCode.RightShift,
    can_resize = true,
})

-- Variables
local AutoKillToggle = false
local AutoPunchToggle = false
local KillTargetToggle = false
local AutoWeightToggle = false
local AutoPushupsToggle = false
local SitupsToggle = false
local MuscleKingFarmToggle = false
local punchTool = nil  -- Variable to store the "Punch" tool
local weightTool = nil  -- Variable to store the "Weight" tool
local pushupsTool = nil  -- Variable to store the "Pushups" tool
local situpsTool = nil  -- Variable to store the "Situps" tool
local targetPlayerName = ""  -- Variable to store the target player name

-- Function to handle the Auto Punch functionality
local function AutoPunch()
    spawn(function()
        while AutoPunchToggle do
            local player = game.Players.LocalPlayer
            local punchTool = player.Backpack:FindFirstChild("Punch") or player.Character:FindFirstChild("Punch")
            
            if punchTool then
                -- Equip the Punch tool if it's found
                player.Character.Humanoid:EquipTool(punchTool)

                -- Use the Punch tool by activating it
                punchTool:Activate()
            end
            
            wait(0.1) -- Adjust frequency of tool activation to your needs
        end
    end)
end

-- Function to handle the Auto Weight functionality
local function AutoWeight()
    spawn(function()
        while AutoWeightToggle do
            local player = game.Players.LocalPlayer
            local weightTool = player.Backpack:FindFirstChild("Weight") or player.Character:FindFirstChild("Weight")
            
            if weightTool then
                -- Equip the Weight tool if it's found
                player.Character.Humanoid:EquipTool(weightTool)

                -- Use the Weight tool by activating it
                weightTool:Activate()
            end
            
            wait(0.1) -- Adjust frequency of tool activation to your needs
        end
    end)
end

-- Function to handle the Auto Pushups (Second Version) functionality
local function AutoPushups()
    spawn(function()
        while AutoPushupsToggle do
            local player = game.Players.LocalPlayer
            local pushupsTool = player.Backpack:FindFirstChild("Pushups") or player.Character:FindFirstChild("Pushups")
            
            if pushupsTool then
                -- Equip the Pushups tool if it's found
                player.Character.Humanoid:EquipTool(pushupsTool)

                -- Use the Pushups tool by activating it
                pushupsTool:Activate()
            end
            
            wait(0.1) -- Adjust frequency of tool activation to your needs
        end
    end)
end

-- Function to handle the Situps (Second Version) functionality
local function AutoSitups()
    spawn(function()
        while SitupsToggle do
            local player = game.Players.LocalPlayer
            local situpsTool = player.Backpack:FindFirstChild("Situps") or player.Character:FindFirstChild("Situps")
            
            if situpsTool then
                -- Equip the Situps tool if it's found
                player.Character.Humanoid:EquipTool(situpsTool)

                -- Use the Situps tool by activating it
                situpsTool:Activate()
            end
            
            wait(0.1) -- Adjust frequency of tool activation to your needs
        end
    end)
end

-- Function to handle the Muscle King Farm functionality
local function MuscleKingFarm()
    spawn(function()
        while MuscleKingFarmToggle do
            local player = game.Players.LocalPlayer
            -- Teleport the player to the specified location
            player.Character.HumanoidRootPart.CFrame = CFrame.new(-8546.25879, 23.045435, -5636.78418)

            -- Equip the "Pushups" tool
            local pushupsTool = player.Backpack:FindFirstChild("Pushups") or player.Character:FindFirstChild("Pushups")
            if pushupsTool then
                player.Character.Humanoid:EquipTool(pushupsTool)
                pushupsTool:Activate()  -- Use the Pushups tool by activating it
            end
            
            wait(0.1)  -- Adjust frequency of tool activation to your needs
        end
    end)
end

-- Auto Farm Tab
local AutoFarm = window:AddTab("Auto Farm")

-- Add Auto Weight toggle in Auto Farm Tab
AutoFarm:AddSwitch("Auto Weight", function(value)
    AutoWeightToggle = value  -- Update the AutoWeight toggle state
    if AutoWeightToggle then
        AutoWeight()  -- Start the Auto Weight loop when the toggle is enabled
    end
end)

-- Add Auto Pushups toggle in Auto Farm Tab
AutoFarm:AddSwitch("Auto Pushups (Second Version)", function(value)
    AutoPushupsToggle = value  -- Update the AutoPushups toggle state
    if AutoPushupsToggle then
        AutoPushups()  -- Start the Auto Pushups loop when the toggle is enabled
    end
end)

-- Add Situps toggle in Auto Farm Tab
AutoFarm:AddSwitch("Situps (Second Version)", function(value)
    SitupsToggle = value  -- Update the Situps toggle state
    if SitupsToggle then
        AutoSitups()  -- Start the Auto Situps loop when the toggle is enabled
    end
end)

-- Add Muscle King Farm toggle in Auto Farm Tab
AutoFarm:AddSwitch("Muscle King Farm", function(value)
    MuscleKingFarmToggle = value  -- Update the MuscleKingFarm toggle state
    if MuscleKingFarmToggle then
        MuscleKingFarm()  -- Start the Muscle King Farm loop when the toggle is enabled
    end
end)

-- Kill Tab
local Kill = window:AddTab("Kill")

-- Add switches (toggles)
Kill:AddSwitch("Auto Kill", function(value)
    AutoKillToggle = value  -- Update the AutoKill toggle state
end)

-- Add Auto Punch toggle in Kill Tab
Kill:AddSwitch("Auto Punch", function(value)
    AutoPunchToggle = value  -- Update the AutoPunch toggle state
    if AutoPunchToggle then
        AutoPunch()  -- Start the Auto Punch loop when the toggle is enabled
    end
end)

-- Add label "Target Player" under the Auto Punch toggle
Kill:AddLabel("Target Player")

-- Add Kill Target toggle
Kill:AddSwitch("Kill Target", function(value)
    KillTargetToggle = value  -- Update the KillTarget toggle state
end)

-- Add textbox to input the target player's name
Kill:AddTextBox("Select Target", function(text)
    targetPlayerName = text  -- Update the target player name when the textbox is filled
end)



local tab = window:AddTab("Server")

-- Add the first slider called "Fast Weight (Premium Only)"
local slider1 = tab:AddSlider("Fast Weight (Premium Only)", function(p)
    -- This slider does nothing for now
end, {
    ["min"] = 0,
    ["max"] = 100,
})
slider1:Set(0)  -- Initial value

-- Add the second slider called "Fast Punch (Premium Only)"
local slider2 = tab:AddSlider("Fast Punch (Premium Only)", function(p)
    -- This slider does nothing for now
end, {
    ["min"] = 0,
    ["max"] = 100,
})
slider2:Set(0)  -- Initial value

-- Add the toggle called "Hatch Muscle King Pets (new Version V2)"
local switch = tab:AddSwitch("Hatch Muscle King Pets (new Version V2)", function(bool)
    -- This toggle does nothing for now
end)
switch:Set(true)





-- Default values for the toggles
AutoFarm:GetSwitch("Auto Weight"):Set(false)  -- Default state for Auto Weight is off
AutoFarm:GetSwitch("Auto Pushups (Second Version)"):Set(false)  -- Default state for Auto Pushups is off
AutoFarm:GetSwitch("Situps (Second Version)"):Set(false)  -- Default state for Situps is off
AutoFarm:GetSwitch("Muscle King Farm"):Set(false)  -- Default state for Muscle King Farm is off
Kill:GetSwitch("Auto Kill"):Set(true)  -- Ensure the Auto Kill toggle starts in the "On" position
Kill:GetSwitch("Auto Punch"):Set(false)  -- Default state for Auto Punch is off
Kill:GetSwitch("Kill Target"):Set(false)  -- Default state for Kill Target is off
