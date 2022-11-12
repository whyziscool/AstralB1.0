--Asstral

loadstring(game:HttpGet('https://raw.githubusercontent.com/exhil13/AstralB1.0/3kdIKfmsdSf/AstralLogoV1', true))()

local lplr = game.Players.LocalPlayer
local cam = game:GetService("Workspace").CurrentCamera
local uis = game:GetService("UserInputService")
local KnitClient = debug.getupvalue(require(lplr.PlayerScripts.TS.knit).setup, 6)
local Client = require(game:GetService("ReplicatedStorage").TS.remotes).default.Client
local getremote = function(tab)
	for i,v in pairs(tab) do
		if v == "Client" then
			return tab[i + 1]
		end
	end
	return ""
end

local bedwars = {
	["SprintController"] = KnitClient.Controllers.SprintController,
	["ClientHandlerStore"] = require(lplr.PlayerScripts.TS.ui.store).ClientStore,
	["KnockbackUtil"] = require(game:GetService("ReplicatedStorage").TS.damage["knockback-util"]).KnockbackUtil,
	["PingController"] = require(lplr.PlayerScripts.TS.controllers.game.ping["ping-controller"]).PingController,
	["DamageIndicator"] = KnitClient.Controllers.DamageIndicatorController.spawnDamageIndicator,
	["SwordController"] = KnitClient.Controllers.SwordController,
	["ViewmodelController"] = KnitClient.Controllers.ViewmodelController,
	["SwordRemote"] = getremote(debug.getconstants((KnitClient.Controllers.SwordController).attackEntity)),
}
function getnearestplayer(maxdist)
	local obj = lplr
	local dist = math.huge
	for i,v in pairs(game:GetService("Players"):GetChildren()) do
		if v.Team ~= lplr.Team and v ~= lplr and isalive(v) and isalive(lplr) then
			local mag = (v.Character:FindFirstChild("HumanoidRootPart").Position - lplr.Character:FindFirstChild("HumanoidRootPart").Position).Magnitude
			if (mag < dist) and (mag < maxdist) then
				dist = mag
				obj = v
			end
		end
	end
	return obj
end
function isalive(plr)
	plr = plr or lplr
	if not plr.Character then return false end
	if not plr.Character:FindFirstChild("Head") then return false end
	if not plr.Character:FindFirstChild("Humanoid") then return false end
	return true
end

local BedwarsSwords = require(game:GetService("ReplicatedStorage").TS.games.bedwars["bedwars-swords"]).BedwarsSwords
function hashFunc(vec) 
	return {value = vec}
end
local function GetInventory(plr)
	if not plr then 
		return {items = {}, armor = {}}
	end

	local suc, ret = pcall(function() 
		return require(game:GetService("ReplicatedStorage").TS.inventory["inventory-util"]).InventoryUtil.getInventory(plr)
	end)

	if not suc then 
		return {items = {}, armor = {}}
	end

	if plr.Character and plr.Character:FindFirstChild("InventoryFolder") then 
		local invFolder = plr.Character:FindFirstChild("InventoryFolder").Value
		if not invFolder then return ret end
		for i,v in next, ret do 
			for i2, v2 in next, v do 
				if typeof(v2) == 'table' and v2.itemType then
					v2.instance = invFolder:FindFirstChild(v2.itemType)
				end
			end
			if typeof(v) == 'table' and v.itemType then
				v.instance = invFolder:FindFirstChild(v.itemType)
			end
		end
	end

	return ret
end
local function getSword()
	local highest, returning = -9e9, nil
	for i,v in next, GetInventory(lplr).items do 
		local power = table.find(BedwarsSwords, v.itemType)
		if not power then continue end
		if power > highest then 
			returning = v
			highest = power
		end
	end
	return returning
end
local HitRemote = Client:Get(bedwars["SwordRemote"])
local Distance = {["Value"] = 18}
local Enabled = true

local astralmainui = {}

local modules = {}
local ScrollingFrame = {}
local UIcount = 0
local binds = { -- list of characters you can bind a module to
	"a";
	"b";
	"c";
	"d";
	"e";
	"f";
	"g";
	"h";
	"i";
	"j";
	"k";
	"l";
	"m";
	"n";
	"o";
	"p";
	"q";
	"r";
	"s";
	"t";
	"u";
	"v";
	"w";
	"x";
	"y";
	"z"
}

function astralmainui.CreateNotification(mod,text,timer)
	local ScreenGui = Instance.new("ScreenGui")
	local Frame = Instance.new("Frame")
	local UICorner = Instance.new("UICorner")
	local TextLabel = Instance.new("TextLabel")
	local TextLabel2 = Instance.new("TextLabel")

	--Properties:

	ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

	Frame.Parent = ScreenGui
	Frame.BackgroundColor3 = Color3.fromRGB(59, 59, 59)
	Frame.Position = UDim2.new(0.833129585, 0, 0.850000024, 0)
	Frame.Size = UDim2.new(0, 273, 0, 100)

	UICorner.Parent = Frame

	TextLabel.Parent = ScreenGui
	TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	TextLabel.BackgroundTransparency = 1.000
	TextLabel.Position = UDim2.new(0.840464532, 0, 0.850000024, 0)
	TextLabel.Size = UDim2.new(0, 248, 0, 29)
	TextLabel.Font = Enum.Font.SourceSans
	TextLabel.Text = mod
	TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
	TextLabel.TextScaled = true
	TextLabel.TextSize = 14.000
	TextLabel.TextWrapped = true

	TextLabel2.Name = "TextLabel2"
	TextLabel2.Parent = ScreenGui
	TextLabel2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	TextLabel2.BackgroundTransparency = 1.000
	TextLabel2.Position = UDim2.new(0.840464532, 0, 0.89268297, 0)
	TextLabel2.Size = UDim2.new(0, 248, 0, 29)
	TextLabel2.Font = Enum.Font.SourceSans
	if text == "toggle" then
		TextLabel2.Text = mod.." has been toggled"
	else
		TextLabel2.Text = text
	end

	TextLabel2.TextColor3 = Color3.fromRGB(255, 255, 255)
	TextLabel2.TextScaled = true
	TextLabel2.TextSize = 14.000
	TextLabel2.TextWrapped = true
	task.wait(timer)
	ScreenGui:Destroy()
end


function astralmainui.CreateLib(name)
	UIcount = UIcount + 1
	local ScreenGui = Instance.new("ScreenGui")
	local ScrollingFrame = Instance.new("ScrollingFrame")
	local UIListLayout = Instance.new("UIListLayout")
	local TextButton = Instance.new("TextButton")
	local TextLabel = Instance.new("TextLabel")
	local drag = Instance.new("Frame",ScreenGui)
	drag.Position = UDim2.new(0.440097809*UIcount/3.5, 0, 0.207317069, 0)
	drag.Size = UDim2.new(0, 195, 0, 50)
	drag.Transparency = 1
	drag.Draggable = true
	ScrollingFrame.Draggable = true
	TextLabel.Draggable = true
	drag.Name = "Drag"
	--Properties:

	ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
	ScreenGui.Name = name

	ScrollingFrame.Parent = ScreenGui
	ScrollingFrame.Active = true
	ScrollingFrame.BackgroundColor3 = Color3.fromRGB(57, 57, 57)
	ScrollingFrame.BorderSizePixel = 0
	ScrollingFrame.Position = UDim2.new(0.440097809*UIcount/3.5, 0, 0.268292695, 0)
	ScrollingFrame.Size = UDim2.new(0, 195, 0, 421)
	ScrollingFrame.ScrollBarThickness = 0

	UIListLayout.Parent = ScrollingFrame
	UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
	UIListLayout.Padding = UDim.new(0, 2)
	TextLabel.Parent = ScreenGui
	TextLabel.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
	TextLabel.Position = UDim2.new(0.440097809*UIcount/3.5, 0-0.6, 0.207317069, 0)
	TextLabel.Size = UDim2.new(0, 195, 0, 50)
	TextLabel.Font = Enum.Font.SourceSans
	TextLabel.Text = name
	TextLabel.TextColor3 = Color3.fromRGB(144, 79, 255)
	TextLabel.TextScaled = true
	TextLabel.TextSize = 14.000
	TextLabel.TextWrapped = true
	local userInput = game:GetService("UserInputService")

	userInput.InputBegan:Connect(function(input,gameProcessed)
		if input.KeyCode == Enum.KeyCode.RightShift then
			local check = ScrollingFrame
			local check2 = TextLabel
			if check.Visible == true then
				check.Visible = false
				check2.Visible = false
			elseif check.Visible == false then
				check.Visible = true
				check2.Visible = true
			end

		end
	end)

end

function astralmainui.NewButton(name,func,lib)
	local TextButton = Instance.new("TextButton")
	TextButton.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")[lib].ScrollingFrame
	TextButton.BackgroundColor3 = Color3.fromRGB(38, 38, 38)
	TextButton.Position = UDim2.new(0, 0, -0.103048779, 0)
	TextButton.Size = UDim2.new(0, 200, 0, 50)
	TextButton.Font = Enum.Font.SourceSans
	TextButton.TextColor3 = Color3.fromRGB(118, 56, 190)
	TextButton.TextScaled = true
	TextButton.TextSize = 14.000
	TextButton.TextWrapped = true
	TextButton.Text = name
	TextButton.MouseButton1Down:Connect(function()
		local func2 = func
		modules[func]()
	end)
	local bind
	local UserInputService = game:GetService("UserInputService")
	local player = game.Players.LocalPlayer
	local mouse = player:GetMouse()

	mouse.KeyDown:connect(function(key)
		if key == bind then
			local func2 = func
			modules[func]()
		end
	end)

	TextButton.MouseButton2Down:Connect(function()
		local binding = true
		local userInput = game:GetService("UserInputService")

		local ScreenGui = Instance.new("ScreenGui")
		local TextBox = Instance.new("TextBox")

		--Properties:

		ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

		TextBox.Parent = ScreenGui
		TextBox.BackgroundColor3 = Color3.fromRGB(140, 19, 134)
		TextBox.Position = UDim2.new(0.389975548, 0, 0.896341443*0.232, 0)
		TextBox.Size = UDim2.new(0, 359, 0, 61)
		TextBox.Font = Enum.Font.SourceSans
		TextBox.Text = ""
		TextBox.TextColor3 = Color3.fromRGB(0, 0, 0)
		TextBox.TextScaled = true
		TextBox.TextSize = 14.000
		TextBox.TextWrapped = true
		TextBox.FocusLost:Connect(function()
			bind = TextBox.Text
			TextBox:Destroy()
		end)
	end)
end

function modules.Aura()
	repeat
        task.wait(0.12)
        local nearest = getnearestplayer(Distance["Value"])
        if nearest ~= nil and nearest.Team ~= lplr.Team and isalive(nearest) and nearest.Character:FindFirstChild("Humanoid").Health > 0.1 and isalive(lplr) and lplr.Character:FindFirstChild("Humanoid").Health > 0.1 and not nearest.Character:FindFirstChild("ForceField") then
            local sword = getSword()
            spawn(function()
                local anim = Instance.new("Animation")
                anim.AnimationId = "rbxassetid://4947108314"
                local animator = lplr.Character:FindFirstChild("Humanoid"):FindFirstChild("Animator")
                animator:LoadAnimation(anim):Play()
                anim:Destroy()
                bedwars["ViewmodelController"]:playAnimation(15)
            end)
            if sword ~= nil then
                bedwars["SwordController"].lastAttack = game:GetService("Workspace"):GetServerTimeNow() - 0.11
                HitRemote:SendToServer({
                    ["weapon"] = sword.tool,
                    ["entityInstance"] = nearest.Character,
                    ["validate"] = {
                        ["raycast"] = {
                            ["cameraPosition"] = hashFunc(cam.CFrame.Position),
                            ["cursorDirection"] = hashFunc(Ray.new(cam.CFrame.Position, nearest.Character:FindFirstChild("HumanoidRootPart").Position).Unit.Direction)
                        },
                        ["targetPosition"] = hashFunc(nearest.Character:FindFirstChild("HumanoidRootPart").Position),
                        ["selfPosition"] = hashFunc(lplr.Character:FindFirstChild("HumanoidRootPart").Position + ((lplr.Character:FindFirstChild("HumanoidRootPart").Position - nearest.Character:FindFirstChild("HumanoidRootPart").Position).magnitude > 14 and (CFrame.lookAt(lplr.Character:FindFirstChild("HumanoidRootPart").Position, nearest.Character:FindFirstChild("HumanoidRootPart").Position).LookVector * 4) or Vector3.new(0, 0, 0)))
                    },
                    ["chargedAttack"] = {["chargeRatio"] = 0.8}
                })
            end
        end
    until not Enabled
end

function modules.Velocity()
	bedwars["kbDirectionStrength"] = 0
	bedwars["kbUpwardStrength"] = 0
	ui.CreateNotification("Velocity","toggle",3)
end


function modules.CFrameSpeed()
	Speed = 0.17

	_G.Speed = true

	You = game.Players.LocalPlayer.Name
	UIS = game:GetService("UserInputService")

	while _G.Speed do
		if UIS:IsKeyDown(Enum.KeyCode.W) then
			game:GetService("Workspace")[You].HumanoidRootPart.CFrame = game:GetService("Workspace")[You].HumanoidRootPart.CFrame * CFrame.new(0,0,-Speed)
		end;
		if UIS:IsKeyDown(Enum.KeyCode.A) then
			game:GetService("Workspace")[You].HumanoidRootPart.CFrame = game:GetService("Workspace")[You].HumanoidRootPart.CFrame * CFrame.new(-Speed,0,0)
		end;
		if UIS:IsKeyDown(Enum.KeyCode.S) then
			game:GetService("Workspace")[You].HumanoidRootPart.CFrame = game:GetService("Workspace")[You].HumanoidRootPart.CFrame * CFrame.new(0,0,Speed)
		end;
		if UIS:IsKeyDown(Enum.KeyCode.D) then
			game:GetService("Workspace")[You].HumanoidRootPart.CFrame = game:GetService("Workspace")[You].HumanoidRootPart.CFrame * CFrame.new(Speed,0,0)
		end;
		wait()
	end
	ui.CreateNotification("Speed - CFrame","toggle",3)
end

function modules.Fly1()
	local e = Instance.new("Part",workspace)
	e.Size = Vector3.new(99999999,2,999999999999)
	e.Position = game.Players.LocalPlayer.Character.HumanoidRootPart.Position
	e.CFrame = e.CFrame - Vector3.new(0,5.2,0)
	e.Anchored = true
	e.Transparency = 1

	local function PlayerTouched(Part)
		local Parent = Part.Parent
		if game.Players:GetPlayerFromCharacter(Parent) then
			wait(2)
			e:Destroy()
			workspace.Gravity = 196.2
		end
	end

	e.Touched:connect(PlayerTouched)
	ui.CreateNotification("Fly1","toggle",3)
end

local sprintEnabled = false
function modules.sprint()
    if sprintEnabled == false then
        sprintEnabled = true
    elseif sprintEnabled == true then
        sprintEnabled = false
    end
    repeat
        wait()
    if not bedwars["SprintController"].sprinting then
        bedwars["SprintController"]:startSprinting()
        end
        until sprintEnabled == false
end

local Distance = {["Value"] = 30}
function getbeds()
    local beds = {}
    for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
        if string.lower(v.Name) == "bed" and v:FindFirstChild("Covers") ~= nil and v:FindFirstChild("Covers").Color ~= lplr.Team.TeamColor then
            table.insert(beds,v)
        end
    end
    return beds
end
function isalive(plr)
    plr = plr or lplr
    if not plr.Character then return false end
    if not plr.Character:FindFirstChild("Head") then return false end
    if not plr.Character:FindFirstChild("Humanoid") then return false end
    return true
end
function getserverpos(Position)
    local x = math.round(Position.X/3)
    local y = math.round(Position.Y/3)
    local z = math.round(Position.Z/3)
    return Vector3.new(x,y,z)
end
function modules.Nuker()
    local Enabled = true
    repeat
        task.wait(0.1)
        if isalive(lplr) and lplr.Character:FindFirstChild("Humanoid").Health > 0.1 then
            local beds = getbeds()
            for i,v in pairs(beds) do
                local mag = (v.Position - lplr.Character:FindFirstChild("HumanoidRootPart").Position).Magnitude
                if mag < Distance["Value"] then
                    game:GetService("ReplicatedStorage").rbxts_include.node_modules:FindFirstChild("@rbxts").net.out._NetManaged.DamageBlock:InvokeServer({
                        ["blockRef"] = {
                            ["blockPosition"] = getserverpos(v.Position)
                        },
                        ["hitPosition"] = getserverpos(v.Position),
                        ["hitNormal"] = getserverpos(v.Position)
                    })
                end
            end
        end
    until not Enabled
end

function modules.HighJump()
	local Velocity = Instance.new("BodyVelocity",game.Players.LocalPlayer.Character.HumanoidRootPart)
	Velocity.Name = "Velocity1"
	Velocity.Velocity = Vector3.new(0,10000,0)
	game.Workspace.Gravity = 0
	wait(1.5)
	game.Workspace.Gravity = 192.6
	game.Players.LocalPlayer.Character.HumanoidRootPart.Velocity1:Destroy()
end

function modules.DamageLessTPHighJump()
	game.Workspace.Gravity = 1
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 50, 0)
wait()
game.Workspace.Gravity = 192.6
end

function modules.LongJump()
	game.Players.LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
	game.Workspace.Gravity = 10
	wait(2.2)
	game.Workspace.Gravity = 192.6
end

function modules.ESP()
	local gui = Instance.new("BillboardGui");
	gui.Name = "names";
	gui.AlwaysOnTop = true;
	gui.LightInfluence = 0;
    gui.Size = UDim2.new(1.75, 0, 1.75, 0);
	local frame = Instance.new("Frame", gui);
	frame.BackgroundColor3 = Color3.fromRGB(170, 0, 0);
	frame.Size = UDim2.new(1.7, 0, 3.89, 0);
	frame.BorderSizePixel = 4;
	frame.BorderColor3 = Color3.fromRGB(0, 0, 0);
	local gi = gui:Clone();
	body = frame:Clone();
	body.Parent = gi;
	body.BackgroundColor3 = Color3.fromRGB(0, 170, 170);

	for _, v in pairs(game:GetService("Players"):GetPlayers()) do
		if v.Name ~= game:GetService("Players").LocalPlayer.Name and v.Character and v.Character:FindFirstChild("Head") then
			gui:Clone().Parent = v.Character.Head;
		end
	end
end

function modules.Chams()
	local players = game.Players:GetPlayers()

		for i,v in pairs(players) do
			local esp = Instance.new("Highlight")
			esp.Name = v.Name
			esp.FillTransparency = 0.5
			esp.FillColor = Color3.new(0.462745, 0, 0.462745)
			esp.OutlineColor = Color3.new(0.462745, 0, 0.462745)
			esp.OutlineTransparency = 0
			esp.Parent = v.Character
		end
		game.Players.PlayerAdded:Connect(function(plr)
			plr.CharacterAdded:Connect(function(chr)
				local esp = Instance.new("Highlight")
				esp.Name = plr.Name
				esp.FillTransparency = 0.5
				esp.FillColor = Color3.new(0.462745, 0, 0.462745)
				esp.OutlineColor = Color3.new(0.462745, 0, 0.462745)
				esp.OutlineTransparency = 0
				esp.Parent = chr
			end)
	end)
end

function modules.NoFall()
    while true do
		wait()
		game:GetService("ReplicatedStorage").rbxts_include.node_modules:FindFirstChild("@rbxts").net.out._NetManaged.GroundHit:FireServer()
	end
end


function modules.AntiVoid()
    local e = Instance.new("Part",workspace)
		e.Size = Vector3.new(99999999,2,999999999999)
		e.Position = Vector3.new(0,27,0)
		e.Anchored = true
		e.BrickColor = BrickColor.new("Royal purple")
		e.Transparency = 0.5


		local function PlayerTouched(Part)
			local Parent = Part.Parent
			if game.Players:GetPlayerFromCharacter(Parent) then
				for i = 1,3 do wait()
					Parent.HumanoidRootPart.CFrame = Parent.HumanoidRootPart.CFrame + Vector3.new(0,25,0)
				end

			end
		end

		e.Touched:connect(PlayerTouched)
end

--library stuff now XD
--@Spring67#6969, @TheRoSploiter#0001, and @Damc#7534 helped make this if your looking at the code lol

astralmainui.CreateLib("Combat")
astralmainui.NewButton("KillAura","Aura","Combat")
astralmainui.NewButton("Velocity","Velocity","Combat")
astralmainui.NewButton("Sprint","sprint","Combat")

astralmainui.CreateLib("Movement")
astralmainui.NewButton("Speed","CFrameSpeed","Movement")
astralmainui.NewButton("Fly1","Fly1","Movement")
astralmainui.NewButton("LongJump","LongJump","Movement")
astralmainui.NewButton("HighJump","HighJump","Movement")
astralmainui.NewButton("TpHighJump","DamageLessTPHighJump","Movement")

astralmainui.CreateLib("Visuals")
astralmainui.NewButton("ESP","ESP","Visuals")
astralmainui.NewButton("Chams","Chams","Visuals")

astralmainui.CreateLib("Other")
astralmainui.NewButton("NoFall","NoFall","Other")
astralmainui.NewButton("AntiVoid","AntiVoid","Other")
astralmainui.NewButton("Nuker","Nuker","Other")
