-- Otimizador de Gráficos com Notificação
local Players = game:GetService("Players")
local Lighting = game:GetService("Lighting")
local StarterGui = game:GetService("StarterGui")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer

-- Função de otimização
local function optimizeGraphics()
	-- Reduz qualidade visual
	Lighting.GlobalShadows = false
	Lighting.Brightness = 1
	Lighting.FogEnd = 100
	Lighting.FogStart = 0
	Lighting.ClockTime = 12
	Lighting.OutdoorAmbient = Color3.fromRGB(127, 127, 127)

	-- Desativa partículas e trilhas
	for _, descendant in pairs(workspace:GetDescendants()) do
		if descendant:IsA("ParticleEmitter") or descendant:IsA("Trail") then
			descendant.Enabled = false
		end
	end

	-- Desativa efeitos de pós-processamento
	for _, effect in pairs(Lighting:GetChildren()) do
		if effect:IsA("PostEffect") then
			effect.Enabled = false
		end
	end

	-- Mensagem de confirmação
	StarterGui:SetCore("SendNotification", {
		Title = "Otimização Concluída!";
		Text = "Desempenho melhorado com sucesso.";
		Duration = 4;
	})
end

-- Aguarda carregamento completo e executa
if RunService:IsRunning() then
	task.wait(2) -- pequena espera para garantir carregamento
	optimizeGraphics()
end
