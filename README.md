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

-- Function to equip and use the "Punch" tool
local function autoPunch()
    while AutoPunchToggle do
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        
        -- Look for the "Punch" tool in the player's Backpack
        if not punchTool then
            punchTool = player.Backpack:FindFirstChild("Punch")
        end
        
        if punchTool then
            -- Equip the "Punch" tool if it is found
            if not character:FindFirstChild("Punch") then
                punchTool.Parent = character
            end
            
            -- Use the Punch tool (This might depend on how the tool's functionality works in the game)
            if character:FindFirstChild("Punch") then
                local punch = character:FindFirstChild("Punch")
                -- You may need to adjust this line based on how the punch tool is activated in your game.
                -- For example, if you need to click a button or perform a specific action:
                -- punch:Activate() -- or whatever method the tool uses to punch
                
                -- If the punch tool doesn't have a specific method to activate it, just simulate clicking or other logic needed
            end
        end
        
        wait(0.1) -- Adjust the frequency of the loop to your needs
    end
end

-- Kill Tab
local Kill = window:AddTab("Kill")

-- Add label "Target Player" under the Kill tab
Kill:AddLabel("Target Player")

-- Add switches (toggles)
Kill:AddSwitch("Auto Kill", function(value)
    AutoKillToggle = value  -- Update the AutoKill toggle state
end)

-- Add Kill Target toggle
Kill:AddSwitch("Kill Target", function(value)
    KillTargetToggle = value  -- Update the KillTarget toggle state
end)

-- Add textbox to input the target player's name
Kill:AddTextBox("Select Target", function(text)
    targetPlayerName = text  -- Update the target player name when the textbox is filled
end)

-- Punch Tab
local Punch = window:AddTab("Punch")

-- Add Auto Punch toggle
Punch:AddSwitch("Auto Punch", function(value)
    AutoPunchToggle = value  -- Update the AutoPunch toggle state
    if AutoPunchToggle then
        spawn(autoPunch)  -- Start the auto punch loop when the toggle is enabled
    end
end)

-- Default values for the toggles
Kill:GetSwitch("Auto Kill"):Set(true)  -- Ensure the Auto Kill toggle starts in the "On" position
Punch:GetSwitch("Auto Punch"):Set(false)  -- Default state for Auto Punch is off
