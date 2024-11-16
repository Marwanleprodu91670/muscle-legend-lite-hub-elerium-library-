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
local punchTool = nil  -- Variable to store the "Punch" tool
local targetPlayerName = ""  -- Variable to store the target player name

-- Function to handle teleportation of the entire body
spawn(function()
    while wait(0.1) do
        if AutoKillToggle then
            local player = game.Players.LocalPlayer
            local character = player.Character or player.CharacterAdded:Wait()

            local rightHand = character:FindFirstChild("RightHand")
            local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")

            if rightHand and humanoidRootPart then
                for _, target in pairs(game.Players:GetPlayers()) do
                    if target ~= player and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
                        -- Teleport the entire body by adjusting the HumanoidRootPart's CFrame
                        target.Character.HumanoidRootPart.CFrame = rightHand.CFrame
                    end
                end
            end
        end

        -- Check if Kill Target Toggle is enabled
        if KillTargetToggle and targetPlayerName ~= "" then
            local player = game.Players.LocalPlayer
            local targetPlayer = game.Players:FindFirstChild(targetPlayerName)

            if targetPlayer and targetPlayer.Character then
                local character = player.Character or player.CharacterAdded:Wait()
                local rightHand = character:FindFirstChild("RightHand")

                if rightHand then
                    local targetHumanoidRootPart = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
                    if targetHumanoidRootPart then
                        -- Teleport the target player's character to the right hand of the local player
                        targetPlayer.Character.HumanoidRootPart.CFrame = rightHand.CFrame
                    end
                end
            end
        end
    end
end)

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


-- Default values for the toggles
Kill:GetSwitch("Auto Kill"):Set(true)  -- Ensure the Auto Kill toggle starts in the "On" position
Kill:GetSwitch("Auto Punch"):Set(false)  -- Default state for Auto Punch is off
Kill:GetSwitch("Kill Target"):Set(false)  -- Default state for Kill Target is off
