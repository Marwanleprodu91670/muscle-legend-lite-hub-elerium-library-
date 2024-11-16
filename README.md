local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

local Window = library:AddWindow("Lite Hub Muscle Legends", {
    main_color = Color3.fromRGB(41, 74, 122),
    min_size = Vector2.new(450, 340),
    toggle_key = Enum.KeyCode.RightShift,
    can_resize = true,
})

local Kill = Window:AddTab("Kill")

Kill:AddSwitch("Expand Punch Hitbox", false, function(state)
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()

    -- Locate the "Punch" tool
    local tool = character:FindFirstChild("Punch")

    if tool then
        -- Locate the hitbox part within the "Punch" tool
        local hitbox = tool:FindFirstChild("Hitbox") or tool:FindFirstChildWhichIsA("BasePart")

        if hitbox then
            if state then
                -- Expand the hitbox by a factor of 100000000
                local currentSize = hitbox.Size
                hitbox.Size = currentSize * 100000000  -- Multiply the current size by 100,000,000
                hitbox.Transparency = 1  -- Make the hitbox invisible for stealth
                hitbox.CanCollide = true  -- Disable collisions to avoid interference
            else
                -- Reset hitbox to default size (change to the actual default size of your tool)
                hitbox.Size = Vector3.new(2, 2, 2)  -- Default size (adjust if needed)
                hitbox.Transparency = 0  -- Restore visibility
                hitbox.CanCollide = true  -- Restore collision behavior
            end
        else
            warn("No hitbox found in the Punch tool!")
        end
    else
        warn("Punch tool not found in character!")
    end
end)


