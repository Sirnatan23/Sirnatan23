-- **Aviso**: Use este script por sua conta e risco.
-- Este script é uma base e pode precisar ser ajustado dependendo da estrutura do jogo.

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

-- Configurações
local treinoRapido = true
local autoEvento = true
local intervaloMusculacao = 0.1 -- Intervalo entre cada ação de musculação

-- Função de musculação rápida
function iniciarMusculacao()
    while treinoRapido do
        -- Simula a musculação (ajuste a lógica com base no jogo)
        local tool = character:FindFirstChildOfClass("Tool")
        if tool and tool:FindFirstChild("Activate") then
            tool:Activate()
        end
        wait(intervaloMusculacao)
    end
end

-- Função de auto evento
function participarEvento()
    while autoEvento do
        for _, evento in pairs(game.Workspace:GetDescendants()) do
            if evento:IsA("Part") and evento.Name == "Evento" then
                character:MoveTo(evento.Position) -- Move o personagem até o evento
                wait(1)
            end
        end
        wait(5) -- Verifica eventos a cada 5 segundos
    end
end

-- Iniciando funcionalidades
if treinoRapido then
    spawn(iniciarMusculacao)
end

if autoEvento then
    spawn(participarEvento)
end
