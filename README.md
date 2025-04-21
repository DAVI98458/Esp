local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera

-- Cria ESP em cima da cabeça dos jogadores
local function createESP(player)
	if player == LocalPlayer then return end
	local character = player.Character
	if not character then return end

	local head = character:FindFirstChild("Head")
	if not head or head:FindFirstChild("ESP") then return end

	local esp = Instance.new("BillboardGui")
	esp.Name = "ESP"
	esp.Adornee = head
	esp.Size = UDim2.new(0, 100, 0, 20)
	esp.AlwaysOnTop = true
	esp.StudsOffset = Vector3.new(0, 2, 0)

	local label = Instance.new("TextLabel", esp)
	label.Size = UDim2.new(1, 0, 1, 0)
	label.BackgroundTransparency = 1
	label.Text = player.Name
	label.TextScaled = true
	label.Font = Enum.Font.SourceSans
	label.TextColor3 = (player.Team == LocalPlayer.Team) and Color3.fromRGB(0, 150, 255) or Color3.fromRGB(255, 0, 0)

	esp.Parent = head
end

-- Atualiza ESP constantemente
RunService.RenderStepped:Connect(function()
	for _, player in ipairs(Players:GetPlayers()) do
		if player.Character and player.Character:FindFirstChild("Head") then
			createESP(player)
		end
	end
end)
