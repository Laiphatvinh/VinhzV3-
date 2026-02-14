local correctKey = "VINH2026"

local gui = Instance.new("ScreenGui", game.Players.LocalPlayer.PlayerGui)

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0,300,0,180)
frame.Position = UDim2.new(0.5,-150,0.5,-90)
frame.BackgroundColor3 = Color3.fromRGB(35,35,35)

local box = Instance.new("TextBox", frame)
box.Size = UDim2.new(0.8,0,0,40)
box.Position = UDim2.new(0.1,0,0.3,0)
box.PlaceholderText = "Nhập key..."

local button = Instance.new("TextButton", frame)
button.Size = UDim2.new(0.8,0,0,40)
button.Position = UDim2.new(0.1,0,0.6,0)
button.Text = "Xác nhận"

button.MouseButton1Click:Connect(function()
    if box.Text == correctKey then
        print("Key đúng — mở menu")
        frame:Destroy()
        -- 
        
    else
        box.Text = ""
        box.PlaceholderText = "Sai key!"
    end
end)
repeat task.wait() until game:IsLoaded()
repeat task.wait() until game.Players.LocalPlayer

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")

local Player = Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")

local Gui = Instance.new("ScreenGui")
Gui.Name = "FPS_PING_SYSTEM"
Gui.ResetOnSpawn = false
Gui.Parent = PlayerGui

local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0,260,0,90)
Frame.BackgroundColor3 = Color3.fromRGB(20,20,20)
Frame.BackgroundTransparency = 0.15
Frame.BorderSizePixel = 0
Frame.Visible = false
Frame.Parent = Gui

Instance.new("UICorner", Frame).CornerRadius = UDim.new(0,18)
local Stroke = Instance.new("UIStroke", Frame)
Stroke.Thickness = 2

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1,0,0,32)
Title.BackgroundTransparency = 1
Title.Text = "Vinhz • KaitunVip"
Title.Font = Enum.Font.GothamBold
Title.TextScaled = true
Title.TextColor3 = Color3.new(1,1,1)
Title.Parent = Frame

local Info = Instance.new("TextLabel")
Info.Size = UDim2.new(1,0,0,45)
Info.Position = UDim2.new(0,0,0,35)
Info.BackgroundTransparency = 1
Info.Text = "Vinhz: -- | KaitunVip: --"
Info.Font = Enum.Font.Gotham
Info.TextScaled = true
Info.TextColor3 = Color3.new(1,1,1)
Info.Parent = Frame

task.wait()
local cam = workspace.CurrentCamera.ViewportSize
Frame.Position = UDim2.new(
	0,
	math.floor(cam.X * 0.5 - Frame.Size.X.Offset / 2),
	0,
	math.floor(cam.Y * 0.1)
)

local fps = 60

RunService.RenderStepped:Connect(function(dt)
	if dt > 0 then
		fps = math.floor(1 / dt)
	end
	local t = os.clock()
	local c = Color3.fromHSV((t % 5) / 5, 0.85, 1)
	Title.TextColor3 = c
	Stroke.Color = c
end)

local function getPing()
	return math.floor(Player:GetNetworkPing() * 1000)
end

task.spawn(function()
	while task.wait(0.5) do
		Info.Text = string.format("FPS: %d | Ping: %d ms", fps, getPing())
	end
end)

local dragging = false
local dragStart, startPos

Frame.InputBegan:Connect(function(input, gpe)
	if gpe then return end
	if input.UserInputType == Enum.UserInputType.MouseButton1
	or input.UserInputType == Enum.UserInputType.Touch then
		dragging = true
		dragStart = input.Position
		startPos = Frame.Position
	end
end)

Frame.InputEnded:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1
	or input.UserInputType == Enum.UserInputType.Touch then
		dragging = false
	end
end)

UserInputService.InputChanged:Connect(function(input, gpe)
	if not dragging or gpe then return end
	if input.UserInputType == Enum.UserInputType.MouseMovement
	or input.UserInputType == Enum.UserInputType.Touch then
		local delta = input.Position - dragStart
		local s = workspace.CurrentCamera.ViewportSize
		local x = math.clamp(startPos.X.Offset + delta.X, 0, s.X - Frame.AbsoluteSize.X)
		local y = math.clamp(startPos.Y.Offset + delta.Y, 0, s.Y - Frame.AbsoluteSize.Y)
		Frame.Position = UDim2.new(0,x,0,y)
	end
end)

local function StartupNotify()
	local N = Instance.new("Frame")
	N.Size = UDim2.new(0,320,0,90)
	N.Position = UDim2.new(1,40,0,40)
	N.BackgroundColor3 = Color3.fromRGB(18,18,18)
	N.BackgroundTransparency = 0.08
	N.BorderSizePixel = 0
	N.Parent = Gui

	Instance.new("UICorner", N).CornerRadius = UDim.new(0,18)
	local NS = Instance.new("UIStroke", N)
	NS.Thickness = 2

	local Icon = Instance.new("ImageLabel")
	Icon.Size = UDim2.new(0,52,0,52)
	Icon.Position = UDim2.new(0,14,0.5,-26)
	Icon.BackgroundTransparency = 1
	Icon.Image = "rbxassetid://123760972746517"
	Icon.Parent = N

	local T = Instance.new("TextLabel")
	T.Size = UDim2.new(1,-90,0,30)
	T.Position = UDim2.new(0,80,0,10)
	T.BackgroundTransparency = 1
	T.Text = "Aov Notify"
	T.Font = Enum.Font.GothamBold
	T.TextSize = 18
	T.TextXAlignment = Enum.TextXAlignment.Left
	T.TextColor3 = Color3.new(1,1,1)
	T.Parent = N

	local M = Instance.new("TextLabel")
	M.Size = UDim2.new(1,-90,0,38)
	M.Position = UDim2.new(0,80,0,42)
	M.BackgroundTransparency = 1
	M.TextWrapped = true
	M.TextXAlignment = Enum.TextXAlignment.Left
	M.TextYAlignment = Enum.TextYAlignment.Top
	M.Text = "Đang khởi động script kaitun Vinhz...."
	M.Font = Enum.Font.Gotham
	M.TextSize = 14
	M.TextColor3 = Color3.fromRGB(220,220,220)
	M.Parent = N

	TweenService:Create(N,TweenInfo.new(0.45,Enum.EasingStyle.Back,Enum.EasingDirection.Out),{
		Position = UDim2.new(1,-340,0,40)
	}):Play()

	task.spawn(function()
		while N.Parent do
			local c = Color3.fromHSV((os.clock() % 4) / 4, 0.9, 1)
			NS.Color = c
			T.TextColor3 = c
			task.wait(0.03)
		end
	end)

	task.delay(2.5,function()
		TweenService:Create(N,TweenInfo.new(0.4,Enum.EasingStyle.Quad),{
			Position = UDim2.new(1,40,0,40)
		}):Play()
		task.wait(0.4)
		N:Destroy()
		Frame.Visible = true
		print([[
========================================
  ✔ CAM ON DA SU DUNG CONFIG VINHZ
========================================
]])
		pcall(function()
			loadstring(game:HttpGet("https://raw.githubusercontent.com/obiiyeuem/vthangsitink/main/BananaCat-kaitunBF.lua"))()
		end)
	end)
end

StartupNotify()
