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
local punchTool = nil  -- Variable to store the "Punch" tool

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
                        if not (whitelistEnabled and target.Name == selectedWhitelistPlayer) then
                            -- Teleport the entire body by adjusting the HumanoidRootPart's CFrame
                            target.Character.HumanoidRootPart.CFrame = rightHand.CFrame
                        end
                    end
                end
            end
        end
    end
end)

-- Function to handle auto punching (equip and use the "Punch" tool infinitely)
spawn(function()
    while wait(0.1) do
        if AutoPunchToggle then
            local player = game.Players.LocalPlayer
            local character = player.Character or player.CharacterAdded:Wait()

            -- Find the "Punch" tool in the player's Backpack
            punchTool = player.Backpack:FindFirstChild("Punch")

            if punchTool and character:FindFirstChild("Humanoid") then
                -- Equip the "Punch" tool if it's not already equipped
                if not character.Humanoid:FindFirstChildOfClass("Tool") then
                    punchTool.Parent = character
                end

                -- Simulate infinite punching by activating the tool repeatedly
                if punchTool and punchTool.Parent == character then
                    -- Check if the tool has an "Activated" event (usually used for activation)
                    if punchTool:FindFirstChild("Activated") then
                        punchTool.Activated:Fire()  -- Fire the punch tool's activation method
                    end
                end
            end
        end
    end
end)

-- Kill Tab
local Kill = window:AddTab("Kill")

-- Add switches (toggles)
Kill:AddSwitch("Auto Kill", function(value)
    AutoKillToggle = value  -- Update the AutoKill toggle state
end)

Kill:AddSwitch("Auto Punch", function(value)
    AutoPunchToggle = value  -- Update the AutoPunch toggle state
    if AutoPunchToggle then
        -- If AutoPunch is turned on, ensure that the punch tool is equipped and used
    else
        -- If AutoPunch is turned off, stop using the punch tool (remove it)
        if punchTool then
            punchTool.Parent = game.Players.LocalPlayer.Backpack  -- Move it back to the backpack if disabled
        end
    end
end)

-- Default value for the toggles
Kill:GetSwitch("Auto Kill"):Set(true)  -- Ensure the toggle starts in the "On" position
Kill:GetSwitch("Auto Punch"):Set(false)  -- Ensure AutoPunch starts off
