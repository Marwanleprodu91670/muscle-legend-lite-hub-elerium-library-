local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

local window = library:AddWindow("Lite Hub Muscle Legends BETA", {
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

-- Define a function to teleport the target player's head to your right hand
local function teleportHeadsToRightHand()
    local player = game.Players.LocalPlayer
    local character = player.Character

    -- Make sure the character exists
    if character then
        local rightHand = character:WaitForChild("RightHand", 5) -- Timeout to prevent indefinite waiting
        if rightHand then
            -- Loop through all players
            for _, targetPlayer in pairs(game.Players:GetPlayers()) do
                local targetCharacter = targetPlayer.Character
                
                -- Check if the target player has a character and a head
                if targetCharacter and targetCharacter:FindFirstChild("Head") then
                    local targetHead = targetCharacter.Head
                    -- Set the target player's head position to your right hand position
                    targetHead.CFrame = rightHand.CFrame
                end
            end
        end
    end
end

-- Define the function to handle the switch state
local function handleAutoKillSwitch(bool)
    if bool then
        -- The toggle is ON, start teleporting players' heads to your right hand
        while switch:Get() do
            teleportHeadsToRightHand()
            -- Wait for a brief moment before repeating the process
            wait(0.1)
        end
    else
        -- The toggle is OFF, stop the teleporting (loop exits naturally)
    end
end

-- Add the switch to the features and bind it to the handleAutoKillSwitch function
Kill:AddSwitch("Auto Kill", handleAutoKillSwitch)

-- Set the initial state of the switch to ON (if you want it to start as active)
switch:Set(true)


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

local features = window:AddTab("Settings") -- Name of tab

-- Add "Anti Ping" button to the settings tab
local antiPingButton = features:AddButton("Anti Ping", function()
    -- Your Anti Ping Code
    local decalsyeeted = true -- Leaving this on makes games look shitty but the fps goes up by at least 20.
    local g = game
    local w = g.Workspace
    local l = g.Lighting
    local t = w.Terrain
    t.WaterWaveSize = 0
    t.WaterWaveSpeed = 0
    t.WaterReflectance = 0
    t.WaterTransparency = 0
    l.GlobalShadows = false
    l.FogEnd = 9e9
    l.Brightness = 0
    settings().Rendering.QualityLevel = "Level01"
    
    for i, v in pairs(g:GetDescendants()) do
        if v:IsA("Part") or v:IsA("Union") or v:IsA("CornerWedgePart") or v:IsA("TrussPart") then
            v.Material = "Plastic"
            v.Reflectance = 0
        elseif v:IsA("Decal") or v:IsA("Texture") and decalsyeeted then
            v.Transparency = 1
        elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then
            v.Lifetime = NumberRange.new(0)
        elseif v:IsA("Explosion") then
            v.BlastPressure = 1
            v.BlastRadius = 1
        elseif v:IsA("Fire") or v:IsA("SpotLight") or v:IsA("Smoke") then
            v.Enabled = false
        elseif v:IsA("MeshPart") then
            v.Material = "Plastic"
            v.Reflectance = 0
            v.TextureID = 10385902758728957
        end
    end

    for i, e in pairs(l:GetChildren()) do
        if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect") or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
            e.Enabled = false
        end
    end
end)

-- Add "Anti Kick" button to the settings tab
local antiKickButton = features:AddButton("Anti Kick", function()
    -- Anti Kick Code
    wait(0.5)
    local ba = Instance.new("ScreenGui")
    local ca = Instance.new("TextLabel")
    local da = Instance.new("Frame")
    local _b = Instance.new("TextLabel")
    local ab = Instance.new("TextLabel")

    ba.Parent = game.CoreGui
    ba.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

    ca.Parent = ba
    ca.Active = true
    ca.BackgroundColor3 = Color3.new(0.176471, 0.176471, 0.176471)
    ca.Draggable = true
    ca.Position = UDim2.new(0.698610067, 0, 0.098096624, 0)
    ca.Size = UDim2.new(0, 370, 0, 52)
    ca.Font = Enum.Font.SourceSansSemibold
    ca.Text = "Anti Afk"
    ca.TextColor3 = Color3.new(0, 1, 1)
    ca.TextSize = 22

    da.Parent = ca
    da.BackgroundColor3 = Color3.new(0.196078, 0.196078, 0.196078)
    da.Position = UDim2.new(0, 0, 1.0192306, 0)
    da.Size = UDim2.new(0, 370, 0, 107)

    _b.Parent = da
    _b.BackgroundColor3 = Color3.new(0.176471, 0.176471, 0.176471)
    _b.Position = UDim2.new(0, 0, 0.800455689, 0)
    _b.Size = UDim2.new(0, 370, 0, 21)
    _b.Font = Enum.Font.Arial
    _b.Text = "Made by luca#5432"
    _b.TextColor3 = Color3.new(0, 1, 1)
    _b.TextSize = 20

    ab.Parent = da
    ab.BackgroundColor3 = Color3.new(0.176471, 0.176471, 0.176471)
    ab.Position = UDim2.new(0, 0, 0.158377, 0)
    ab.Size = UDim2.new(0, 370, 0, 44)
    ab.Font = Enum.Font.ArialBold
    ab.Text = "Status: Active"
    ab.TextColor3 = Color3.new(0, 1, 1)
    ab.TextSize = 20

    local bb = game:service'VirtualUser'
    game:service'Players'.LocalPlayer.Idled:connect(function()
        bb:CaptureController()
        bb:ClickButton2(Vector2.new())
        ab.Text = "Roblox tried kicking you but I didn't let them!"
        wait(2)
        ab.Text = "Status: Active"
    end)
end)

local features = window:AddTab("Spy")

-- Create the toggle for "Spy Player"
local switch = features:AddSwitch("Spy Player", function(bool)
    -- Will be executed when the toggle is turned on or off
    if bool then
        local username = playerTextbox:GetText()
        if username and username ~= "" then
            -- Spectate the player if the username is valid
            spectatePlayer(username)
        end
    else
        -- Stop spectating the player if the toggle is off
        stopSpectating()
    end
end)

switch:Set(false)

-- Create the textbox to write the player's username
local playerTextbox = features:AddTextBox("Write Player Username", function(text)
    -- Textbox callback (you can add validation here if needed)
    print("Username entered: " .. text)
end)

-- Function to start spectating the player
function spectatePlayer(username)
    local player = game.Players:FindFirstChild(username)
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        -- Ensure the player and their character are valid
        local camera = game.Workspace.CurrentCamera
        camera.CameraSubject = player.Character.Humanoid
        camera.CameraType = Enum.CameraType.Custom
        print("Now spectating " .. username)
    else
        warn("Player not found or no valid character")
    end
end

-- Function to stop spectating
function stopSpectating()
    local camera = game.Workspace.CurrentCamera
    camera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
    camera.CameraType = Enum.CameraType.Custom
    print("Stopped spectating")
end


-- Assuming you're using a UI framework that has `AddTab`, `AddLabel`, and `AddButton` methods.

-- Create the teleportation tab
local features = window:AddTab("Teleport")

-- Add a label to the teleportation tab
features:AddLabel("Islands:")

-- Teleport function (already corrected)
local function teleportToIsland(position)
    local player = game.Players.LocalPlayer
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local humanoidRootPart = player.Character.HumanoidRootPart
        humanoidRootPart.CFrame = CFrame.new(position)
    else
        warn("Player character or HumanoidRootPart not found.")
    end
end

-- Add buttons to teleport to different islands
features:AddButton("Tiny Island", function()
    teleportToIsland(Vector3.new(-38.4037132, 9.66723633, 1832.29114))
end)

features:AddButton("Frost Island", function()
    teleportToIsland(Vector3.new(-2533.64258, 13.7738762, -408.134796))
end)

features:AddButton("Mythical Island", function()
    teleportToIsland(Vector3.new(2170.5437, 13.8738737, 1073.75525))
end)

features:AddButton("Inferno Island", function()
    teleportToIsland(Vector3.new(-6678.75635, 13.8738737, -1285.4198))
end)

features:AddButton("Legend Island", function()
    teleportToIsland(Vector3.new(4685.5625, 997.608765, -3910.30908))
end)

features:AddButton("Muscle King Island", function()
    teleportToIsland(Vector3.new(-8546.25879, 23.045435, -5636.78418))
end)

-- Ensure the window is visible (if needed for your UI framework)
window:Show()  -- Or whatever method your framework uses to show the window










-- Default values for the toggles
AutoFarm:GetSwitch("Auto Weight"):Set(false)  -- Default state for Auto Weight is off
AutoFarm:GetSwitch("Auto Pushups (Second Version)"):Set(false)  -- Default state for Auto Pushups is off
AutoFarm:GetSwitch("Situps (Second Version)"):Set(false)  -- Default state for Situps is off
AutoFarm:GetSwitch("Muscle King Farm"):Set(false)  -- Default state for Muscle King Farm is off
Kill:GetSwitch("Auto Kill"):Set(true)  -- Ensure the Auto Kill toggle starts in the "On" position
Kill:GetSwitch("Auto Punch"):Set(false)  -- Default state for Auto Punch is off
Kill:GetSwitch("Kill Target"):Set(false)  -- Default state for Kill Target is off
