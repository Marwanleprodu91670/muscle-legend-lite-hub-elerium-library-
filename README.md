local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

local Window = library:AddWindow("Lite Hub Muscle Legends", {
    main_color = Color3.fromRGB(41, 74, 122),
    min_size = Vector2.new(450, 340),
    toggle_key = Enum.KeyCode.RightShift,
    can_resize = true,
})

local Auto Farm = Window:AddTab("Auto Farm")

-- Toggle for Pushups
Auto Farm:AddSwitch("PushupsToggle", false, function(state)
    -- Continuously equip and use Pushups tool when toggle is on
    while state do
        local pushupsTool = game.Players.LocalPlayer.Backpack:FindFirstChild("Pushups")
        if pushupsTool then
            pushupsTool:Activate()  -- Assuming Activate is the correct method for using the tool
        end
        wait(0.1)  -- Short delay to prevent flooding
    end
end)

-- Toggle for Situps
Auto Farm:AddSwitch("SitupsToggle", false, function(state)
    -- Continuously equip and use Situps tool when toggle is on
    while state do
        local situpsTool = game.Players.LocalPlayer.Backpack:FindFirstChild("Situps")
        if situpsTool then
            situpsTool:Activate()  -- Assuming Activate is the correct method for using the tool
        end
        wait(0.1)  -- Short delay to prevent flooding
    end
end)

-- Toggle for Weight
Auto Farm:AddSwitch("WeightToggle", false, function(state)
    -- Continuously equip and use Weight tool when toggle is on
    while state do
        local weightTool = game.Players.LocalPlayer.Backpack:FindFirstChild("Weight")
        if weightTool then
            weightTool:Activate()  -- Assuming Activate is the correct method for using the tool
        end
        wait(0.1)  -- Short delay to prevent flooding
    end
end)

-- Toggle for Handstands
Auto Farm:AddSwitch("HandstandsToggle", false, function(state)
    -- Continuously equip and use Handstands tool when toggle is on
    while state do
        local handstandsTool = game.Players.LocalPlayer.Backpack:FindFirstChild("Handstands")
        if handstandsTool then
            handstandsTool:Activate()  -- Assuming Activate is the correct method for using the tool
        end
        wait(0.1)  -- Short delay to prevent flooding
    end
end)
