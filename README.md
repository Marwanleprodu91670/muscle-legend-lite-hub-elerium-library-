local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

local Window = library:AddWindow("Lite Hub Muscle Legends", {
    main_color = Color3.fromRGB(41, 74, 122),
    min_size = Vector2.new(450, 340),
    toggle_key = Enum.KeyCode.RightShift,
    can_resize = true,
})

--variables




--functions
function teleportHeads()
    while teleportToggle do
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

-- Enable teleporting heads
function enableTeleport()
    spawn(teleportHeads) -- Start teleporting heads
end

-- Disable teleporting heads
function disableTeleport()
    teleportToggle = false -- Stop teleporting
end

--equip Punch tool function fr fr Idk what to say lmfao
function equipTool(toolName)
    local player = game.Players.LocalPlayer
    local backpack = player.Backpack
    local character = player.Character

    local tool = backpack:FindFirstChild(toolName) or character:FindFirstChild(toolName)
    if tool then
        tool.Parent = character -- Equip the tool by moving it to the character
    else
        warn("Tool '" .. toolName .. "' not found!")
    end
end

-- Equip loop
local equipLoop
function enableEquipLoop()
    equipLoop = true
    spawn(function()
        while equipLoop do
            equipTool("Punch") -- Equip the "Punch" tool
            wait(0.1) -- Prevent rapid spamming
        end
    end)
end

-- Disable the equip loop
function disableEquipLoop()
    equipLoop = false
end



local Kill = Window:AddTab("Kill")

Kill:AddSwitch("Auto Kill", false, function(state)
   teleportToggle = state
    if teleportToggle then
        enableTeleport()
    else
        disableTeleport()
    end
end)

Kill:AddSwitch("Equip Punch", false, function(state)
   equipToggle = state
    if equipToggle then
        enableEquipLoop()
    else
        disableEquipLoop()
    end
end)
