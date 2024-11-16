local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

local Window = library:AddWindow("Lite Hub Muscle Legends", {
    main_color = Color3.fromRGB(41, 74, 122),
    min_size = Vector2.new(450, 340),
    toggle_key = Enum.KeyCode.RightShift,
    can_resize = true,
})

--variables
-- Variables
local autoPushupsEnabled = false
local autoSitupsEnabled = false
local autoWeightEnabled = false
local autoHandstandsEnabled = false
local autoPunchEnabled = false
local autoKillEnabled = false
local whitelistEnabled = false
local killTargetEnabled = false
local spyPlayerEnabled = false
local selectedWhitelistPlayer = nil
local selectedTargetPlayer = nil
local selectedSpyPlayer = nil
local lockPositionEnabled = false
local selectedPosition = CFrame.new(0, 0, 0)
local AutoKillToggle = false



--functions
--another variable to make script still work after player die
local function onCharacterAdded(character)
    character:WaitForChild("Humanoid") -- Wait for the Humanoid to load

    -- Reinitialize any required toggles or tools here
    if autoPushupsEnabled then AutoPushups() end
    if autoSitupsEnabled then AutoSitups() end
    if autoWeightEnabled then AutoWeight() end
    if autoHandstandsEnabled then AutoHandstands() end
    if autoPunchEnabled then AutoPunch() end
    if autoKillEnabled then AutoKill() end
    if killTargetEnabled then KillTarget() end
end

local player = game.Players.LocalPlayer

-- Initial character setup
if player.Character then
    onCharacterAdded(player.Character)
end

-- Connect the character added event
player.CharacterAdded:Connect(onCharacterAdded)


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

-- Function to toggle Auto Punch
function AutoPunch()
    spawn(function()
        while autoPunchEnabled do
            local player = game.Players.LocalPlayer
            local punchTool = player.Backpack:FindFirstChild("Punch") or player.Character:FindFirstChild("Punch")
            
            if punchTool then
                player.Character.Humanoid:EquipTool(punchTool)
                punchTool:Activate()
            end
            wait(0.1)
        end
    end)
end

local function autoKillPlayers()
    -- Loop to continuously check Auto Kill toggle
    spawn(function()
        while AutoKillToggle do
            -- Get the player and character
            local player = game.Players.LocalPlayer
            local character = player.Character or player.CharacterAdded:Wait()
            
            -- Get the right hand of the character
            local rightHand = character:FindFirstChild("RightHand")
            
            -- Check if the right hand exists
            if rightHand then
                -- Loop through all players in the game
                for _, target in pairs(game.Players:GetPlayers()) do
                    -- Check that the target is a valid player and is not the local player
                    if target ~= player and target.Character and target.Character:FindFirstChild("Head") then
                        -- Check for whitelist if enabled
                        if not (whitelistEnabled and target.Name == selectedWhitelistPlayer) then
                            -- Teleport the target's head to the right hand's position
                            target.Character.Head.CFrame = rightHand.CFrame
                        end
                    end
                end
            end
            -- Wait a short time before repeating the loop
            wait(0.1) -- Delay for smoother execution
        end
    end)
end

-- Function to toggle Kill Target
function KillTarget()
    spawn(function()
        while killTargetEnabled do
            local player = game.Players.LocalPlayer
            local character = player.Character or player.CharacterAdded:Wait()
            local rightHand = character:FindFirstChild("RightHand")

            if rightHand and selectedTargetPlayer then
                local targetPlayer = game.Players:FindFirstChild(selectedTargetPlayer)
                if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("Head") then
                    targetPlayer.Character.Head.CFrame = rightHand.CFrame
                end
            end
            wait(0.1)
        end
    end)
end

-- Function to toggle Spy Player
function SpyPlayer()
    spawn(function()
        while spyPlayerEnabled do
            if selectedSpyPlayer then
                local targetPlayer = game.Players:FindFirstChild(selectedSpyPlayer)
                if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("Head") then
                    workspace.CurrentCamera.CameraSubject = targetPlayer.Character.Humanoid
                end
            end
            wait(0.1)
        end
    end)
end

-- Function to reset camera to local player
function ResetCamera()
    workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
end

-- Function to lock or unlock player position
function LockPosition()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    
    if lockPositionEnabled then
        humanoid.PlatformStand = true -- Freeze the player
    else
        humanoid.PlatformStand = false -- Unfreeze the player
    end
end

-- Function to refresh player list for dropdown
local function RefreshPlayerList()
    local players = {}
    for _, player in pairs(game.Players:GetPlayers()) do
        if player.Name ~= game.Players.LocalPlayer.Name then
            table.insert(players, player.Name)
        end
    end
    return players
end

-- Function for Anti Ping
function AntiPing()
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
end


local Kill = Window:AddTab("Kill")

Kill:AddSwitch("Auto Kill", false, function(state)
   AutoKillToggle = value
        if value then
            autoKillPlayers()
        end
end)

Kill:AddSwitch("Equip Punch", false, function(state)
   autoPunchEnabled = value
        if value then
            AutoPunch()
        end
end)
