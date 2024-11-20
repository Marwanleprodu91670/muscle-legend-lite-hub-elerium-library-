-- Load the library
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

-- Create the main UI window
local window = library:AddWindow("Elerium Test", {
	main_color = Color3.fromRGB(255, 255, 255), -- Color
	min_size = Vector2.new(450, 346), -- Size of the gui
	can_resize = false, -- true or false
})

-- Variables
local AutoKillToggle, AutoPunchToggle, KillTargetToggle = false, false, false
local AutoWeightToggle, AutoPushupsToggle, SitupsToggle, MuscleKingFarmToggle = false, false, false, false
local targetPlayerName = "" -- Stores the target player name

-- Helper Function: Equip and activate a tool
local function equipAndActivateTool(toolName)
    local player = game.Players.LocalPlayer
    if not player.Character or not player.Backpack then return end
    local tool = player.Backpack:FindFirstChild(toolName) or player.Character:FindFirstChild(toolName)
    if tool then
        player.Character.Humanoid:EquipTool(tool)
        tool:Activate()
    end
end

-- Function: Auto Weight
local function AutoWeight()
    spawn(function()
        while AutoWeightToggle do
            equipAndActivateTool("Weight")
            wait(0.1)
        end
    end)
end

-- Function: Auto Pushups
local function AutoPushups()
    spawn(function()
        while AutoPushupsToggle do
            equipAndActivateTool("Pushups")
            wait(0.1)
        end
    end)
end

-- Function: Auto Situps
local function AutoSitups()
    spawn(function()
        while SitupsToggle do
            equipAndActivateTool("Situps")
            wait(0.1)
        end
    end)
end

-- Function: Muscle King Farm
local function MuscleKingFarm()
    spawn(function()
        while MuscleKingFarmToggle do
            local player = game.Players.LocalPlayer
            if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                player.Character.HumanoidRootPart.CFrame = CFrame.new(-8546.25879, 23.045435, -5636.78418)
                equipAndActivateTool("Pushups")
            end
            wait(0.1)
        end
    end)
end

-- Function: Auto Punch
local function AutoPunch()
    spawn(function()
        while AutoPunchToggle do
            equipAndActivateTool("Punch")
            wait(0.1)
        end
    end)
end

-- Function: Auto Kill
local function AutoKill()
    spawn(function()
        while AutoKillToggle do
            local player = game.Players.LocalPlayer
            local rightHand = player.Character and player.Character:FindFirstChild("RightHand")
            if rightHand then
                for _, targetPlayer in ipairs(game.Players:GetPlayers()) do
                    if targetPlayer ~= player and targetPlayer.Character then
                        local targetHead = targetPlayer.Character:FindFirstChild("Head")
                        if targetHead then
                            targetHead.CFrame = rightHand.CFrame
                        end
                    end
                end
            end
            wait(0.1)
        end
    end)
end

-- Tabs and Features
local AutoFarm = window:AddTab("Auto Farm")
AutoFarm:AddSwitch("Auto Weight", function(value) AutoWeightToggle = value if value then AutoWeight() end end)
AutoFarm:AddSwitch("Auto Pushups", function(value) AutoPushupsToggle = value if value then AutoPushups() end end)
AutoFarm:AddSwitch("Auto Situps", function(value) SitupsToggle = value if value then AutoSitups() end end)
AutoFarm:AddSwitch("Muscle King Farm", function(value) MuscleKingFarmToggle = value if value then MuscleKingFarm() end end)

local Kill = window:AddTab("Kill")
Kill:AddSwitch("Auto Kill", function(value) AutoKillToggle = value if value then AutoKill() end end)
Kill:AddSwitch("Auto Punch", function(value) AutoPunchToggle = value if value then AutoPunch() end end)
Kill:AddLabel("Target Player")
Kill:AddSwitch("Kill Target", function(value) KillTargetToggle = value end)
Kill:AddTextBox("Select Target", function(text) targetPlayerName = text end)

-- Additional Tabs (Settings, Spy, and Teleport)
local settingsTab = window:AddTab("Settings")
settingsTab:AddButton("Anti Ping", function()
    local g = game
    g.Workspace.Terrain.WaterWaveSize = 0
    g.Workspace.Terrain.WaterWaveSpeed = 0
    g.Lighting.GlobalShadows = false
    g.Lighting.FogEnd = 1e9
    g.Lighting.Brightness = 0
    settings().Rendering.QualityLevel = Enum.QualityLevel.Level01
    for _, v in pairs(g:GetDescendants()) do
        if v:IsA("Part") then v.Material = Enum.Material.Plastic end
        if v:IsA("Decal") or v:IsA("Texture") then v.Transparency = 1 end
    end
end)

settingsTab:AddButton("Anti Kick", function()
    local vu = game:GetService("VirtualUser")
    game.Players.LocalPlayer.Idled:connect(function()
        vu:Button2Down(Vector2.new(), workspace.CurrentCamera.CFrame)
    end)
end)

-- Spy Tab
local spyTab = window:AddTab("Spy")
spyTab:AddSwitch("Spy Player", function(bool)
    local player = game.Players.LocalPlayer
    if bool and targetPlayerName ~= "" then
        local target = game.Players:FindFirstChild(targetPlayerName)
        if target and target.Character then
            game.Workspace.CurrentCamera.CameraSubject = target.Character.Humanoid
        end
    else
        game.Workspace.CurrentCamera.CameraSubject = player.Character.Humanoid
    end
end)
spyTab:AddTextBox("Write Player Username", function(text) targetPlayerName = text end)

-- Teleport Tab
local teleportTab = window:AddTab("Teleport")
teleportTab:AddLabel("Islands:")
local islandPositions = {
    ["Tiny Island"] = Vector3.new(-38.4037132, 9.66723633, 1832.29114),
    ["Frost Island"] = Vector3.new(-2533.64258, 13.7738762, -408.134796),
    ["Mythical Island"] = Vector3.new(2170.5437, 13.8738737, 1073.75525),
    ["Inferno Island"] = Vector3.new(-6678.75635, 13.8738737, -1285.4198),
    ["Legend Island"] = Vector3.new(4685.5625, 997.608765, -3910.30908),
    ["Muscle King Island"] = Vector3.new(-8546.25879, 23.045435, -5636.78418),
}
for name, pos in pairs(islandPositions) do
    teleportTab:AddButton(name, function()
        local player = game.Players.LocalPlayer
        if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(pos)
        end
    end)
end

-- Stats Tab
local Stats = window:AddTab("Stats")

-- Create the dropdown menu
local playerDropdown = Stats:AddDropdown("Select Player", function(selectedPlayerName)
    updatePlayerStats(selectedPlayerName)
end)

-- Create labels for displaying stats
local strengthLabel = Stats:AddLabel("Strength: 0")
local durabilityLabel = Stats:AddLabel("Durability: 0")
local agilityLabel = Stats:AddLabel("Agility: 0")
local pet1Label = Stats:AddLabel("Pet1: None")
local pet2Label = Stats:AddLabel("Pet2: None")
local pet3Label = Stats:AddLabel("Pet3: None")
local pet4Label = Stats:AddLabel("Pet4: None")

-- Function to update stats of the selected player
local function updatePlayerStats(playerName)
    local player = game.Players:FindFirstChild(playerName)
    if not player then
        strengthLabel:SetText("Strength: N/A")
        durabilityLabel:SetText("Durability: N/A")
        agilityLabel:SetText("Agility: N/A")
        pet1Label:SetText("Pet1: N/A")
        pet2Label:SetText("Pet2: N/A")
        pet3Label:SetText("Pet3: N/A")
        pet4Label:SetText("Pet4: N/A")
        return
    end

    local statsFolder = player:FindFirstChild("Stats")
    if statsFolder then
        local strength = statsFolder:FindFirstChild("Strength")
        strengthLabel:SetText("Strength: " .. (strength and strength.Value or "N/A"))

        local durability = statsFolder:FindFirstChild("Durability")
        durabilityLabel:SetText("Durability: " .. (durability and durability.Value or "N/A"))

        local agility = statsFolder:FindFirstChild("Agility")
        agilityLabel:SetText("Agility: " .. (agility and agility.Value or "N/A"))
    end

    pet1Label:SetText("Pet1: " .. (player:FindFirstChild("pet1") and player.pet1.Value or "None"))
    pet2Label:SetText("Pet2: " .. (player:FindFirstChild("pet2") and player.pet2.Value or "None"))
    pet3Label:SetText("Pet3: " .. (player:FindFirstChild("pet3") and player.pet3.Value or "None"))
    pet4Label:SetText("Pet4: " .. (player:FindFirstChild("pet4") and player.pet4.Value or "None"))
end

-- Function to refresh the dropdown with all players
local function refreshDropdown()
    playerDropdown:Clear() -- Clear existing options
    for _, player in ipairs(game.Players:GetPlayers()) do
        playerDropdown:Add(player.Name)
    end
end

-- Auto-refresh dropdown
spawn(function()
    while wait(1) do
        refreshDropdown()
    end
end)

-- Set initial player dropdown value
playerDropdown:SetValue(game.Players.LocalPlayer.Name)

-- Show the window
window:Show()
