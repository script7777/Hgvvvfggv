local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local StarterGui = game:GetService("StarterGui")

local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

local noclip = false

pcall(function()
	StarterGui:SetCore("SendNotification", {
		Title = "Noclip Pronto";
		Text = "Criado by NoXiter";
		Duration = 5;
	})
end)

local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
screenGui.Name = "NoclipGUI"

local button = Instance.new("TextButton", screenGui)
button.Size = UDim2.new(0, 120, 0, 50)
button.Position = UDim2.new(0.05, 0, 0.85, 0)
button.Text = "Ativar Noclip"
button.BackgroundColor3 = Color3.fromRGB(50, 150, 255)
button.TextScaled = true
button.TextColor3 = Color3.new(1, 1, 1)
button.Font = Enum.Font.SourceSansBold

button.MouseButton1Click:Connect(function()
	noclip = not noclip
	if noclip then
		button.Text = "Desativar Noclip"
		button.BackgroundColor3 = Color3.fromRGB(255, 100, 100)
	else
		button.Text = "Ativar Noclip"
		button.BackgroundColor3 = Color3.fromRGB(50, 150, 255)
	end
end)

RunService.Stepped:Connect(function()
	if noclip and player.Character then
		for _, part in pairs(player.Character:GetDescendants()) do
			if part:IsA("BasePart") then
				part.CanCollide = false
			end
		end
	end
end)

player.CharacterAdded:Connect(function(char)
	character = char
	character:WaitForChild("Humanoid")

	if not noclip then
		for _, part in pairs(character:GetDescendants()) do
			if part:IsA("BasePart") then
				part.CanCollide = true
			end
		end
	end
end)
