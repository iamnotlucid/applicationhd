print("Script started.")

local gid = 32462646 
local rgate = game.Workspace.Castle.CastleDoors:WaitForChild("RightCastleDoor")
local lgate = game.Workspace.Castle.CastleDoors:WaitForChild("LeftCastleDoor")
local ts = game:GetService("TweenService")
local keyword = "open"

function typewrite(object, text)
	for i = 1, #text, 1 do
		object.Text = string.sub(text, 1, i)
		task.wait(0.05)
	end
end

game:GetService("Players").PlayerAdded:Connect(function(player)
	print(player.Name .. " has joined the game.")
    game.ReplicatedStorage.AdmitterEvent:FireServer(player)

	local guideGui = player.PlayerGui:WaitForChild("Guide", 10)
	if guideGui then
		guideGui.Enabled = true
		typewrite(guideGui.Frame.Speech, "Follow the path, " .. player.Name .. ".")
		task.wait(7)
		guideGui.Enabled = false
	else
		warn("Guide GUI not found for player: " .. player.Name)
	end

	local tweeninfo = TweenInfo.new(
		8,
		Enum.EasingStyle.Quad,
		Enum.EasingDirection.InOut,
		0,
		false,
		0
	)

	local rproperties = {
		Position = Vector3.new(467.619, 136.074, -57.363)
	}
	local lproperties = {
		Position = Vector3.new(466.708, 136.074, -20.911)
	}

	local function OpenGates()
		local rtween = ts:Create(rgate, tweeninfo, rproperties)
		local ltween = ts:Create(lgate, tweeninfo, lproperties)
		rtween:Play()
		ltween:Play()
	end

	local function Checker(plr)
		if plr:IsInGroup(gid) then
			print(plr.Name .. " is part of the group.")
			guideGui.Enabled = true
			typewrite(guideGui.Frame.Speech, "Pass.")
			task.wait(3)
			guideGui.Enabled = false
			OpenGates()
		else
			plr:Kick("Trespasser.")
		end
	end


	game.ReplicatedStorage.AdmitterEvent.OnClientEvent:Connect(function(player)
		print("Recieved.")
		Checker(player)
	end)
	
	end)
