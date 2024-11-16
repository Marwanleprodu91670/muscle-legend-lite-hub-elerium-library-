local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

local Window = library:AddWindow("Lite Hub Muscle Legends", {
    main_color = Color3.fromRGB(41, 74, 122),
    min_size = Vector2.new(450, 340),
    toggle_key = Enum.KeyCode.RightShift,
    can_resize = true,
})

local AutoKillToggle = false

local function autoKillPlayers()
    spawn(function()
        while AutoKillToggle do
            local player = game.Players.LocalPlayer
            local character = player.Character or player.CharacterAdded:Wait()
            
            if character then
                local rightHand = character:FindFirstChild("RightHand")
                if rightHand then
                    for _, target in pairs(game.Players:GetPlayers()) do
                        if target ~= player and target.Character and target.Character:FindFirstChild("Head") then
                            local targetHead = target.Character:FindFirstChild("Head")
                            if targetHead then
                                targetHead.CFrame = rightHand.CFrame
                            end
                        end
                    end
                end
            end
            
            wait(0.1)
        end
    end)
end

local Kill = Window:AddTab("Kill")

Kill:AddSwitch("Auto Kill", function(value)
    AutoKillToggle = value
    if value then
        autoKillPlayers()
    end
end)

