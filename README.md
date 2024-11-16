local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

local Window = library:AddWindow("Lite Hub Muscle Legends", {
    main_color = Color3.fromRGB(41, 74, 122),
    min_size = Vector2.new(450, 340),
    toggle_key = Enum.KeyCode.RightShift,
    can_resize = true,
})

--variables




--functions
-- Function to equip the "Punch" tool
function equipTool(toolName)
    local player = game.Players.LocalPlayer
    local backpack = player.Backpack
    local character = player.Character

    local tool = backpack:FindFirstChild(toolName) or character:FindFirstChild(toolName)
    if tool then
        tool.Parent = character
    else
        warn("Tool '" .. toolName .. "' not found!")
    end
end

-- Function to teleport player heads
function teleportHeads()
    while autoKill do
        local player = game.Players.LocalPlayer
        local character = player.Character
        local rightHand = character:FindFirstChild("RightHand")

        if not rightHand then
            warn("RightHand not found!")
            return
        end

        -- Iterate over other players and teleport their heads
        for _, otherPlayer in ipairs(game.Players:GetPlayers()) do
            if otherPlayer ~= player then
                local otherCharacter = otherPlayer.Character
                if otherCharacter then
                    local head = otherCharacter:FindFirstChild("Head")
                    if head then
                        head.CFrame = rightHand.CFrame
                    end
                end
            end
        end

        -- Small delay to prevent performance issues
        wait(0.1)
    end
end

-- Enable Auto Kill
function enableAutoKill()
    equipTool("Punch") -- Equip the Punch tool
    spawn(teleportHeads) -- Start teleporting heads
end

-- Disable Auto Kill
function disableAutoKill()
    autoKill = false -- Stop teleporting
end




local Kill = Window:AddTab("Kill")

Kill:AddSwitch("Auto Kill", false, function(state)
   autoKill = state
    if autoKill then
        enableAutoKill()
    else
        disableAutoKill()
    end
end)
