repeat wait(1) until game:IsLoaded()
if game.PlaceId == 2866967438 or game.PlaceId == 13378270416 or game.PlaceId == 7773766301 then
 function hopserver()local v0=game.PlaceId;local v1={};local v2="";local v3=os.date("!*t").hour;local v4=false;local v5=pcall(function()v1=game:GetService("HttpService"):JSONDecode(readfile("NotSameServers.json"));end);if  not v5 then table.insert(v1,v3);writefile("NotSameServers.json",game:GetService("HttpService"):JSONEncode(v1));end function TPReturner()local v6;if (v2=="") then v6=game.HttpService:JSONDecode(game:HttpGet("https://games.roblox.com/v1/games/"   .. v0   .. "/servers/Public?sortOrder=Asc&limit=100" ));else v6=game.HttpService:JSONDecode(game:HttpGet("https://games.roblox.com/v1/games/"   .. v0   .. "/servers/Public?sortOrder=Asc&limit=100&cursor="   .. v2 ));end local v7="";if (v6.nextPageCursor and (v6.nextPageCursor~="null") and (v6.nextPageCursor~=nil)) then v2=v6.nextPageCursor;end local v8=0;for v9,v10 in pairs(v6.data) do local v11=true;v7=tostring(v10.id);if (tonumber(v10.maxPlayers)>tonumber(v10.playing)) then for v13,v14 in pairs(v1) do if (v8~=0) then if (v7==tostring(v14)) then v11=false;end elseif (tonumber(v3)~=tonumber(v14)) then local v15=pcall(function()delfile("NotSameServers.json");v1={};table.insert(v1,v3);end);end v8=v8 + 1 ;end if (v11==true) then table.insert(v1,v7);wait();pcall(function()writefile("NotSameServers.json",game:GetService("HttpService"):JSONEncode(v1));wait();game:GetService("TeleportService"):TeleportToPlaceInstance(v0,v7,game.Players.LocalPlayer);end);wait(4);end end end end function Teleport()while wait() do pcall(function()TPReturner();if (v2~="") then TPReturner();end end);end end Teleport();end
    local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/SmellLikeHacker/IDK/main/GUI56"))()
    local Window = library:CreateWindow("SLH Hub | "..game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId).Name.." | V1.10")
    local Tab1 = Window:CreateTab("Main")
 local Sector1 = Tab1:CreateSector("Section1", "left")

 Sector1:AddToggle("AutoChest", false, function(t)
  _G.Chest = t
 end)
 Sector1:AddTextbox("Second" , "60" , function(w)
  _G.Second = w
 end)
 Sector1:AddToggle("Hopserver(Age Joined)", false, function(t)
  _G.Hop = t
 end)
 Sector1:AddToggle("EspMob", false, function(t)
  _G.EspMob = t
 end)
 Sector1:AddToggle("FreezeMob", false, function(t)
  _G.FreezeMob = t
 end)

 spawn(function()
  pcall(function()
   while wait() do
    if _G.EspMob then
     spawn(function()
      for i, v in pairs(game.Workspace:GetChildren()) do
       if v:FindFirstChild("Health") and v:FindFirstChild("IsSeaMonster") then
        if not v:FindFirstChild("Highlight") then
         Instance.new("Highlight", v).Adornee = v
        end
       end
      end
     end)
    end
   end
  end)
 end)

 spawn(function()
  pcall(function()
   while wait() do
    if _G.Chest then
     pcall(function()
      if workspace.RandomChests:FindFirstChildOfClass("Model") then
       for i,v in pairs(workspace.RandomChests:GetChildren()) do
        if v:IsA("Model") and v:FindFirstChild("HumanoidRootPart") then
         game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame
         fireproximityprompt(v.HumanoidRootPart.ProximityPrompt)
        end
       end
      else
       for i, v in pairs(game.Workspace:GetChildren()) do
        if string.find(v.Name, "ShipModel") then
         for i, x in pairs(v:GetChildren()) do
          if string.match(x.Name, "Chest_") then
           game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = x.HumanoidRootPart.CFrame
           wait()
           fireproximityprompt(x.HumanoidRootPart.ProximityPrompt)    
          end                                
         end
        end
       end
      end
     end)
    end
   end
  end)
 end)
 spawn(function()
  pcall(function()
   while wait() do
    if _G.Hop then
     pcall(function()
      local time = math.round(game.Workspace.DistributedGameTime)
      if time > tonumber(_G.Second) then
       hopserver()
       repeat wait() until a
      end
     end)
    end
   end
  end)
 end)

 function EquipSpears()
  pcall(function()
   for i,v in pairs(game:GetService("Players").LocalPlayer.PlayerGui.Interface.Inventory.QuickAccess:GetChildren()) do
    if v.ClassName == "Frame" then
     for ii,vv in pairs(v:GetChildren()) do
      for iii,vvv in pairs(vv:GetChildren()) do
       for iiii,vvvv in pairs(vvv:GetChildren()) do
        if vvvv.Name == "ItemViewport" then
         if vvvv:FindFirstChild("Model") then
          for e,o in pairs(vvvv:GetChildren()) do
           for ee,oo in pairs(o:GetChildren()) do
            if oo.Name == "Model" then
             for a,b in pairs(oo:GetChildren()) do
              for aa,bb in pairs(game:GetService("ReplicatedStorage").Assets.Spears:GetChildren()) do
               if b.Name == bb.Name then
                game:GetService("ReplicatedStorage"):WaitForChild("CloudFrameShared"):WaitForChild("DataStreams"):WaitForChild("SetEquippedItem"):InvokeServer(tonumber(v.Name))
               end
              end
             end
            end
           end
          end
         end
        end
       end
      end
     end
    end
   end
  end)
 end
 spawn(function()
  pcall(function()
   while wait() do
    if _G.FreezeMob then
     pcall(function()
      for i, v in pairs(game.Workspace:GetChildren()) do
       if v:FindFirstChild("Health") and v:FindFirstChild("IsSeaMonster") then
        if v.HumanoidRootPart.Anchored == false then
         v.HumanoidRootPart.Anchored = true
        end
       end
      end
     end)
    end
   end
  end)
 end)

        
local TabSetting = Window:CreateTab("Setting/Misc")
local Setting1 = TabSetting:CreateSector("Section1", "left")
Setting1:AddTextbox("Speed" , "16" , function(w)
 _G.Speed = w
end)
Setting1:AddTextbox("Jump" , "50" , function(w)
 _G.Jump = w
end)
Setting1:AddToggle("WalkSpeed", false, function(t)
 _G.WalkSpeed = t
end)
Setting1:AddToggle("JumpPower", false, function(t)
 _G.JumpPower = t
end)
Setting1:AddToggle("Ctrl+ClickTP", false, function(t)
 _G.CtrlClickTP = t
end)
Setting1:AddToggle("CloseGuiAfterExecute", false, function(o)
 _G.CloseGuiAfterExecute = o
end)
Setting1:AddButton("Rejoin" , function()
 game:GetService("TeleportService"):TeleportToPlaceInstance(game.PlaceId, game.JobId, game:GetService("Players").LocalPlayer)
end)
Setting1:AddButton("HopServer" , function()
 hopserver()
end)
Setting1:AddButton("FireProximityPrompt" , function()
 for i, v in pairs(game:GetService("Workspace"):GetDescendants()) do
  if v:IsA("ProximityPrompt") then
   fireproximityprompt(v)
  end
 end
end)
Setting1:AddButton("InstantProximityPrompt" , function()
 game:GetService("ProximityPromptService").PromptButtonHoldBegan:Connect(function(prompt)
  prompt.HoldDuration = 0
 end)
end)
spawn(function()
pcall(function()
 while task.wait() do
  pcall(function()
   if _G.WalkSpeed then
    pcall(function()
     game.Players.LocalPlayer.character.Humanoid.WalkSpeed = tonumber(_G.Speed)
    end)
   end
  end)
 end
end)
end)
spawn(function()
pcall(function()
 while task.wait() do
  pcall(function()
   if _G.JumpPower then
    pcall(function()
     game.Players.LocalPlayer.character.Humanoid.JumpPower = tonumber(_G.Jump)
    end)
   end
  end)
 end
end)
end)

local UIS = game:GetService("UserInputService")
local Player = game.Players.LocalPlayer
local Mouse = Player:GetMouse()
function GetCharacter()
 return game.Players.LocalPlayer.Character
 end
 function Teleport(pos)
 local Char = GetCharacter()
 if Char then
  Char:MoveTo(pos)
 end
end
UIS.InputBegan:Connect(function(input)
 if input.UserInputType == Enum.UserInputType.MouseButton1 and UIS:IsKeyDown(Enum.KeyCode.LeftControl) and _G.CtrlClickTP == true then
  Teleport(Mouse.Hit.p)
 end
end)

local Setting2 = TabSetting:CreateSector("Section2", "Right")
Setting2:AddDropdown("StatGuiPosition", {"Center","Left","Right"}, "Right", false, function(h)
 game:GetService("CoreGui").StatBySmell.Frame.UIListLayout.HorizontalAlignment = h
end)
Setting2:AddDropdown("CreditGuiPosition", {"Center","Left","Right"}, "Left", false, function(h)
 game:GetService("CoreGui").Credit.FRame.UIListLayout.HorizontalAlignment = h
end)
Setting2:AddToggle("StatGui", true, function(o)
 game:GetService("CoreGui").StatBySmell.Enabled = o
end)
Setting2:AddToggle("CreditGui", true, function(o)
 game:GetService("CoreGui").Credit.Enabled = o
end)
Setting2:AddToggle("RejoinIfGotKick", false, function(o)
 _G.rejoinKick = o
end)
spawn(function()
 getgenv().rejoin = game:GetService("CoreGui").RobloxPromptGui.promptOverlay.ChildAdded:Connect(function(Kick)
  if ((Kick.Name == "ErrorPrompt") and Kick:FindFirstChild("MessageArea") and Kick.MessageArea:FindFirstChild("ErrorFrame")) then
   if _G.rejoinKick == true then
    game:GetService("TeleportService"):Teleport(game.PlaceId)
   end
  end
 end)
end)
Setting2:AddToggle("BootsWhitescreen", false, function(o)
 _G.BootsWhitescreen = o
end)
Setting2:AddButton("infiniteyield" , function()
 loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
end)
Setting2:AddButton("ResetCamera" , function()
 game:GetService("Workspace").CurrentCamera:Destroy()
 wait(.1)
 game:GetService("Workspace").CurrentCamera.CameraSubject = game:GetService("Players").LocalPlayer.Character.Humanoid
 game:GetService("Workspace").CurrentCamera.CameraType = "Custom"
 game:GetService("Players").LocalPlayer.CameraMinZoomDistance = .5
 game:GetService("Players").LocalPlayer.CameraMaxZoomDistance = 100000
 game:GetService("Players").LocalPlayer.CameraMode = "Classic"
end)
Setting2:AddButton("CopyDiscordLink" , function()
 setclipboard("https://discord.gg/48geaWzacy")
end)
Setting2:AddButton("JoinDiscord" , function()
 request = http_request or request or HttpPost or syn.request
 request({Url = "http://127.0.0.1:6463/rpc?v=1",Method = "POST",Headers = {["Content-Type"] = "a
