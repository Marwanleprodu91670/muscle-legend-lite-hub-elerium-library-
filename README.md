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

-- Add the "Server" tab to the window
window:AddTab("Server")

-- Anti Ping Button
Server:AddButton("Anti Ping", function()
    local decalsyeeted = true -- Leaving this on reduces visual quality but increases FPS.
    local g = game
    local w = g.Workspace
    local l = g.Lighting
    local t = w.Terrain
    
    -- Set Terrain properties
    t.WaterWaveSize = 0
    t.WaterWaveSpeed = 0
    t.WaterReflectance = 0
    t.WaterTransparency = 0
    
    -- Set Lighting properties
    l.GlobalShadows = false
    l.FogEnd = 9e9
    l.Brightness = 0
    
    -- Set rendering quality
    settings().Rendering.QualityLevel = "Level01"
    
    -- Loop through all descendants and modify materials and properties
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

    -- Disable visual effects in Lighting
    for i, e in pairs(l:GetChildren()) do
        if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect") or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
            e.Enabled = false
        end
    end
end)

-- Anti Kick Button
Server:AddButton("Anti Kick", function()
    wait(0.5)
    
    -- Create the GUI elements for Anti Kick display
    local ba = Instance.new("ScreenGui")
    local ca = Instance.new("TextLabel")
    local da = Instance.new("Frame")
    local _b = Instance.new("TextLabel")
    local ab = Instance.new("TextLabel")
    
    -- Setup GUI elements
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

-- Auto Open Muscle King Crystal (Second Version)
serverTab:AddSwitch("Auto Open Muscle King Crystal (Second Version)", function(value)
    -- This toggle does nothing at the moment, but functionality can be added later.
end)

-- Weight Speed Slider (Premium Only)
Server:AddSlider("Weight Speed (Premium only)", function(p)
    setwalkspeed(p)
end, {
    ["min"] = 0,
    ["max"] = 1000,
})

-- Punch Speed Slider (Premium Only)
Server:AddSlider("Punch Speed (Premium only)", function(p)
    setpunchspeed(p) -- Assuming there's a function `setpunchspeed`
end, {
    ["min"] = 0,
    ["max"] = 1000,
})

-- Set default values for sliders
Server:GetSlider("Weight Speed (Premium only)"):Set(16)
Server:GetSlider("Punch Speed (Premium only)"):Set(16)



-- Default values for the toggles
AutoFarm:GetSwitch("Auto Weight"):Set(false)  -- Default state for Auto Weight is off
AutoFarm:GetSwitch("Auto Pushups (Second Version)"):Set(false)  -- Default state for Auto Pushups is off
AutoFarm:GetSwitch("Situps (Second Version)"):Set(false)  -- Default state for Situps is off
AutoFarm:GetSwitch("Muscle King Farm"):Set(false)  -- Default state for Muscle King Farm is off
Kill:GetSwitch("Auto Kill"):Set(true)  -- Ensure the Auto Kill toggle starts in the "On" position
Kill:GetSwitch("Auto Punch"):Set(false)  -- Default state for Auto Punch is off
Kill:GetSwitch("Kill Target"):Set(false)  -- Default state for Kill Target is off
