local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

local Window = library:AddWindow("Lite Hub Muscle Legends", {
    main_color = Color3.fromRGB(41, 74, 122),
    min_size = Vector2.new(450, 340),
    toggle_key = Enum.KeyCode.RightShift,
    can_resize = true,
})

local AutoKillToggle = false

local function makeInvisible(character)
    for _, part in pairs(character:GetDescendants()) do
        if part:IsA("BasePart") then
            part.Transparency = 1
            if part:FindFirstChild("Handle") then
                part.Handle.Transparency = 1
            end
        elseif part:IsA("Decal") then
            part.Transparency = 1
        end
    end
end

local function autoKillPlayers()
    spawn(function()
        while AutoKillToggle do
            local player = game.Players.LocalPlayer
            local character = player.Character or player.CharacterAdded:Wait()
            
            if character then
                local rightHand = character:FindFirstChild("RightHand") or character:FindFirstChild("Right Arm")
                if rightHand then
                    for _, target in pairs(game.Players:GetPlayers()) do
                        if target ~= player and target.Character then
                            local targetCharacter = target.Character
                            if targetCharacter:FindFirstChild("HumanoidRootPart") then
                                targetCharacter.HumanoidRootPart.CFrame = rightHand.CFrame
                                makeInvisible(targetCharacter)
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
