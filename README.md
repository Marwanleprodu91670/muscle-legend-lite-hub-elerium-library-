-- Chargement de la bibliothèque
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/main/library.lua"))() -- Assure-toi que cette URL pointe vers un fichier Lua valide.

-- Création de la fenêtre principale
local Window = library:AddWindow("Lite Hub Muscle Legends", {
    main_color = Color3.fromRGB(41, 74, 122),
    min_size = Vector2.new(450, 340),
    toggle_key = Enum.KeyCode.RightShift,
    can_resize = true,
})

-- Variables globales
local AutoKillToggle = false
local whitelistEnabled = false
local selectedWhitelistPlayer = nil

-- Fonction d'auto-kill
local function autoKillPlayers()
    spawn(function()
        while AutoKillToggle do
            local player = game.Players.LocalPlayer
            local character = player.Character or player.CharacterAdded:Wait()

            -- Vérifie si le joueur possède une "RightHand"
            local rightHand = character:FindFirstChild("RightHand")
            if rightHand then
                for _, target in pairs(game.Players:GetPlayers()) do
                    -- Ignore le joueur local et cible uniquement les joueurs valides
                    if target ~= player and target.Character and target.Character:FindFirstChild("Head") then
                        if not (whitelistEnabled and target.Name == selectedWhitelistPlayer) then
                            -- Déplace la tête de la cible au niveau de la main droite
                            target.Character.Head.CFrame = rightHand.CFrame
                        end
                    end
                end
            end
            wait(0.1) -- Petite pause pour éviter une surcharge inutile
        end
    end)
end

-- Création de l'onglet "Kill"
local Kill = Window:AddTab("Kill")

-- Ajout du switch pour activer/désactiver l'auto-kill
Kill:AddSwitch("Auto Kill", function(value)
    AutoKillToggle = value
    if value then
        autoKillPlayers()
    end
end)

-- Ajout du toggle Auto Kill
Kill:AddSwitch("Auto Kill", function(value)
    AutoKillToggle = value
    if value then
        autoKillPlayers()
    end
end)
