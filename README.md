local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Marwanleprodu91670/lib/refs/heads/main/README.md"))()

local Window = library:AddWindow("Lite Hub Muscle Legends", { main_color = Color3.fromRGB(41, 74, 122), min_size = Vector2.new(450, 340), toggle_key = Enum.KeyCode.RightShift, can_resize = true, })

--variables
local autoKillEnabled = false

--function
-- Loop to continuously check Auto Kill toggle
spawn(function()
	while AutoKillToggle do
		-- Get the player and character
		local player = game.Players.LocalPlayer
		local character = player.Character or player.CharacterAdded:Wait()

		-- Get the right hand of the character
		local rightHand = character:FindFirstChild("RightHand")

		-- Check if the right hand exists
		if rightHand then
			-- Loop through all players in the game
			for _, target in pairs(game.Players:GetPlayers()) do
				-- Check that the target is a valid player and is not the local player
				if target ~= player and target.Character and target.Character:FindFirstChild("Head") then
					-- Check for whitelist if enabled
					if not (whitelistEnabled and target.Name == selectedWhitelistPlayer) then
						-- Teleport the target's head to the right hand's position
						target.Character.Head.CFrame = rightHand.CFrame
					end
				end
			end
		end
		-- Wait a short time before repeating the loop
		wait(0.1) -- Delay for smoother execution
	end
end)
end

--tabs 
local Main = window:AddTab("Main") 
local AutoFarm = window:AddTab("AutoFarm") 
local Teleport = window:AddTab("Teleport") 
local Misc = window:AddTab("Misc")
local Misc = window:AddTab("Kill")

--toggles
Kill:AddSwitch("Auto Kill", function(bool)
	AutoKillToggle = value
	if value then
		autoKillPlayers()
	end
end)
switch:Set(true)

	
	
	
	
	
	
	
	
