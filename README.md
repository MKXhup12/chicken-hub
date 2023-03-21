local CurrentIndexQuest = 1
local QuestInfos = require(game:GetService("ReplicatedStorage").Modules.QuestsInfos).Info
getgenv().Level = 0 
function EquipWeapon(ToolSe)
        pcall(function()    
			if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
				local tool = game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe)
				game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
			end
		end)
end

task.spawn(function()
  pcall(function()
      game:GetService("RunService").Heartbeat:Connect(function()
          if _G.AutoFarm then
              if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
                  local Noclip = Instance.new("BodyVelocity")
                  Noclip.Name = "BodyClip"
                  Noclip.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
                  Noclip.MaxForce = Vector3.new(100000,100000,100000)
                  Noclip.Velocity = Vector3.new(0,0,0)
              end
          else
              if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
                  game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
              end
          end
      end)
  end)
end)
function getLevel() 
    local Level = 0;
    local x, p = pcall(function() 
           for i, v in pairs(game:GetService("Players").LocalPlayer.PlayerGui.Stats.Main.Frame.StatsContainer:GetChildren()) do
        	if v:IsA("TextLabel") and game:GetService("Players").LocalPlayer.Data.Attributes:GetAttribute(v.Name) then
        		if v.Name ~= "Haki" then
        			Level = Level + game:GetService("Players").LocalPlayer.Data.Attributes:GetAttribute(v.Name)/5
        		end;
        	end;
        end; 
        return math.floor(Level)
    end)
    if x then getgenv().Level = p; return p end 
    if not x then return getgenv().Level end 
end
function getLevelData()
        local Level = getLevel()
        local Mob = game:GetService("Workspace"):FindFirstChild("Mobs")
        print(Level)
        if Level == 1 or Level <= 14 then 
            return "Bandit (Level 1)"
        elseif Level == 15 or Level <= 29 then 
           return "Bandit Leader (Level 15)"
        elseif Level == 30 or Level <= 59 then 
            return "Clown Pirate (Level 30)"
        elseif Level == 60 or Level <= 74 then 
            if Mob:FindFirstChild("Clown Leader (Level 60)") then 
                return "Clown Leader (Level 60)"
            else 
                return "Clown Pirate (Level 30)"
            end
        elseif Level == 75 or Level <= 89 then 
            return "Caveman (Level 75)"
        elseif Level == 90 or Level <= 119 then 
            return "Monkey (Level 90)"
        elseif Level == 120 or Level <= 199 then 
            if Mob:FindFirstChild("Gorilla (Level 120)") then 
                return "Gorilla (Level 120)"
            else 
                return "Monkey (Level 90)"
            end
        elseif Level == 200 or Level <= 274 then 
            return "Snow Bandit (Level 200)"
        elseif Level == 275 or Level <= 349 then 
            return "Small Yeti (Level 275)"
        elseif Level == 350 or Level <= 449 then 
            if Mob:FindFirstChild("Yeti (Level 350)") then 
                return "Yeti (Level 350)"
            else 
                return "Small Yeti (Level 275)"
            end
        elseif Level == 450 or Level <= 599 then 
            return "Sor Bandit (Level 450)"
        elseif Level == 600 or Level <= 799 then 
            return "Pharaoh Guard (Level 600)"
        elseif Level == 800 or Level <= 999 then 
             if Mob:FindFirstChild("Anubis the Bone Keeper (Level 800)") then 
                return "Anubis the Bone Keeper (Level 800)"
            else 
                return "Pharaoh Guard (Level 600)"
            end
        elseif Level == 1000 or Level <= 1099 then 
            return "Sky Bandit (Level 1000)"
        elseif Level == 1100 or Level <= 1199 then 
            return "High-Level Sky Borit (Level 1100)"
        else 
            if Mob:FindFirstChild("Sky Leader (Level 1200)") then 
                return "Sky Leader (Level 1200)"
            else 
                return "High-Level Sky Borit (Level 1100)"
            end
        end
end
spawn(function() 
    while true do wait(.3)   
        local ReplicatedStorage = game:GetService("ReplicatedStorage");
        local weaponChange = ReplicatedStorage.Remotes.Mouse1Combat;
        local CombatFrameWorkHit = ReplicatedStorage.Remotes.M1sDamage;
        if __Attack then 
            pcall(function() 
                for i, v in pairs(game.Workspace.Mobs:GetChildren()) do
                    if v:FindFirstChild("HumanoidRootPart")  and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 350 and game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool") then
                        local Tool = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool")
                        weaponChange:FireServer(Tool.Name);
                        CombatFrameWorkHit:FireServer(Tool.Name, v);
                        for i2, v2 in pairs(game.Workspace.Mobs:GetChildren()) do 
                            if v2:FindFirstChild("HumanoidRootPart")  and (v2.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 350 and game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool") then
                                CombatFrameWorkHit:FireServer(Tool.Name, v2);
                            end
                        end
                    end;
                end;    
            end)    
        end
    end
end)
spawn(function() 
    while true do 
        if _G.AutoFarm then 
            local MobAttack = getLevelData()
            local Mob = game:GetService("Workspace"):FindFirstChild("Mobs")
            if Mob then 
                if Mob:FindFirstChild(MobAttack) then 
                    for i , v in pairs(Mob:GetChildren()) do 
                        if v.Name == MobAttack and v:FindFirstChild('Humanoid') and v.Humanoid.Health > 0 then 
                            local Quests = game.Players.LocalPlayer:WaitForChild("Data", 60):WaitForChild("Quests");
                            if Quests:GetAttribute("QuestName") == "None" then
                                game:GetService("ReplicatedStorage").Remotes.QuestRemote:FireServer("GetQuest", MobAttack)
                            end
                            if Quests:GetAttribute("QuestName") ~= MobAttack then 
                                game:GetService("ReplicatedStorage").Remotes.QuestRemote:FireServer("GetQuest", MobAttack)    
                            end
                            repeat task.wait() 
                                MobAttack = getLevelData()
                                __Attack = true 
                                spawn(function() 
                                     game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,15,5)   
                                end)
                                spawn(function() 
                                    EquipWeapon("Combat")    
                                end)
                                pcall(function() 
                                    __Attack = true 
                                    if not v:FindFirstChild("Pos") then 
                                        	local Part = Instance.new('Part')
                                    		Part.Parent = v
                                    		Part.CanCollide = false
                                    		Part.Anchored = true
                                    		Part.CFrame = v.HumanoidRootPart.CFrame
                                    		Part.Transparency = 1   
                                    end
                                    for i2, v2 in pairs(Mob:GetChildren()) do 
                                        if v2 ~= v and v2.Name == MobAttack then 
                                            if v2.Humanoid.Health == v2.Humanoid.MaxHealth then 
                                                repeat task.wait() 
                                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v2.HumanoidRootPart.CFrame * CFrame.new(0,15,5)   
                                                until (v2.Humanoid.Health == v2.Humanoid.MaxHealth) == false or not _G.AutoFarm
                                            end
                                            if (v2.Humanoid.Health == v2.Humanoid.MaxHealth) == false then 
                                                v2.Head.CanCollide = false
                                                v2.Humanoid.Sit = false
                                                v2.HumanoidRootPart.CanCollide = false
                                                v2.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame
                                                for i3 , v3 in pairs(v2:GetChildren()) do 
                                                    if v3:IsA("BasePart") and v3.CanCollide == true then
                                                        v3.CanCollide = false
                                                    end
                                                end   
                                            end
                                        end
                                    end
                                end)
                            until Quests:GetAttribute("QuestName") ~= MobAttack or not v.Parent or v.Humanoid.Health <= 0 or not _G.AutoFarm 
                            __Attack = false 
                        end
                    end
                else 
                    if Mob:FindFirstChild("Sky Leader (Level 1200)") and not Mob:FindFirstChild(MobAttack) then 
                       repeat wait()
                           pcall(function() 
                                 game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Mob:FindFirstChild("Sky Leader (Level 1200)").HumanoidRootPart.CFrame * CFrame.new(1,0,0)   
                           end)
                       until Mob:FindFirstChild(MobAttack) or not _G.AutoFarm
                    end
                    if Mob:FindFirstChild("High-Level Sky Bandit (Level 1100)") and not Mob:FindFirstChild(MobAttack) then 
                       repeat wait()
                           pcall(function() 
                                 game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Mob:FindFirstChild("High-Level Sky Bandit (Level 1100)").HumanoidRootPart.CFrame * CFrame.new(1,0,0)   
                           end)
                       until Mob:FindFirstChild(MobAttack) or not _G.AutoFarm
                    end
                end
            end    
        end
        wait()     
    end
end)



local DiscordLib = loadstring(game:HttpGet"https://raw.githubusercontent.com/kickTh/New-Ui/main/discord%20lib%20(1).txt")()

local win = DiscordLib:Window("MAMA HUB 1.0")

local serv = win:Server("Main", "")


local tgls = serv:Channel("Main")

tgls:Toggle("Auto Grind Level",false, function(bool)
_G.AutoFarm = bool
end)

