local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

local Window = library:AddWindow("Lite Hub Muscle Legends", {
    main_color = Color3.fromRGB(41, 74, 122),
    min_size = Vector2.new(450, 340),
    toggle_key = Enum.KeyCode.RightShift,
    can_resize = true,
})

local Kill = Window:AddTab("Kill")

Kill:AddSwitch("Auto Kill", false, function(state)
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()

    -- Locate the "Punch" tool
    local tool = character:FindFirstChild("Punch")  -- Specifically target the "Punch" tool

    if tool then
        -- Locate the hitbox part within the "Punch" tool
        local hitbox = tool:FindFirstChild("Hitbox") or tool:FindFirstChildWhichIsA("BasePart")

        if hitbox then
            if state then
                -- Enable hitbox expansion
                hitbox.Size = Vector3.new(100, 100, 100)  -- Enlarge hitbox
                hitbox.Transparency = 1  -- Make invisible for stealth
                hitbox.CanCollide = false  -- Disable collisions to avoid environmental interference
            else
                -- Reset hitbox to default size
                hitbox.Size = Vector3.new(2, 2, 2)  -- Default hitbox size (adjust if needed)
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

