--[[ 
VR ANYWHERE FIXED BY 64WILL64
(WiII#0300 on discord)
youtube.com/64will64gaming
]]
local options = {}

-- OPTIONS:

options.headscale = 3 -- how big you are in vr, 1 is default, 3 is recommended for max comfort in vr
options.forcebubblechat = true -- decide if to force bubblechat so you can see peoples messages

options.righthandhat = "Pal Hair" -- name of the accessory which you are using as your right hand
options.lefthandhat = "LavanderHair" -- name of the accessory which you are using as your left hand

options.righthandrotoffset = Vector3.new(0,0,0)
options.lefthandrotoffset = Vector3.new(0,0,0)

--

local plr = game:GetService("Players").LocalPlayer
local char = plr.Character

game:GetService("RunService").Heartbeat:Connect(function()
    for i,v in pairs(char:GetChildren()) do
        if v:IsA("Accessory") then
            v.Handle.Velocity = Vector3.new(0,30,0)
        end
    end
end)

local VR = game:GetService("VRService")
local input = game:GetService("UserInputService")

local cam = workspace.CurrentCamera

cam.CameraType = "Scriptable"

cam.HeadScale = options.headscale

wait()

game.Players.LocalPlayer.Character:MoveTo(game.Players.LocalPlayer.Character.HumanoidRootPart.Position + Vector3.new(0,0,15))

local function createpart(size, name)
	local Part = Instance.new("Part", char)
	Part.CFrame = char.HumanoidRootPart.CFrame
	Part.Size = size
	Part.Transparency = .99
	Part.CanCollide = false
	Part.Anchored = true
	Part.Name = name
end;

createpart(Vector3.new(1,1,2), "RH")
createpart(Vector3.new(1,1,2), "LH")

game.Players.LocalPlayer.Character.Archivable = true
local clone = game.Players.LocalPlayer.Character.Head:Clone()
clone.Parent = game.Players.LocalPlayer.Character
clone.Name = "H"
clone.Anchored = true
clone.Transparency = .99

game:GetService("StarterGui"):SetCore("VRLaserPointerMode", 0)
game:GetService("StarterGui"):SetCore("VREnableControllerModels", false)

local R1down = false

for i,v in pairs(char.Humanoid:GetAccessories()) do
	if v:FindFirstChild("Handle") then
		local handle = v.Handle

		if v.Name == options.righthandhat then
			handle:FindFirstChildOfClass("SpecialMesh"):Destroy()
		elseif v.Name == options.lefthandhat then
			handle:FindFirstChildOfClass("SpecialMesh"):Destroy()
		end
	end
end

char.Humanoid.AnimationPlayed:connect(function(anim)
	anim:Stop()
end)

for i,v in pairs(char.Humanoid:GetPlayingAnimationTracks()) do
	v:AdjustSpeed(0)
end

local torso = char:FindFirstChild("Torso") or char:FindFirstChild("UpperTorso")
torso.Anchored = true
char.HumanoidRootPart.Anchored = true

workspace.CurrentCamera.CFrame = CFrame.new(workspace.CurrentCamera.CFrame.Position)

input.UserCFrameChanged:Connect(function(Type, Value)
	if Type == Enum.UserCFrame.RightHand then
		char.RH.CFrame = cam.CoordinateFrame * (CFrame.new(Value.p*(cam.HeadScale-1))*Value)
	end
	if Type == Enum.UserCFrame.LeftHand then
		char.LH.CFrame = cam.CoordinateFrame * (CFrame.new(Value.p*(cam.HeadScale-1))*Value) 
	end
	if Type == Enum.UserCFrame.Head then
		char.H.CFrame = cam.CoordinateFrame * (CFrame.new(Value.p*(cam.HeadScale-1))*Value)
	end
end)

local function Align(Part1,Part0,CFrameOffset)
	local AlignPos = Instance.new('AlignPosition', Part1);
	AlignPos.Parent.CanCollide = false;
	AlignPos.ApplyAtCenterOfMass = true;
	AlignPos.MaxForce = 67752;
	AlignPos.MaxVelocity = math.huge/9e110;
	AlignPos.ReactionForceEnabled = false;
	AlignPos.Responsiveness = 200;
	AlignPos.RigidityEnabled = false;
	local AlignOri = Instance.new('AlignOrientation', Part1);
	AlignOri.MaxAngularVelocity = math.huge/9e110;
	AlignOri.MaxTorque = 67752;
	AlignOri.PrimaryAxisOnly = false;
	AlignOri.ReactionTorqueEnabled = false;
	AlignOri.Responsiveness = 200;
	AlignOri.RigidityEnabled = false;
	local AttachmentA=Instance.new('Attachment',Part1);
	local AttachmentB=Instance.new('Attachment',Part0);
	AttachmentB.CFrame = AttachmentB.CFrame * CFrameOffset
	AlignPos.Attachment0 = AttachmentA;
	AlignPos.Attachment1 = AttachmentB;
	AlignOri.Attachment0 = AttachmentA;
	AlignOri.Attachment1 = AttachmentB;
end

for _, accessweld in next, char:GetChildren() do
    if accessweld:IsA("Accessory") then
        accessweld.Handle:BreakJoints()
    end
end

for _, accesstrans in next, char:GetChildren() do
    if accesstrans:IsA("Accessory") then 
        if accesstrans.Name ~= options.lefthandhat and accesstrans.Name ~= options.righthandhat then
            accesstrans.Handle.Transparency = 1
        end
    end
end

Align(char:FindFirstChild(options.righthandhat).Handle,char.RH,CFrame.new(0,0,0))
Align(char:FindFirstChild(options.lefthandhat).Handle,char.LH,CFrame.new(0,0,0))

for _, Accessory in next, char:GetChildren() do
if Accessory:IsA("Accessory") and Accessory:FindFirstChild("Handle") and Accessory.Name ~= options.lefthandhat and Accessory.Name ~= options.righthandhat then
local Attachment1 = Accessory.Handle:FindFirstChildWhichIsA("Attachment")
local Attachment0 = char.H:FindFirstChild(tostring(Attachment1), true)
local Orientation = Instance.new("AlignOrientation")
local Position = Instance.new("AlignPosition")
print(Attachment1, Attachment0, Accessory)
Orientation.Attachment0 = Attachment1
Orientation.Attachment1 = Attachment0
Orientation.RigidityEnabled = false
Orientation.ReactionTorqueEnabled = true
Orientation.MaxTorque = 20000
Orientation.Responsiveness = 200
Orientation.Parent = char.H
Position.Attachment0 = Attachment1
Position.Attachment1 = Attachment0
Position.RigidityEnabled = false
Position.ReactionForceEnabled = true
Position.MaxForce = 40000
Position.Responsiveness = 200
Position.Parent = char.H
end
end

input.InputChanged:connect(function(key)
	if key.KeyCode == Enum.KeyCode.ButtonR1 then
		if key.Position.Z > 0.9 then
			R1down = true
		else
			R1down = false
		end
	end
end)

input.InputBegan:connect(function(key)
	if key.KeyCode == Enum.KeyCode.ButtonR1 then
		R1down = true
	end
end)

input.InputEnded:connect(function(key)
	if key.KeyCode == Enum.KeyCode.ButtonR1 then
		R1down = false
	end
end)

game:GetService("RunService").RenderStepped:connect(function()
	if R1down then
		cam.CFrame = cam.CFrame:Lerp(cam.CoordinateFrame + (char.RH.CFrame*CFrame.Angles(-math.rad(options.righthandrotoffset.X),-math.rad(options.righthandrotoffset.Y),math.rad(180-options.righthandrotoffset.X))).LookVector * cam.HeadScale/2, .5)
	end
end)

local function bubble(plr,msg)
	game:GetService("Chat"):Chat(plr.Character.Head,msg,Enum.ChatColor.White)
end

if options.forcebubblechat == true then
	game.Players.PlayerAdded:connect(function(plr)
		plr.Chatted:connect(function(msg)
			game:GetService("Chat"):Chat(plr.Character.Head,msg,Enum.ChatColor.White)
		end)
	end)

	for i,v in pairs(game.Players:GetPlayers()) do
		v.Chatted:connect(function(msg)
			game:GetService("Chat"):Chat(v.Character.Head,msg,Enum.ChatColor.White)
		end)
	end
end

for i,v in pairs(char:GetDescendants()) do
    if v:IsA("Tool") then
        v:Destroy()
    end
end
