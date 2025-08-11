-- Coloque este LocalScript em StarterPlayerScripts

local function reduzirGraficos()
    -- Desativa sombras em todas as luzes
    for _, light in ipairs(workspace:GetDescendants()) do
        if light:IsA("PointLight") or light:IsA("SpotLight") or light:IsA("SurfaceLight") then
            light.Shadows = false
            light.Enabled = false
        end
    end

    -- Desativa efeitos visuais como partículas e explosões
    for _, obj in ipairs(workspace:GetDescendants()) do
        if obj:IsA("ParticleEmitter") or obj:IsA("Smoke") or obj:IsA("Fire") or obj:IsA("Explosion") then
            obj.Enabled = false
        end
    end

    -- Remove reflexos e materiais pesados
    for _, part in ipairs(workspace:GetDescendants()) do
        if part:IsA("BasePart") then
            part.Reflectance = 0
            part.Material = Enum.Material.Plastic
        end
    end

    -- Desativa efeitos de iluminação global
    local lighting = game:GetService("Lighting")
    lighting.GlobalShadows = false
    lighting.FogEnd = 1000000
    lighting.FogStart = 1000000
    lighting.Brightness = 1
    lighting.OutdoorAmbient = Color3.new(1, 1, 1)
    
    -- Remove efeitos de pós-processamento (se houver)
    for _, effect in ipairs(lighting:GetChildren()) do
        if effect:IsA("BlurEffect") or effect:IsA("SunRaysEffect") or effect:IsA("ColorCorrectionEffect") or effect:IsA("BloomEffect") or effect:IsA("DepthOfFieldEffect") then
            effect.Enabled = false
        end
    end
end

-- Executa ao carregar o jogo
reduzirGraficos()
