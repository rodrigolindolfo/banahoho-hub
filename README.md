local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/Rayfield/main/source"))()

local Window = Library:CreateWindow({
   Name = "Hybrid Mobile | CDK & Soul Guitar",
   LoadingTitle = "Iniciando Sistema...",
   ConfigurationSaving = { Enabled = false }
})

local function addStats(statName)
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint", statName, 1)
end

local TabFarm = Window:CreateTab("Auto Farm", 4483362458)

TabFarm:CreateToggle({
   Name = "Auto Farm Level",
   CurrentValue = false,
   Callback = function(Value)
      _G.AutoFarm = Value
      spawn(function()
         while _G.AutoFarm do
            wait(0.1)
            pcall(function()
                if not game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", "BanditQuest1", 1)
                end
            end)
         end
      end)
   end,
})

local TabItems = Window:CreateTab("Itens Lendários", 4483362458)

TabItems:CreateButton({
   Name = "Obter Soul Guitar (Requer Materiais)",
   Callback = function()
      game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SoulGuitarQuest")
   end,
})

TabItems:CreateToggle({
   Name = "Auto CDK Quest (Tushita/Yama)",
   CurrentValue = false,
   Callback = function(Value)
      _G.CDKQuest = Value
      print("Iniciando Verificação de CDK...")
   end,
})

local TabStats = Window:CreateTab("Status", 4483362458)

TabStats:CreateToggle({
   Name = "Auto Melee",
   CurrentValue = false,
   Callback = function(Value)
      _G.AutoStatsMelee = Value
      spawn(function()
         while _G.AutoStatsMelee do
            wait(0.5)
            if _G.AutoStatsMelee then addStats("Melee") end
         end
      end)
   end,
})

TabStats:CreateToggle({
   Name = "Auto Defense",
   CurrentValue = false,
   Callback = function(Value)
      _G.AutoStatsDefense = Value
      spawn(function()
         while _G.AutoStatsDefense do
            wait(0.5)
            if _G.AutoStatsDefense then addStats("Defense") end
         end
      end)
   end,
})
