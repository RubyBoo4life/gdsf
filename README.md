-- Gui to Lua
-- Version: 3.2

-- Instances:

local RubyExploit = Instance.new("ScreenGui")
local Main = Instance.new("Frame")
local TextLabel = Instance.new("TextLabel")
local ScrollingFrame = Instance.new("ScrollingFrame")
local Fly = Instance.new("TextButton")
local Health = Instance.new("TextButton")
local InfiniteHealth = Instance.new("TextButton")
local JumpPower = Instance.new("TextButton")
local KillAll = Instance.new("TextButton")
local NoClip = Instance.new("TextButton")
local Reset = Instance.new("TextButton")
local WalkSpeed = Instance.new("TextButton")
local TextLabel_2 = Instance.new("TextLabel")
local TextLabel_3 = Instance.new("TextLabel")
local Raq = Instance.new("Frame")
local TextLabel_4 = Instance.new("TextLabel")
local User = Instance.new("TextBox")
local Pass = Instance.new("TextBox")
local TextButton = Instance.new("TextButton")

--Properties:

RubyExploit.Name = "RubyExploit"
RubyExploit.Parent = game.CoreGui

Main.Name = "Main"
Main.Parent = RubyExploit
Main.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
Main.Position = UDim2.new(0.746968448, 0, 0.332220376, 0)
Main.Size = UDim2.new(0, 298, 0, 386)
Main.Visible = false
Main.Active = true
Main.Draggable = true

TextLabel.Parent = Main
TextLabel.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
TextLabel.Size = UDim2.new(0, 298, 0, 30)
TextLabel.Font = Enum.Font.Sarpanch
TextLabel.Text = "Ruby's Exploit | By RubyBoo4life"
TextLabel.TextColor3 = Color3.fromRGB(255, 170, 0)
TextLabel.TextScaled = true
TextLabel.TextSize = 14.000
TextLabel.TextWrapped = true

ScrollingFrame.Parent = Main
ScrollingFrame.Active = true
ScrollingFrame.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
ScrollingFrame.Position = UDim2.new(0.0167785231, 0, 0.183937818, 0)
ScrollingFrame.Size = UDim2.new(0, 287, 0, 283)

Fly.Name = "Fly"
Fly.Parent = ScrollingFrame
Fly.BackgroundColor3 = Color3.fromRGB(148, 148, 148)
Fly.Position = UDim2.new(0.470383257, 0, 0.0929575861, 0)
Fly.Size = UDim2.new(0, 140, 0, 50)
Fly.Font = Enum.Font.Sarpanch
Fly.Text = "Fly"
Fly.TextColor3 = Color3.fromRGB(255, 170, 0)
Fly.TextScaled = true
Fly.TextSize = 14.000
Fly.TextWrapped = true
Fly.MouseButton1Down:connect(function()
	repeat wait()
	until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:findFirstChild("Torso") and game.Players.LocalPlayer.Character:findFirstChild("Humanoid")
	local mouse = game.Players.LocalPlayer:GetMouse()
	repeat wait() until mouse
	local plr = game.Players.LocalPlayer
	local torso = plr.Character.Torso
	local flying = true
	local deb = true
	local ctrl = {f = 0, b = 0, l = 0, r = 0}
	local lastctrl = {f = 0, b = 0, l = 0, r = 0}
	local maxspeed = 50
	local speed = 0

	function Fly()
		local bg = Instance.new("BodyGyro", torso)
		bg.P = 9e4
		bg.maxTorque = Vector3.new(9e9, 9e9, 9e9)
		bg.cframe = torso.CFrame
		local bv = Instance.new("BodyVelocity", torso)
		bv.velocity = Vector3.new(0,0.1,0)
		bv.maxForce = Vector3.new(9e9, 9e9, 9e9)
		repeat wait()
			plr.Character.Humanoid.PlatformStand = true
			if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then
				speed = speed+.5+(speed/maxspeed)
				if speed > maxspeed then
					speed = maxspeed
				end
			elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then
				speed = speed-1
				if speed < 0 then
					speed = 0
				end
			end
			if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then
				bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed
				lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r}
			elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then
				bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed
			else
				bv.velocity = Vector3.new(0,0.1,0)
			end
			bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0)
		until not flying
		ctrl = {f = 0, b = 0, l = 0, r = 0}
		lastctrl = {f = 0, b = 0, l = 0, r = 0}
		speed = 0
		bg:Destroy()
		bv:Destroy()
		plr.Character.Humanoid.PlatformStand = false
	end
	mouse.KeyDown:connect(function(key)
		if key:lower() == "e" then
			if flying then flying = false
			else
				flying = true
				Fly()
			end
		elseif key:lower() == "w" then
			ctrl.f = 1
		elseif key:lower() == "s" then
			ctrl.b = -1
		elseif key:lower() == "a" then
			ctrl.l = -1
		elseif key:lower() == "d" then
			ctrl.r = 1
		end
	end)
	mouse.KeyUp:connect(function(key)
		if key:lower() == "w" then
			ctrl.f = 0
		elseif key:lower() == "s" then
			ctrl.b = 0
		elseif key:lower() == "a" then
			ctrl.l = 0
		elseif key:lower() == "d" then
			ctrl.r = 0
		end
	end)
	Fly()

end)

Health.Name = "Health"
Health.Parent = ScrollingFrame
Health.BackgroundColor3 = Color3.fromRGB(148, 148, 148)
Health.Position = UDim2.new(0.470383257, 0, 0.249926746, 0)
Health.Size = UDim2.new(0, 140, 0, 50)
Health.Font = Enum.Font.Sarpanch
Health.Text = "2x Health"
Health.TextColor3 = Color3.fromRGB(255, 170, 0)
Health.TextScaled = true
Health.TextSize = 14.000
Health.TextWrapped = true
Fly.MouseButton1Down:connect(function()
	script.Parent.MouseButton1Click:Connect(function()
		game.Players.LocalPlayer.Character.Humanoid.Health = 200
	end)
end)

InfiniteHealth.Name = "InfiniteHealth"
InfiniteHealth.Parent = ScrollingFrame
InfiniteHealth.BackgroundColor3 = Color3.fromRGB(148, 148, 148)
InfiniteHealth.Position = UDim2.new(-0.0174216032, 0, 0.249926746, 0)
InfiniteHealth.Size = UDim2.new(0, 140, 0, 50)
InfiniteHealth.Font = Enum.Font.Sarpanch
InfiniteHealth.Text = "Infinite Health"
InfiniteHealth.TextColor3 = Color3.fromRGB(255, 170, 0)
InfiniteHealth.TextScaled = true
InfiniteHealth.TextSize = 14.000
InfiniteHealth.TextWrapped = true
InfiniteHealth.MouseButton1Down:connect(function()
	script.Parent.MouseButton1Click:Connect(function()
		game.Players.LocalPlayer.Character.Humanoid.Health = 999999999
	end)
end)

JumpPower.Name = "JumpPower"
JumpPower.Parent = ScrollingFrame
JumpPower.BackgroundColor3 = Color3.fromRGB(148, 148, 148)
JumpPower.Position = UDim2.new(0.470383257, 0, 0.165789381, 0)
JumpPower.Size = UDim2.new(0, 140, 0, 50)
JumpPower.Font = Enum.Font.Sarpanch
JumpPower.Text = "2x Jump Power"
JumpPower.TextColor3 = Color3.fromRGB(255, 170, 0)
JumpPower.TextScaled = true
JumpPower.TextSize = 14.000
JumpPower.TextWrapped = true
JumpPower.MouseButton1Down:connect(function()
	script.Parent.MouseButton1Click:Connect(function()
		game.Players.LocalPlayer.Character.Humanoid.JumpPower = 100
	end)
end)

KillAll.Name = "KillAll"
KillAll.Parent = ScrollingFrame
KillAll.BackgroundColor3 = Color3.fromRGB(148, 148, 148)
KillAll.Position = UDim2.new(0, 0, 0.513063192, 0)
KillAll.Size = UDim2.new(0, 287, 0, 50)
KillAll.Font = Enum.Font.Sarpanch
KillAll.Text = "Kill All"
KillAll.TextColor3 = Color3.fromRGB(255, 170, 0)
KillAll.TextScaled = true
KillAll.TextSize = 14.000
KillAll.TextWrapped = true
KillAll.MouseButton1Down:connect(function()
	script.Parent.MouseButton1Click:Connect(function()
		--game.Players.LocalPlayer.Character.Humanoid.Health = 0
		Players = game:GetService("Players")
		for i, player in pairs(Players:GetPlayers()) do
			player.Character.Humanoid.Health = 0
		end
	end)
end)

NoClip.Name = "NoClip"
NoClip.Parent = ScrollingFrame
NoClip.BackgroundColor3 = Color3.fromRGB(148, 148, 148)
NoClip.Position = UDim2.new(-0.0174216032, 0, 0.0929575861, 0)
NoClip.Size = UDim2.new(0, 140, 0, 50)
NoClip.Font = Enum.Font.Sarpanch
NoClip.Text = "NoClip"
NoClip.TextColor3 = Color3.fromRGB(255, 170, 0)
NoClip.TextScaled = true
NoClip.TextSize = 14.000
NoClip.TextWrapped = true
NoClip.MouseButton1Down:connect(function()
	-- Sub Please
	local s = loadstring(game:HttpGet(("https://raw.githubusercontent.com/RobloxScripts52/noclip/main/noclip.lua"), true))()
	print(s)
end)

Reset.Name = "Reset"
Reset.Parent = ScrollingFrame
Reset.BackgroundColor3 = Color3.fromRGB(148, 148, 148)
Reset.Position = UDim2.new(-0.0174216032, 0, 0.430697173, 0)
Reset.Size = UDim2.new(0, 287, 0, 50)
Reset.Font = Enum.Font.Sarpanch
Reset.Text = "Reset"
Reset.TextColor3 = Color3.fromRGB(255, 170, 0)
Reset.TextScaled = true
Reset.TextSize = 14.000
Reset.TextWrapped = true
Reset.MouseButton1Down:connect(function()
	script.Parent.MouseButton1Click:Connect(function()
		game.Players.LocalPlayer.Character.Humanoid.Health = 0
	end)
end)

WalkSpeed.Name = "WalkSpeed"
WalkSpeed.Parent = ScrollingFrame
WalkSpeed.BackgroundColor3 = Color3.fromRGB(148, 148, 148)
WalkSpeed.Position = UDim2.new(-0.0174216032, 0, 0.165789366, 0)
WalkSpeed.Size = UDim2.new(0, 140, 0, 50)
WalkSpeed.Font = Enum.Font.Sarpanch
WalkSpeed.Text = "2x Walk Speed"
WalkSpeed.TextColor3 = Color3.fromRGB(255, 170, 0)
WalkSpeed.TextScaled = true
WalkSpeed.TextSize = 14.000
WalkSpeed.TextWrapped = true
WalkSpeed.MouseButton1Down:connect(function()
	script.Parent.MouseButton1Click:Connect(function()
		game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 32
	end)
end)

TextLabel_2.Parent = ScrollingFrame
TextLabel_2.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
TextLabel_2.Position = UDim2.new(0, 0, 0.34455958, 0)
TextLabel_2.Size = UDim2.new(0, 287, 0, 50)
TextLabel_2.Font = Enum.Font.Sarpanch
TextLabel_2.Text = "Kill"
TextLabel_2.TextColor3 = Color3.fromRGB(255, 170, 0)
TextLabel_2.TextScaled = true
TextLabel_2.TextSize = 14.000
TextLabel_2.TextWrapped = true

TextLabel_3.Parent = ScrollingFrame
TextLabel_3.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
TextLabel_3.Size = UDim2.new(0, 287, 0, 50)
TextLabel_3.Font = Enum.Font.Sarpanch
TextLabel_3.Text = "Character"
TextLabel_3.TextColor3 = Color3.fromRGB(255, 170, 0)
TextLabel_3.TextScaled = true
TextLabel_3.TextSize = 14.000
TextLabel_3.TextWrapped = true

Raq.Name = "Raq"
Raq.Parent = RubyExploit
Raq.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
Raq.Position = UDim2.new(0.746337712, 0, 0.331288338, 0)
Raq.Size = UDim2.new(0, 298, 0, 386)
Raq.Active = true
Raq.Draggable = true

TextLabel_4.Parent = Raq
TextLabel_4.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
TextLabel_4.BackgroundTransparency = 1.000
TextLabel_4.Size = UDim2.new(0, 298, 0, 50)
TextLabel_4.Font = Enum.Font.Sarpanch
TextLabel_4.Text = "Ruby's Exploit"
TextLabel_4.TextColor3 = Color3.fromRGB(255, 170, 0)
TextLabel_4.TextScaled = true
TextLabel_4.TextSize = 14.000
TextLabel_4.TextWrapped = true

User.Name = "User"
User.Parent = Raq
User.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
User.BorderColor3 = Color3.fromRGB(255, 170, 0)
User.BorderSizePixel = 2
User.Position = UDim2.new(0.147651002, 0, 0.183937818, 0)
User.Size = UDim2.new(0, 200, 0, 50)
User.Font = Enum.Font.Sarpanch
User.Text = "Username"
User.TextColor3 = Color3.fromRGB(255, 170, 0)
User.TextScaled = true
User.TextSize = 14.000
User.TextWrapped = true

Pass.Name = "Pass"
Pass.Parent = Raq
Pass.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Pass.BorderColor3 = Color3.fromRGB(255, 170, 0)
Pass.BorderSizePixel = 2
Pass.Position = UDim2.new(0.147651002, 0, 0.352331579, 0)
Pass.Size = UDim2.new(0, 200, 0, 50)
Pass.Font = Enum.Font.Sarpanch
Pass.Text = "Password"
Pass.TextColor3 = Color3.fromRGB(255, 170, 0)
Pass.TextScaled = true
Pass.TextSize = 14.000
Pass.TextWrapped = true

TextButton.Parent = Raq
TextButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
TextButton.BorderSizePixel = 2
TextButton.Position = UDim2.new(0, 44, 0, 214)
TextButton.Size = UDim2.new(0, 200, 0, 50)
TextButton.Font = Enum.Font.SourceSans
TextButton.Text = "Log In"
TextButton.TextColor3 = Color3.fromRGB(0, 0, 0)
TextButton.TextScaled = true
TextButton.TextSize = 14.000
TextButton.TextWrapped = true
TextButton.MouseButton1Down:connect(function()
if User.Text == "RubyBoo" and Pass.Text == "acmv" then
		Raq.Visible = false
		wait(0.5)
		Main.Visible = true
	end
end)

-- Scripts:

local function GDJYO_fake_script() -- Main.LocalScript 
	local script = Instance.new('LocalScript', Main)

	local Plr = game.Players.LocalPlayer
	
	Plr:GetMouse().KeyDown:Connect(function(K)
		if K == "k" then
			script.Parent.Visible = true
		end
	end)
	
	local Plr = game.Players.LocalPlayer
	
	Plr:GetMouse().KeyDown:Connect(function(L)
		if L == "l" then
			script.Parent.Visible = false
		end
	end)
end
coroutine.wrap(GDJYO_fake_script)()
local function WINULFJ_fake_script() -- Health.LocalScript 
	local script = Instance.new('LocalScript', Health)

	script.Parent.MouseButton1Click:Connect(function()
	game.Players.LocalPlayer.Character.Humanoid.Health = 200
	end)
end
coroutine.wrap(WINULFJ_fake_script)()
local function OFSBCG_fake_script() -- InfiniteHealth.LocalScript 
	local script = Instance.new('LocalScript', InfiniteHealth)

	script.Parent.MouseButton1Click:Connect(function()
	game.Players.LocalPlayer.Character.Humanoid.Health = 99999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999
	end)
end
coroutine.wrap(OFSBCG_fake_script)()
local function OLDGH_fake_script() -- JumpPower.LocalScript 
	local script = Instance.new('LocalScript', JumpPower)

	script.Parent.MouseButton1Click:Connect(function()
	game.Players.LocalPlayer.Character.Humanoid.JumpPower = 100
	end)
end
coroutine.wrap(OLDGH_fake_script)()
local function SJVYWNN_fake_script() -- KillAll.Script 
	local script = Instance.new('Script', KillAll)

	script.Parent.MouseButton1Click:Connect(function()
		--game.Players.LocalPlayer.Character.Humanoid.Health = 0
		Players = game:GetService("Players")
		for i, player in pairs(Players:GetPlayers()) do
			player.Character.Humanoid.Health = 0
		end
	end)
end
coroutine.wrap(SJVYWNN_fake_script)()
local function TNGD_fake_script() -- NoClip.LocalScript 
	local script = Instance.new('LocalScript', NoClip)

	local tool = game.StarterGui.RubyExploit.Main.Frame1.NoClip.Noclip
	local player = game.Players.LocalPlayer
	
	script.Parent.MouseButton1Click:Connect(function()
		tool:Clone()
		tool:Clone().Parent = player.Backpack
	end)
	
end
coroutine.wrap(TNGD_fake_script)()
local function MXEB_fake_script() -- Reset.LocalScript 
	local script = Instance.new('LocalScript', Reset)

	script.Parent.MouseButton1Click:Connect(function()
		game.Players.LocalPlayer.Character.Humanoid.Health = 0
	end)
end
coroutine.wrap(MXEB_fake_script)()
local function OSAXOHE_fake_script() -- WalkSpeed.LocalScript 
	local script = Instance.new('LocalScript', WalkSpeed)

	script.Parent.MouseButton1Click:Connect(function()
	game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 32
	end)
end
coroutine.wrap(OSAXOHE_fake_script)()
