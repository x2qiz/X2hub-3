local FLINGROT = Vector3.new(1000, 1000, 1000)


local Lib = {}
local CharaUI = Instance.new("ScreenGui")
local Main = Instance.new("Frame")
local TheEffect = Instance.new("ImageLabel")
local Title = Instance.new("TextLabel")
local ExecuteButton = Instance.new("TextButton")
local ExecuteUIGrid = Instance.new("UICorner")
local Options = Instance.new("Frame")
local UIListLayout = Instance.new("UIListLayout")




CharaUI.Name = "CharaUI"
CharaUI.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")


Main.Name = "Main"
Main.Parent = CharaUI
Main.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
Main.BorderSizePixel = 0
Main.Position = UDim2.new(0.288261503, 0, 0.290196091, 0)
Main.Size = UDim2.new(0, 460, 0, 299)

pcall(function()
	function dragify(Frame)
		dragToggle = nil
		dragSpeed = .25 -- You can edit this.
		dragInput = nil
		dragStart = nil
		dragPos = nil

		function updateInput(input)
			Delta = input.Position - dragStart
			Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + Delta.X, startPos.Y.Scale, startPos.Y.Offset + Delta.Y)
			game:GetService("TweenService"):Create(Frame, TweenInfo.new(.25), {Position = Position}):Play()
		end

		Frame.InputBegan:Connect(function(input)
			if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then
				dragToggle = true
				dragStart = input.Position
				startPos = Frame.Position
				input.Changed:Connect(function()
					if (input.UserInputState == Enum.UserInputState.End) then
						dragToggle = false
					end
				end)
			end
		end)

		Frame.InputChanged:Connect(function(input)
			if (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
				dragInput = input
			end
		end)

		game:GetService("UserInputService").InputChanged:Connect(function(input)
			if (input == dragInput and dragToggle) then
				updateInput(input)
			end
		end)
	end
end)
dragify(Main)

TheEffect.Name = "The Effect"
TheEffect.Parent = Main
TheEffect.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TheEffect.BackgroundTransparency = 1.000
TheEffect.Size = UDim2.new(0, 460, 0, 299)
TheEffect.Image = "rbxassetid://9118540849"

Title.Name = "Title"
Title.Parent = Main
Title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Title.BackgroundTransparency = 1.000
Title.Position = UDim2.new(0.0159991048, 0, 0.022637561, 0)
Title.Size = UDim2.new(0, 281, 0, 16)
Title.Font = Enum.Font.GothamSemibold
Title.Text = "Charas Cannon"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 20.000
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.TextYAlignment = Enum.TextYAlignment.Top

ExecuteButton.Name = "Execute Button"
ExecuteButton.Parent = Main
ExecuteButton.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
ExecuteButton.BorderSizePixel = 0
ExecuteButton.Position = UDim2.new(0.0304186046, 0, 0.874365568, 0)
ExecuteButton.Size = UDim2.new(0, 312, 0, 29)
ExecuteButton.Font = Enum.Font.Gotham
ExecuteButton.Text = "Execute"
ExecuteButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ExecuteButton.TextSize = 14.000
ExecuteButton.TextTransparency = 0.200
ExecuteButton.MouseButton1Down:Connect(function()
    CharaUI:Destroy()

	local netboost = 1500 --velocity 
--netboost usage: 
--set to false to disable
--vector3 if you dont want the velocity to change
--number to change the velocity in real time with magnitude equal to the number
local simradius = "shp" --simulation radius method
--"shp" - sethiddenproperty
--"ssr" - setsimulationradius
--false - disable
local newanimate = true --disable the animate script and enable after reanimation
local R15toR6 = true --tries to convert your character to r6 if its r15
local addtools = false --puts all tools from backpack to character and lets you hold them after reanimation
local loadtime = game:GetService("Players").RespawnTime + 0.5 --anti respawn delay
local method = 3 --reanimation method
--methods:
--0 - breakJoints (takes [loadtime] seconds to laod)
--1 - limbs
--2 - limbs + anti respawn
--3 - limbs + breakJoints after [loadtime] seconds
--4 - remove humanoid + breakJoints
--5 - remove humanoid + limbs
local alignmode = 2 --AlingPosition mode
--modes:
--1 - AlignPosition rigidity enabled true
--2 - 2 AlignPositions rigidity enabled both true and false
--3 - AlignPosition rigidity enabled false
local hedafterneck = true --disable aligns for head and enable after neck is removed

local lp = game:GetService("Players").LocalPlayer
local rs = game:GetService("RunService")
local stepped = rs.Stepped
local heartbeat = rs.Heartbeat
local renderstepped = rs.RenderStepped
local sg = game:GetService("StarterGui")
local ws = game:GetService("Workspace")

local c = lp.Character

local function gp(parent, name, className)
	local ret = nil
	if parent then
		for i, v in pairs(parent:GetChildren()) do
			if (v.Name == name) and v:IsA(className) then
				ret = v
			end
		end
	end
	return ret
end

local function align(Part0, Part1)
	Part0.CustomPhysicalProperties = PhysicalProperties.new(0.0001, 0.0001, 0.0001, 0.0001, 0.0001)

	local att1 = Instance.new("Attachment")
	att1.Orientation = Vector3.new(0, 0, 0)
	att1.Position = Vector3.new(0, 0, 0)
	att1.Archivable = true
	local att0 = att1:Clone()

	if (alignmode == 1) or (alignmode == 2) then
    	local ape = Instance.new("AlignPosition", att0)
    	ape.ApplyAtCenterOfMass = false
    	ape.MaxForce = math.huge
    	ape.MaxVelocity = math.huge
    	ape.ReactionForceEnabled = false
    	ape.Responsiveness = 200
    	ape.Attachment1 = att1
    	ape.Attachment0 = att0
    	ape.Name = "AlignPositionRtrue"
    	ape.RigidityEnabled = true
	end

	if (alignmode == 2) or (alignmode == 3) then
    	local apd = Instance.new("AlignPosition", att0)
    	apd.ApplyAtCenterOfMass = false
    	apd.MaxForce = math.huge
    	apd.MaxVelocity = math.huge
    	apd.ReactionForceEnabled = false
    	apd.Responsiveness = 200
    	apd.Attachment1 = att1
    	apd.Attachment0 = att0
    	apd.Name = "AlignPositionRfalse"
    	apd.RigidityEnabled = false
    end

	local ao = Instance.new("AlignOrientation", att0)
	ao.MaxAngularVelocity = math.huge
	ao.MaxTorque = math.huge
	ao.PrimaryAxisOnly = false
	ao.ReactionTorqueEnabled = false
	ao.Responsiveness = 200
	ao.Attachment1 = att1
	ao.Attachment0 = att0
	ao.RigidityEnabled = false

	att1.Parent = Part1
	att1.Name = "att1_" .. Part1.Name

	att0.Parent = Part0
	att0.Name = "att0_" .. Part0.Name
	
	if typeof(netboost) == "Vector3" then
	    spawn(function()
	        local vel = Vector3.new(0, 0, 0)
        	while Part0 and Part0.Parent do
                Part0.Velocity = vel
                heartbeat:Wait()
                if Part0 and Part0.Parent then
                    vel = Part0.Velocity
                    Part0.Velocity = netboost
                    stepped:Wait()
                end
            end
        end)
	end

    if typeof(netboost) == "number" then
        spawn(function()
	        local vel = Vector3.new(0, 0, 0)
        	while Part0 and Part0.Parent do
                Part0.Velocity = vel
                heartbeat:Wait()
                if Part0 and Part0.Parent then
                    local newvel = vel
                    local mag = newvel.Magnitude
                    if mag < 0.1 then
                        newvel = Vector3.new(0, netboost, 0)
                    else
                        local multiplier = netboost / mag
                        newvel *= Vector3.new(multiplier,  multiplier, multiplier)
                    end
                    vel = Part0.Velocity
                    Part0.Velocity = newvel
                    stepped:Wait()
                end
            end
        end)
    end
end

local function respawnrequest()
    local c = lp.Character
    local ccfr = ws.CurrentCamera.CFrame
	local fc = Instance.new("Model")
	local nh = Instance.new("Humanoid", fc)
	lp.Character = fc
	nh.Health = 0
	lp.Character = c
	fc:Destroy()
    local con = nil
    local function confunc()
        con:Disconnect()
        ws.CurrentCamera.CFrame = ccfr
    end
    con = renderstepped:Connect(confunc)
end

local destroyhum = (method == 4) or (method == 5)
local breakjoints = (method == 0) or (method == 4)
local antirespawn = (method == 0) or (method == 2) or (method == 3)

addtools = addtools and gp(lp, "Backpack", "Backpack")

if not (c and c.Parent) then
    return
end

if simradius == "shp" then
    local shp = sethiddenproperty or set_hidden_property or set_hidden_prop or sethiddenprop
    if shp then
        spawn(function()
            while heartbeat:Wait() and c and c.Parent do
                shp(lp, "SimulationRadius", math.huge)
            end
        end)
    end
end

if simradius == "ssr" then
    local ssr = setsimulationradius or set_simulation_radius or set_sim_radius or setsimradius or set_simulation_rad or setsimulationrad
    if ssr then
        spawn(function()
            while stepped:Wait() and c and c.Parent do
                ssr(math.huge)
            end
        end)
    end
end

if antirespawn then
    respawnrequest()
end

if method == 0 then
	wait(loadtime)
	if not (c and c.Parent) then
	    return
	end
end

if newanimate then
    local animate = gp(c, "Animate", "LocalScript")
    if animate and (not animate.Disabled) then
        animate.Disabled = true
    else
        newanimate = false
    end
end

local hum = c:FindFirstChildOfClass("Humanoid")
if hum then
    for i, v in pairs(hum:GetPlayingAnimationTracks()) do
	    v:Stop()
    end
end

if addtools then
    for i, v in pairs(addtools:GetChildren()) do
        if v and v.Parent and v:IsA("Tool") then
            v.Parent = c
        end
    end
end

pcall(function()
    settings().Physics.AllowSleep = false
    settings().Physics.PhysicsEnvironmentalThrottle = Enum.EnviromentalPhysicsThrottle.Disabled
end)

local OLDscripts = {}

for i, v in pairs(c:GetDescendants()) do
	if v.ClassName == "Script" then
		table.insert(OLDscripts, v)
	end
end

local scriptNames = {}

for i, v in pairs(c:GetDescendants()) do
	if v and v.Parent and v:IsA("BasePart") then
	    local newName = tostring(i)
	    local exists = true
	    while exists do
		    exists = false
		    for i, v in pairs(OLDscripts) do
		        if v.Name == newName then
		            exists = true
		        end
		    end
		    if exists then
		        newName = newName .. "_"    
		    end
	    end
        table.insert(scriptNames, newName)
		Instance.new("Script", v).Name = newName
	end
end

c.Archivable = true
local cl = c:Clone()
for i, v in pairs(cl:GetDescendants()) do
    pcall(function()
        v.Transparency = 1
        v.Anchored = false
    end)
end

local model = Instance.new("Model", c)
model.Name = model.ClassName

for i, v in pairs(c:GetChildren()) do
	if v and v.Parent and (v ~= model) then
	    if destroyhum and v:IsA("Humanoid") then
	        v:Destroy()
	    else
	        if addtools and v:IsA("Tool") then
	            for i1, v1 in pairs(v:GetDescendants()) do
	                if v1 and v1.Parent and v1:IsA("BasePart") then
	                    local bv = Instance.new("BodyVelocity", v1)
	                    bv.Velocity = Vector3.new(0, 0, 0)
	                    bv.MaxForce = Vector3.new(1000, 1000, 1000)
	                    bv.P = 1250
	                    bv.Name = "bv_" .. v.Name
	                end
	            end
	        end
		    v.Parent = model
	    end
	end
end
local head = gp(model, "Head", "BasePart")
local torso = gp(model, "Torso", "BasePart") or gp(model, "UpperTorso", "BasePart")
if breakjoints then
    model:BreakJoints()
else
    if head and torso then
        for i, v in pairs(model:GetDescendants()) do
            if v and v.Parent and v:IsA("Weld") or v:IsA("Snap") or v:IsA("Glue") or v:IsA("Motor") or v:IsA("Motor6D") then
                local save = false
                if (v.Part0 == torso) and (v.Part1 == head) then
                    save = true
                end
                if (v.Part0 == head) and (v.Part1 == torso) then
                    save = true
                end
                if save then
                    if hedafterneck then
                        hedafterneck = v
                    end
                else
                    v:Destroy()
                end
            end
        end
    end
    if method == 3 then
        spawn(function()
            wait(loadtime)
            if model and model.Parent then
                model:BreakJoints()
            end
        end)
    end
end

cl.Parent = c
for i, v in pairs(cl:GetChildren()) do
	if v and v.Parent then
		v.Parent = c
	end
end
cl:Destroy()

local ccolcon = nil
	local function ccolf()
		if c and c.Parent then
			for i, v in pairs(c:GetDescendants()) do
				if v:IsA("BasePart") then
					v.CanCollide = false
				end
			end
		else
			ccolcon:Disconnect()
		end
	end
	ccolcon = stepped:Connect(ccolf)
	ccolf()

for i, scr in pairs(model:GetDescendants()) do
	if scr and scr.Parent and (scr.ClassName == "Script") and table.find(scriptNames, scr.Name) then
		local Part0 = scr.Parent
		if Part0:IsA("BasePart") then
			for i1, scr1 in pairs(c:GetDescendants()) do
				if scr1 and scr1.Parent and (scr1.ClassName == "Script") and (scr1.Name == scr.Name) and (not scr1:IsDescendantOf(model)) then
					local Part1 = scr1.Parent
					if (Part1.ClassName == Part0.ClassName) and (Part1.Name == Part0.Name) then
						align(Part0, Part1)
					end
				end
			end
		end
	end
end

if (typeof(hedafterneck) == "Instance") and head and head.Parent then
    local aligns = {}
    for i, v in pairs(head:GetDescendants()) do
        if v and v.Parent and (v:IsA("AlignPosition") or v:IsA("AlignOrientation")) then
            table.insert(aligns, v)
            v.Enabled = false
        end
    end
    spawn(function()
        while c and c.Parent and hedafterneck and hedafterneck.Parent do
            stepped:Wait()
        end
        if not (c and c.Parent and head and head.Parent) then
            return
        end
        for i, v in pairs(aligns) do
            pcall(function()
                v.Enabled = true
            end)
        end
    end)
end

for i, v in pairs(c:GetDescendants()) do
	if v and v.Parent then
		if v.ClassName == "Script" then
			if table.find(scriptNames, v.Name) then
				v:Destroy()
			end
		else
		    if not v:IsDescendantOf(model) then
				if v:IsA("Decal") then
				    v.Transparency = 1
				end
				if v:IsA("ForceField") then
				    v.Visible = false
				end
				if v:IsA("Sound") then
				    v.Playing = false
				end
				if v:IsA("BillboardGui") or v:IsA("SurfaceGui") or v:IsA("ParticleEmitter") or v:IsA("Fire") or v:IsA("Smoke") or v:IsA("Sparkles") then
					v.Enabled = false
				end
			end
		end
	end
end

if newanimate then
    local animate = gp(c, "Animate", "LocalScript")
    if animate then
        animate.Disabled = false
    end
end

if addtools then
    for i, v in pairs(c:GetChildren()) do
        if v and v.Parent and v:IsA("Tool") then
            v.Parent = addtools
        end
    end
end

local hum0 = model:FindFirstChildOfClass("Humanoid")
local hum1 = c:FindFirstChildOfClass("Humanoid")
if hum1 then
	ws.CurrentCamera.CameraSubject = hum1
	if hum0 then
		hum0.Changed:Connect(function(prop)
			if (prop == "Jump") and hum1 and hum1.Parent then
				hum1.Jump = hum0.Jump
			end
		end)
	else
	    lp.Character = nil
	    lp.Character = c
	end
end

local rb = Instance.new("BindableEvent", c)
rb.Event:Connect(function()
	rb:Destroy()
	sg:SetCore("ResetButtonCallback", true)
	if destroyhum then
	    c:BreakJoints()
	    return
	end
	if antirespawn then
	    if hum0 and hum0.Parent and (hum0.Health > 0) then
	        model:BreakJoints()
	        hum0.Health = 0
	    end
		respawnrequest()
	else
	    if hum0 and hum0.Parent and (hum0.Health > 0) then
	        model:BreakJoints()
	        hum0.Health = 0
	    end
	end
end)
sg:SetCore("ResetButtonCallback", rb)

spawn(function()
	while c and c.Parent do
		if hum0 and hum0.Parent and hum1 and hum1.Parent then
            hum1.Jump = hum0.Jump
        end
		wait()
	end
	sg:SetCore("ResetButtonCallback", true)
end)

R15toR6 = R15toR6 and hum1 and (hum1.RigType == Enum.HumanoidRigType.R15)
if R15toR6 then
	local cf = nil
	pcall(function()
		cf = gp(c, "HumanoidRootPart", "BasePart").CFrame
	end)
	if cf then
		local R6parts = { 
			head = {
				Name = "Head",
				Size = Vector3.new(2, 1, 1),
				R15 = {
					Head = 0
				}
			},
			torso = {
				Name = "Torso",
				Size = Vector3.new(2, 2, 1),
				R15 = {
					UpperTorso = 0.2,
					LowerTorso = -0.8
				}
			},
			root = {
				Name = "HumanoidRootPart",
				Size = Vector3.new(2, 2, 1),
				R15 = {
					HumanoidRootPart = 0
				}
			},
			leftArm = {
				Name = "Left Arm",
				Size = Vector3.new(1, 2, 1),
				R15 = {
					LeftHand = -0.85,
					LeftLowerArm = -0.2,
					LeftUpperArm = 0.4
				}
			},
			rightArm = {
				Name = "Right Arm",
				Size = Vector3.new(1, 2, 1),
				R15 = {
					RightHand = -0.85,
					RightLowerArm = -0.2,
					RightUpperArm = 0.4
				}
			},
			leftLeg = {
				Name = "Left Leg",
				Size = Vector3.new(1, 2, 1),
				R15 = {
					LeftFoot = -0.85,
					LeftLowerLeg = -0.15,
					LeftUpperLeg = 0.6
				}
			},
			rightLeg = {
				Name = "Right Leg",
				Size = Vector3.new(1, 2, 1),
				R15 = {
					RightFoot = -0.85,
					RightLowerLeg = -0.15,
					RightUpperLeg = 0.6
				}
			}
		}
		for i, v in pairs(c:GetChildren()) do
			if v:IsA("BasePart") then
				for i1, v1 in pairs(v:GetChildren()) do
					if v1:IsA("Motor6D") then
						v1.Part0 = nil
					end
				end
			end
		end
		for i, v in pairs(R6parts) do
			local part = Instance.new("Part")
			part.Name = v.Name
			part.Size = v.Size
			part.CFrame = cf
			part.Anchored = false
			part.Transparency = 1
			part.CanCollide = false
			for i1, v1 in pairs(v.R15) do
				local R15part = gp(c, i1, "BasePart")
				if R15part then
					local weld = Instance.new("Weld", R15part)
					weld.Part0 = part
					weld.Part1 = R15part
					weld.C0 = CFrame.new(0, v1, 0)
					weld.C1 = CFrame.new(0, 0, 0)
					R15part.Massless = true
					R15part.Name = "R15_" .. i1
				    R15part.Parent = part
				end
			end
			part.Parent = c
			R6parts[i] = part
		end
		local R6joints = {
			neck = {
				Parent = R6parts.torso,
				Name = "Neck",
				Part0 = R6parts.torso,
				Part1 = R6parts.head,
				C0 = CFrame.new(0, 1, 0, -1, 0, 0, 0, 0, 1, 0, 1, -0),
				C1 = CFrame.new(0, -0.5, 0, -1, 0, 0, 0, 0, 1, 0, 1, -0)
			},
			rootJoint = {
				Parent = R6parts.root,
				Name = "RootJoint" ,
				Part0 = R6parts.root,
				Part1 = R6parts.torso,
				C0 = CFrame.new(0, 0, 0, -1, 0, 0, 0, 0, 1, 0, 1, -0),
				C1 = CFrame.new(0, 0, 0, -1, 0, 0, 0, 0, 1, 0, 1, -0)
			},
			rightShoulder = {
				Parent = R6parts.torso,
				Name = "Right Shoulder",
				Part0 = R6parts.torso,
				Part1 = R6parts.rightArm,
				C0 = CFrame.new(1, 0.5, 0, 0, 0, 1, 0, 1, -0, -1, 0, 0),
				C1 = CFrame.new(-0.5, 0.5, 0, 0, 0, 1, 0, 1, -0, -1, 0, 0)
			},
			leftShoulder = {
				Parent = R6parts.torso,
				Name = "Left Shoulder",
				Part0 = R6parts.torso,
				Part1 = R6parts.leftArm,
				C0 = CFrame.new(-1, 0.5, 0, 0, 0, -1, 0, 1, 0, 1, 0, 0),
				C1 = CFrame.new(0.5, 0.5, 0, 0, 0, -1, 0, 1, 0, 1, 0, 0)
			},
			rightHip = {
				Parent = R6parts.torso,
				Name = "Right Hip",
				Part0 = R6parts.torso,
				Part1 = R6parts.rightLeg,
				C0 = CFrame.new(1, -1, 0, 0, 0, 1, 0, 1, -0, -1, 0, 0),
				C1 = CFrame.new(0.5, 1, 0, 0, 0, 1, 0, 1, -0, -1, 0, 0)
			},
			leftHip = {
				Parent = R6parts.torso,
				Name = "Left Hip" ,
				Part0 = R6parts.torso,
				Part1 = R6parts.leftLeg,
				C0 = CFrame.new(-1, -1, 0, 0, 0, -1, 0, 1, 0, 1, 0, 0),
				C1 = CFrame.new(-0.5, 1, 0, 0, 0, -1, 0, 1, 0, 1, 0, 0)
			}
		}
		for i, v in pairs(R6joints) do
			local joint = Instance.new("Motor6D")
			for prop, val in pairs(v) do
				joint[prop] = val
			end
			R6joints[i] = joint
		end
		hum1.RigType = Enum.HumanoidRigType.R6
		hum1.HipHeight = 0
	end
end


	local LoadLibrary = game:GetObjects("rbxassetid://8299466510")[1]

	function Align(Part0, Part1, Position, Angle)
	if Part0:FindFirstChild("Attachment") then
		Part0:FindFirstChild("Attachment"):Remove()
	end
    local AlignPosition = Instance.new("AlignPosition",Part0)
    local AlignOrientation = Instance.new("AlignOrientation",Part0)
    
    local Attachment1 = Instance.new("Attachment", Part0)
    local Attachment2 = Instance.new("Attachment", Part1)

    AlignPosition.Attachment0 = Attachment1
    AlignPosition.Attachment1 = Attachment2
    
    AlignOrientation.Attachment0 = Attachment1
    AlignOrientation.Attachment1 = Attachment2
    
    Attachment2.Position = Position or Vector3.new(0,0,0)
    Attachment2.Orientation = Angle or Vector3.new(0,0,0)
    
    AlignOrientation.MaxTorque = math.huge
    AlignOrientation.MaxAngularVelocity = math.huge
    AlignOrientation.PrimaryAxisOnly = false 
    AlignOrientation.Responsiveness = 200
    AlignOrientation.RigidityEnabled = false
    AlignOrientation.ReactionTorqueEnabled = false
    AlignPosition.MaxForce = math.huge
    AlignPosition.MaxVelocity = math.huge
    AlignPosition.ReactionForceEnabled = false
    AlignPosition.Responsiveness = 200
    AlignPosition.ApplyAtCenterOfMass = true
    AlignPosition.RigidityEnabled = true
    game:GetService("RunService").Heartbeat:Connect(function()
        Part0.Velocity = Vector3.new(-29.99,0,0)
    end)
    if Part0.Parent:IsA("Accessory") then
    	Part0:BreakJoints()
    end
end


local function AlignHat(p1,p2,nomesh)
    pcall(function()
    p1:FindFirstChildOfClass("Weld"):Destroy()
    if nomesh then 
        p1:FindFirstChildOfClass("SpecialMesh"):Destroy()
    end
    end)
    --p1.AccessoryWeld:Destroy()
     A1 = Instance.new("Attachment", p1) 
     A2 = Instance.new("Attachment", p2)
     Mover = Instance.new("AlignPosition", p1)
     Mover.RigidityEnabled = false
    Mover.Attachment0 = A1
    Mover.Attachment1 = A2
    Mover.Responsiveness = 200
    Mover.MaxVelocity = math.huge
    Mover.MaxForce = math.huge
     Rotater = Instance.new("AlignOrientation", p1)
     Rotater.RigidityEnabled = false
    Rotater.Attachment0 = A1
    Rotater.Attachment1 = A2
    Rotater.Responsiveness = 200
    Rotater.MaxAngularVelocity = math.huge
    Rotater.MaxTorque = math.huge
end

local function RandomString()
	return game:GetService("HttpService"):GenerateGUID(false)
end
local stopeverything = false
local HipVal = 3
KEYHOLD = false
s = script
Script = script
SCRIPT = script
scrpt = script
Scrpt = script
SCRPT = script
IT = Instance.new
CF = CFrame.new
VT = Vector3.new
RAD = math.rad
C3 = Color3.new
UD2 = UDim2.new
BRICKC = BrickColor.new
ANGLES = CFrame.Angles
EULER = CFrame.fromEulerAnglesXYZ
COS = math.cos
ACOS = math.acos
SIN = math.sin
ASIN = math.asin
SQRT = math.sqrt
ABS = math.abs
MRANDOM = math.random
FLOOR = math.floor
HUGE = math.huge
radian = math.rad
random = math.random
Vec3 = Vector3.new
Inst = Instance.new
cFrame = CFrame.new
Euler = CFrame.fromEulerAnglesXYZ
vt = Vector3.new
bc = BrickColor.new
br = BrickColor.random
it = Instance.new
angles = CFrame.Angles
Cf = CFrame.new
Cos = math.cos
Sin = math.sin
Abs = math.abs
Rad = math.rad

local lplr = game:GetService("Players").LocalPlayer
local Player = lplr
local PLAYER = Player
local sine = 0
local NeckSnap = false
local USERNAME = lplr.Name
local Player = game:GetService("Players").LocalPlayer
local USERID = lplr.UserId
local taunt = {Value = "None"}
local songid = {Value = "rbxassetid://6174456295"}
local attack = false
local walkspeed = 50
local TauntRemote = {}
local SongSync = {Value = 0}
local ISFLYING = false
local antivoid = nil
local shade = Color3.fromRGB(0,0,0)

local Character = game.Players.LocalPlayer.Character
local Mouse,mouse,MOUSE,m,M = lplr:GetMouse(),lplr:GetMouse(),lplr:GetMouse(),lplr:GetMouse(),lplr:GetMouse()

local S = 1
local eeeblock = Instance.new("Part")
local Humanoid = Character.Humanoid
Humanoid.Animator:Destroy()
Humanoid.HipHeight = HipVal
local LeftArm = Character["Left Arm"]
local RightArm = Character["Right Arm"]
local LeftLeg = Character["Left Leg"]
local RightLeg = Character["Right Leg"]
local Head = Character.Head
local Torso = Character.Torso
local RootPart = Character.HumanoidRootPart
local RootJoint = RootPart.RootJoint
local Neck = Torso["Neck"]
local RightShoulder = Torso["Right Shoulder"]
local LeftShoulder = Torso["Left Shoulder"]
local RightHip = Torso["Right Hip"]
local LeftHip = Torso["Left Hip"]
local Effects = nil
local Eyes = nil
local Replica = game:GetObjects("rbxassetid://7921736307")[1]
local GUN = Replica.MegaGunnModel

GUN.Parent = Character
local GunJoint = GUN.Joint.Weld
GUN.Joint.Weld.Part0 = RightArm


	Railgun = workspace[game.Players.LocalPlayer.Name]["Starslayer Railgun"].Handle
	AlignHat(Railgun,GUN.Joint,false)
Railgun.Attachment.CFrame = CFrame.new(-1, -0, -0, -4.37113989e-08, 0.642787635, -0.766044438, 0, 0.766044438, 0.642787635, 1, 2.80971459e-08, -3.34848735e-08)
local Hole = GUN.Hole
local Holetwo = GUN.Hole2
local shade = Character["Torso"].Color
local alreadyfixing = false
local Effects = Instance.new("Folder")
Effects.Parent = Character
local eeeblock = Instance.new("Part")
eeeblock.Name = "yes"
eeeblock.CanCollide = false
eeeblock.Transparency = 1
eeeblock.CFrame = Torso.CFrame
eeeblock.Parent = Character
local eee = Instance.new("Sound",eeeblock)
eee.Volume = 1
eee.Pitch = 1
eee.SoundId = songid.Value
eee:Play()
eee.Name = "yes"
eee.Looped = true
eee.TimePosition = SongSync.Value
eee.DescendantAdded:Connect(function(v)
	if stopeverything then wait(math.huge) end
	if v:IsA("SoundEffect") then
		v.Enabled = false
		v:GetPropertyChangedSignal("Enabled"):Connect(function()
			if stopeverything then wait(math.huge) end
			if v.Enabled ~= false then
				v.Enabled = false
			end
		end)
	end
	game:GetService("Debris"):AddItem(v,.01)
end)
function TauntRemote:FireServer(Name, ID)
	taunt.Value = Name
	if songid.Value ~= "rbxassetid://"..ID then
		songid.Value = "rbxassetid://"..ID
		SongSync.Value = 0
		eee.Volume = 1
		eee.Pitch = 1
		eee.SoundId = songid.Value
		eee.TimePosition = SongSync.Value
	end
end


function chatfunc(textt,glitchy)
	local text = string.gsub(textt,"​","")
	local chat = coroutine.wrap(function()
		local oldthing = eeeblock:FindFirstChild("TalkingBillBoard")
		if oldthing then
			oldthing:Destroy()
		end
		local sayingstuff = Instance.new("BillboardGui",eeeblock)
		sayingstuff.Size = UDim2.new(0,9999,2,0)
		sayingstuff.StudsOffset = Vector3.new(0,5,0)
		sayingstuff.Adornee = eeeblock
		sayingstuff.Name = "TalkingBillBoard"
		local sayingstuff2 = Instance.new("TextLabel",sayingstuff)
		sayingstuff2.BackgroundTransparency = 1
		sayingstuff2.BorderSizePixel = 0
		sayingstuff2.Text = ""
		sayingstuff2.Font = "Arcade"
		sayingstuff2.TextScaled = true
		sayingstuff2.TextStrokeTransparency = 0
		coroutine.resume(coroutine.create(function()
			while not stopeverything and sayingstuff2:IsDescendantOf(game) do
				local hBRUH,sBRUH,vBRUH = Color3.toHSV(GUN.NeonParts.Color)
				sayingstuff2.TextColor3 = Color3.fromHSV(hBRUH,sBRUH,vBRUH/2)
				swait()
			end
		end))
		sayingstuff2.TextStrokeColor3 = shade
		sayingstuff2.Size = UDim2.new(1,0,1,0)
		local sayingstuff3 = Instance.new("TextLabel",sayingstuff)
		sayingstuff3.BackgroundTransparency = 1
		sayingstuff3.BorderSizePixel = 0
		sayingstuff3.Text = ""
		sayingstuff3.Font = "Arcade"
		sayingstuff3.TextScaled = true
		sayingstuff3.TextStrokeTransparency = 0
		coroutine.resume(coroutine.create(function()
			while not stopeverything and sayingstuff3:IsDescendantOf(game) do
				sayingstuff3.TextColor3 = GUN.NeonParts.Color
				swait()
			end
		end))
		sayingstuff3.TextStrokeColor3 = shade
		sayingstuff3.Size = UDim2.new(1,0,1,0)
		coroutine.resume(coroutine.create(function()
			while not stopeverything and sayingstuff ~= nil do
				swait()
				if glitchy then
					local fonts = {"Antique","Arcade","Arial","ArialBold","Bodoni","Cartoon","Code","Fantasy","Garamond","Gotham","GothamBlack","GothamBold","GothamSemibold","Highway","SciFi","SourceSans","SourceSansBold","SourceSansItalic","SourceSansLight","SourceSansSemibold"}
					local randomfont = fonts[math.random(1,#fonts)]
					sayingstuff2.Font = randomfont
					sayingstuff3.Font = randomfont
				end
				sayingstuff2.Position = UDim2.new(0,math.random(-3,3),0,math.random(-3,3)) 
				sayingstuff3.Position = UDim2.new(0,math.random(-3,3),0,math.random(-3,3)) 
				sayingstuff3.Rotation = math.random(-1,1)	
				sayingstuff2.Rotation = math.random(-1,1)
			end
		end))
		for i = 1,string.len(text) do
			swait(2)
			sayingstuff2.Text = string.sub(text,1,i)
			sayingstuff3.Text = string.sub(text,1,i)
		end
		swait(120)
		for i = 1,50 do
			swait()
			sayingstuff2.TextStrokeTransparency = i/50
			sayingstuff2.TextTransparency = sayingstuff2.TextStrokeTransparency
			sayingstuff3.TextStrokeTransparency = sayingstuff2.TextStrokeTransparency
			sayingstuff3.TextTransparency = sayingstuff2.TextStrokeTransparency
		end
		sayingstuff:Destroy()
	end)
	chat()
end

function onChatted(msg)
	chatfunc(msg)
end
Player.Chatted:connect(onChatted)

local ROOTC0 = CFrame.new(0,0,0) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(180))
local NECKC0 = CFrame.new(0,1,0) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(180))
local RIGHTSHOULDERC0 = CFrame.new(-0.5,0,0) * CFrame.Angles(math.rad(0),math.rad(90),math.rad(0))
local LEFTSHOULDERC0 = CFrame.new(0.5,0,0) * CFrame.Angles(math.rad(0),math.rad(-90),math.rad(0))
local BG = nil
local BV = nil
local soundfixing = false
local fixinggui = false
local gui = nil
local exitbutton = nil
local restartingscript = false
local TS = game:GetService("TweenService")
local PS = game:GetService("PhysicsService")
local Anim = "Idle"
local attacktype = 1
local delays = false
local play = true
local Torsovelocity = (RootPart.Velocity * Vector3.new(1,0,1)).Magnitude 
local doe = 0
Humanoid.WalkSpeed = walkspeed
local rc0 = CFrame.new() * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(180))
local nc0 = CFrame.new(0,1,0) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(180))
local rscp = CFrame.new(-.5,0,0) * CFrame.Angles(math.rad(0),math.rad(90),math.rad(0))
local lscp = CFrame.new(.5,0,0) * CFrame.Angles(math.rad(0),math.rad(-90),math.rad(0))
function QFCF(cf)
	local mx,my,mz,m00,m01,m02,m10,m11,m12,m20,m21,m22 = cf:components()
	local trace = m00 + m11 + m22
	if trace > 0 then 
		local s = math.sqrt(1 + trace)
		local recip = 0.5/s
		return (m21 - m12) * recip,(m02 - m20) * recip,(m10 - m01) * recip,s * 0.5
	else
		local i = 0
		if m11 > m00 then
			i = 1
		end
		if m22 > (i == 0 and m00 or m11) then
			i = 2
		end
		if i == 0 then
			local s = math.sqrt(m00 - m11 - m22 + 1)
			local recip = 0.5/s
			return 0.5 * s,(m10 + m01) * recip,(m20 + m02) * recip,(m21 - m12) * recip
		elseif i == 1 then
			local s = math.sqrt(m11 - m22 - m00 + 1)
			local recip = 0.5/s
			return (m01 + m10) * recip,0.5 * s,(m21 + m12) * recip,(m02 - m20) * recip
		elseif i == 2 then
			local s = math.sqrt(m22 - m00 - m11 + 1)
			local recip = 0.5/s return (m02 + m20) * recip,(m12 + m21) * recip,0.5 * s,(m10 - m01) * recip
		end
	end
end

function QTCF(px,py,pz,x,y,z,w)
	local xs,ys,zs = x + x,y + y,z + z
	local wx,wy,wz = w * xs,w * ys,w * zs
	local xx = x * xs
	local xy = x * ys
	local xz = x * zs
	local yy = y * ys
	local yz = y * zs
	local zz = z * zs
	return CFrame.new(px,py,pz,1 - (yy + zz),xy - wz,xz + wy,xy + wz,1 - (xx + zz),yz - wx,xz - wy,yz + wx,1 - (xx + yy))
end
function QS(a,b,t)
	local cosTheta = a[1] * b[1] + a[2] * b[2] + a[3] * b[3] + a[4] * b[4]
	local startInterp,finishInterp;
	if cosTheta >= 0.0001 then
		if (1 - cosTheta) > 0.0001 then
			local theta = math.acos(cosTheta)
			local invSinTheta = 1/math.sin(theta)
			startInterp = math.sin((1 - t) * theta) * invSinTheta
			finishInterp = math.sin(t * theta) * invSinTheta
		else
			startInterp = 1 - t
			finishInterp = t
		end
	else
		if (1 + cosTheta) > 0.0001 then
			local theta = math.acos(-cosTheta)
			local invSinTheta = 1/math.sin(theta)
			startInterp = math.sin((t - 1) * theta) * invSinTheta
			finishInterp = math.sin(t * theta) * invSinTheta
		else
			startInterp = t - 1
			finishInterp = t
		end
	end
	return a[1] * startInterp + b[1] * finishInterp,a[2] * startInterp + b[2] * finishInterp,a[3] * startInterp + b[3] * finishInterp,a[4] * startInterp + b[4] * finishInterp
end

function Clerp(a,b,t)
	local qa = {QFCF(a)}
	local qb = {QFCF(b)}
	local ax,ay,az = a.x,a.y,a.z
	local bx,by,bz = b.x,b.y,b.z
	local _t = 1 - t
	return QTCF(_t * ax + t * bx,_t * ay + t * by,_t * az + t * bz,QS(qa,qb,t))
end


ArtificialHB = Instance.new("BindableEvent",script)
ArtificialHB.Name = "Heartbeat"

script:WaitForChild("Heartbeat")

frame = 1 / 60
tf = 0
allowframeloss = false
tossremainder = false
lastframe = tick()
script.Heartbeat:Fire()

game:GetService("RunService").Heartbeat:Connect(function(s,p)
	tf = tf + s
	if tf >= frame then
		if allowframeloss then
			script.Heartbeat:Fire()
			lastframe = tick()
		else
			for i = 1,math.floor(tf / frame) do
				script.Heartbeat:Fire()
			end
			lastframe = tick()
		end
		if tossremainder then
			tf = 0
		else
			tf = tf - frame * math.floor(tf / frame)
		end
	end
end)

function swait(num)
	if num == 0 or num == nil then
		ArtificialHB.Event:Wait()
	else
		for i = 0,num do
			ArtificialHB.Event:Wait()
		end
	end
end
function Swait(num)
	if num == 0 or num == nil then
		ArtificialHB.Event:Wait()
	else
		for i = 0,num do
			ArtificialHB.Event:Wait()
		end
	end
end

SWAIT = Swait


function mdmg(pos, range) end
if true then --added so it doesnt change other variables from the script in case i used same names
    local hrp = gp(c, "HumanoidRootPart", "BasePart") -- "gp" is the function i used in my reanimate i hope its not changed
    local hrp1 = gp(model, "HumanoidRootPart", "BasePart")
    local att0 = gp(hrp, "att1_HumanoidRootPart", "Attachment")
	or gp(gp(hrp, "R15_HumanoidRootPart", "BasePart"), "att1_HumanoidRootPart", "Attachment")
    if hrp and hrp1 and att0 then
        hrp1.Transparency = 0.5
        local flingpart = Instance.new("Part", workspace)
        flingpart.Anchored = true
        flingpart.Transparency = 1
        flingpart.CanCollide = false
        flingpart.Size = Vector3.new(0.1, 0.1, 0.1)
        flingpart.Name = "flingpart"
        for i, v in pairs(hrp1:GetDescendants()) do
            if v and v.Parent and v:IsA("AlignOrientation") then
                v.Enabled = false
            end
        end
        local flingpos = false
        spawn(function()
            while stepped:Wait() and hrp and hrp.Parent and att0 and att0.Parent and hrp1 and hrp1.Parent and flingpart and flingpart.Parent do
                hrp1.RotVelocity = FLINGROT
                if flingpos then
                    att0.Parent = flingpart
                    flingpart.Position = flingpos
                else
                    att0.Parent = hrp
                end
            end
        end)
        mdmg = function(position, range)
            print("mdmg")
            for i, v in pairs(workspace:GetDescendants()) do
                if v and v.Parent and v:IsA("Model") and v:FindFirstChildOfClass("Humanoid") and (not v:IsDescendantOf(c)) then
                    local parts = v:GetChildren()
                    for i1, v1 in pairs(parts) do
                        if v1 and v1.Parent and v1:IsA("BasePart") then
                            if (position - v1.Position).Magnitude < range then
                                local flingpos1 = v1.Position
                                flingpos = flingpos1
                                spawn(function()
                                    while stepped:Wait() and (flingpos == flingpos1) do
                                        if v1 and v1.Parent then
                                            flingpos1 = v1.Position
                                            flingpos = flingpos1
                                        end
                                    end
                                end)
                                spawn(function()
                                    wait(1)
                                    if flingpos == flingpos1 then
                                        flingpos = false
                                    end
                                end)
                            end
                        end
                    end
                end
            end
        end
    else
        print("failed to make fling damage")
    end
end

function CreateConnection(TYPE,PARENT,PART0,PART1,C0,C1)
	if stopeverything then wait(math.huge) end
	local NEWWELD = Instance.new(TYPE)
	NEWWELD.Part0 = PART0
	NEWWELD.Part1 = PART1
	NEWWELD.C0 = C0
	NEWWELD.C1 = C1
	NEWWELD.Parent = PARENT
	return NEWWELD
end	

function CreateMesh(MESH,PARENT,MESHTYPE,MESHID,TEXTUREID,SCALE,OFFSET)
	local NEWMESH = Instance.new(MESH)
	if MESH == "SpecialMesh" then
		NEWMESH.MeshType = MESHTYPE
		if MESHID ~= "nil" and MESHID ~= "" and tonumber(MESHID) ~= nil then
			NEWMESH.MeshId = "rbxassetid://"..MESHID
		elseif MESHID ~= "nil" and MESHID ~= "" then
			NEWMESH.MeshId = MESHID
		end
		if TEXTUREID ~= "nil" and TEXTUREID ~= "" then
			NEWMESH.TextureId = "rbxassetid://"..TEXTUREID
		end
	end
	NEWMESH.Offset = OFFSET or Vector3.new()
	NEWMESH.Scale = SCALE
	NEWMESH.Parent = PARENT
	return NEWMESH
end

function CreatePart(FORMFACTOR,PARENT,MATERIAL,REFLECTANCE,TRANSPARENCY,BRICKCOLOR,NAME,SIZE,ANCHOR)
	local NEWPART = Instance.new("Part")
	NEWPART.Massless = true
	NEWPART.formFactor = FORMFACTOR
	NEWPART.Reflectance = REFLECTANCE
	NEWPART.Transparency = TRANSPARENCY
	NEWPART.CanCollide = false
	NEWPART.Locked = true
	NEWPART.Anchored = true
	if ANCHOR == false then
		NEWPART.Anchored = false
	end
	NEWPART.Color = BRICKCOLOR
	NEWPART.Name =  RandomString()

	NEWPART.Size = SIZE
	NEWPART.Position = Torso.Position
	NEWPART.Material = MATERIAL
	NEWPART:BreakJoints()
	NEWPART.Parent = PARENT
	return NEWPART
end

local S = Instance.new("Sound")
function CreateSound(ID,PARENT,VOLUME,PITCH,DOESLOOP)
	local NEWSOUND = nil
	coroutine.resume(coroutine.create(function()
		NEWSOUND = S:Clone()
		NEWSOUND.Parent = PARENT
		NEWSOUND.Volume = VOLUME
		NEWSOUND.Pitch = PITCH
		NEWSOUND.SoundId = "rbxassetid://"..ID
		NEWSOUND:play()
		if DOESLOOP == true then
			NEWSOUND.Looped = true
		else
			coroutine.resume(coroutine.create(function()
				pcall(function()
					repeat if stopeverything then wait(math.huge) end Swait() until NEWSOUND.Playing == false
					NEWSOUND:Destroy()
				end)
			end))
		end
	end))
	return NEWSOUND
end

local function weldBetween(a,b)
	local weldd = Instance.new("Weld")
	weldd.Part0 = a
	weldd.Part1 = b
	weldd.C1 = b.CFrame:inverse() * a.CFrame
	weldd.Parent = b
	return weldd
end
function rayCast(Position,Direction,Range,Ignore)
	return workspace:FindPartOnRay(Ray.new(Position,Direction.unit * (Range or 999.999)),Ignore) 
end 		


function Effect(Table)
	local TYPE = (Table.EffectType or "Sphere")
	local SIZE = (Table.Size or Vector3.new(1,1,1))
	local ENDSIZE = (Table.Size2 or Vector3.new())
	local TRANSPARENCY = (Table.Transparency or 0)
	local ENDTRANSPARENCY = (Table.Transparency2 or 1)
	local CFRAME = (Table.CFrame or Torso.CFrame)
	local MOVEDIRECTION = (Table.MoveToPos or nil)
	local ROTATION1 = (Table.RotationX or 0)
	local ROTATION2 = (Table.RotationY or 0)
	local ROTATION3 = (Table.RotationZ or 0)
	local MATERIAL = (Table.Material or "Neon")
	local COLOR = (Table.Color or shade)
	local hOK,sOK,vOK = Color3.toHSV(COLOR)
	local RAINBOWPART = false
	if sOK > .1 then
		RAINBOWPART = true
	end
	local TIME = (Table.Time or 45)
	local SOUNDID = (Table.SoundID or nil)
	local SOUNDPITCH = (Table.SoundPitch or nil)
	local SOUNDVOLUME = (Table.SoundVolume or nil)
	local USEBOOMERANGMATH = (Table.UseBoomerangMath or false)
	local BOOMERANG = (Table.Boomerang or 0)
	local SIZEBOOMERANG = (Table.SizeBoomerang or 0)
	coroutine.resume(coroutine.create(function()
		local PLAYSSOUND = false
		local SOUND = nil
		local EFFECT = CreatePart(3,Effects,MATERIAL,0,TRANSPARENCY,shade,"Effect",Vector3.new(1,1,1),true)
		if RAINBOWPART then
			coroutine.resume(coroutine.create(function()
				while not stopeverything and EFFECT:IsDescendantOf(game) do
					EFFECT.Color = GUN.NeonParts.Color
					swait()
				end
			end))
		end
		if SOUNDID ~= nil and SOUNDPITCH ~= nil and SOUNDVOLUME ~= nil then
			PLAYSSOUND = true
			SOUND = CreateSound(SOUNDID,EFFECT,SOUNDVOLUME,SOUNDPITCH,false)
		end
		EFFECT.Color = COLOR
		local MSH = nil
		if TYPE == "Sphere" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"Sphere","","",SIZE,Vector3.new())
		elseif TYPE == "Block" or TYPE == "Box" then
			MSH = Instance.new("BlockMesh",EFFECT)
			MSH.Scale = SIZE
		elseif TYPE == "Wave" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","20329976","",SIZE,Vector3.new(0,0,-SIZE.X/8))
		elseif TYPE == "Ring" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","559831844","",Vector3.new(SIZE.X,SIZE.X,0.1),Vector3.new())
		elseif TYPE == "Slash" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","662586858","",Vector3.new(SIZE.X/10,0,SIZE.X/10),Vector3.new())
		elseif TYPE == "Round Slash" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","662585058","",Vector3.new(SIZE.X/10,0,SIZE.X/10),Vector3.new())
		elseif TYPE == "Swirl" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","168892432","",SIZE,Vector3.new())
		elseif TYPE == "Skull" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","4770583","",SIZE,Vector3.new())
		elseif TYPE == "Crystal" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","9756362","",SIZE,Vector3.new())
		end
		if MSH ~= nil then
			local BOOMR1 = 1+BOOMERANG/50
			local BOOMR2 = 1+SIZEBOOMERANG/50
			local MOVESPEED = nil
			if MOVEDIRECTION ~= nil then
				if USEBOOMERANGMATH == true then
					MOVESPEED = ((CFRAME.p - MOVEDIRECTION).Magnitude/TIME)*BOOMR1
				else
					MOVESPEED = ((CFRAME.p - MOVEDIRECTION).Magnitude/TIME)
				end
			end
			local GROWTH = nil
			if USEBOOMERANGMATH == true then
				GROWTH = (SIZE - ENDSIZE)*(BOOMR2+1)
			else
				GROWTH = (SIZE - ENDSIZE)
			end
			local TRANS = TRANSPARENCY - ENDTRANSPARENCY
			if TYPE == "Block" then
				EFFECT.CFrame = CFRAME*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360)))
			else
				EFFECT.CFrame = CFRAME
			end
			if USEBOOMERANGMATH == true then
				for LOOP = 1,TIME+1 do
					swait()
					MSH.Scale = MSH.Scale - (Vector3.new((GROWTH.X)*((1 - (LOOP/TIME)*BOOMR2)),(GROWTH.Y)*((1 - (LOOP/TIME)*BOOMR2)),(GROWTH.Z)*((1 - (LOOP/TIME)*BOOMR2)))*BOOMR2)/TIME
					if TYPE == "Wave" then
						MSH.Offset = Vector3.new(0,0,-MSH.Scale.Z/8)
					end
					EFFECT.Transparency = EFFECT.Transparency - TRANS/TIME
					if TYPE == "Block" then
						EFFECT.CFrame = CFRAME*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360)))
					else
						EFFECT.CFrame = EFFECT.CFrame*CFrame.Angles(math.rad(ROTATION1),math.rad(ROTATION2),math.rad(ROTATION3))
					end
					if MOVEDIRECTION ~= nil then
						local ORI = EFFECT.Orientation
						EFFECT.CFrame = CFrame.new(EFFECT.Position,MOVEDIRECTION)*CFrame.new(0,0,-(MOVESPEED)*((1 - (LOOP/TIME)*BOOMR1)))
						EFFECT.Orientation = ORI
					end
				end
			else
				for LOOP = 1,TIME+1 do
					swait()
					MSH.Scale = MSH.Scale - GROWTH/TIME
					if TYPE == "Wave" then
						MSH.Offset = Vector3.new(0,0,-MSH.Scale.Z/8)
					end
					EFFECT.Transparency = EFFECT.Transparency - TRANS/TIME
					if TYPE == "Block" then
						EFFECT.CFrame = CFRAME*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360)))
					else
						EFFECT.CFrame = EFFECT.CFrame*CFrame.Angles(math.rad(ROTATION1),math.rad(ROTATION2),math.rad(ROTATION3))
					end
					if MOVEDIRECTION ~= nil then
						local ORI = EFFECT.Orientation
						EFFECT.CFrame = CFrame.new(EFFECT.Position,MOVEDIRECTION)*CFrame.new(0,0,-MOVESPEED)
						EFFECT.Orientation = ORI
					end
				end
			end
			EFFECT.Transparency = 1
			if PLAYSSOUND == false then
				EFFECT:Destroy()
			else
				repeat if stopeverything then wait(math.huge) end swait() until EFFECT:FindFirstChildOfClass("Sound") == nil
				EFFECT:Destroy()
			end
		else
			if PLAYSSOUND == false then
				EFFECT:Destroy()
			else
				repeat if stopeverything then wait(math.huge) end swait() until EFFECT:FindFirstChildOfClass("Sound") == nil
				EFFECT:Destroy()
			end
		end
	end))
end

if _G.Night == Bool then
HUGE = math.huge
local lit = game:GetService("Lighting")
function checksky(v)
	if v:IsA("BloomEffect") then
		return
	end
	if v:IsA("PostEffect") or v:IsA("Sky") or v:IsA("Atmosphere") then
		game:GetService("Debris"):AddItem(v,.01)
	end
end
for i,v in pairs(lit:GetDescendants()) do
	checksky(v)
end
lit.DescendantAdded:Connect(function(v)
	if stopeverything then wait(HUGE) end
	checksky(v)
end)
Bloom = Instance.new("BloomEffect",game:GetService("Lighting"))
VISUALS = game:GetService("Lighting")
VISUALSSz = game:GetService("Lighting")
local bswcrlightingeffect = Instance.new("BoolValue")
bswcrlightingeffect.Name = "BSWCRLightingEffect"
bswcrlightingeffect.Value = false

pcall(function()
	VISUALS.ClockTime = 6
	Bloom.Intensity = 0 + sick.PlaybackLoudness/500
	VISUALSSz.ExposureCompensation = math.clamp((0 + sick.PlaybackLoudness/125),0,5)
	VISUALSSz.FogEnd = math.clamp(sick.PlaybackLoudness,50,1000)
	VISUALSSz.Brightness = 0
	VISUALS.EnvironmentDiffuseScale = 0 + sick.PlaybackLoudness/100
	if dienerd ~= true then
		lit.Ambient = Color3.new(1,1,1)
		lit.Brightness = 1
		lit.ColorShift_Bottom = Color3.new()
		lit.ColorShift_Top = Color3.new()
		lit.EnvironmentDiffuseScale = 0
		lit.EnvironmentSpecularScale = 0
		lit.GlobalShadows = true
		lit.OutdoorAmbient = Color3.new(.5,.5,.5)
		lit.ClockTime = 6
		lit.GeographicLatitude = 41.733
		lit.ExposureCompensation = 0
		lit.FogColor = Color3.fromRGB(192,192,192)
		lit.FogEnd = 100000
	end
end)
end



function EFFECT1(bonuspeed,FastSpeed,type,pos,x1,y1,z1,value,color,outerpos)
	local type = type
	local rng = Instance.new("Part",Effects)
	rng.Anchored = true
	rng.Color = GUN.NeonParts.Color
	rng.CanCollide = false
	rng.FormFactor = 3
	rng.Name = "Ring"
	rng.Material = "Neon"
	rng.Size = Vector3.new(1,1,1)
	rng.Transparency = 0
	rng.TopSurface = 0
	rng.BottomSurface = 0
	rng.CFrame = pos
	rng.CFrame = rng.CFrame + rng.CFrame.lookVector*outerpos
	local rngm = Instance.new("SpecialMesh",rng)
	rngm.MeshType = "Brick"
	rngm.Scale = Vector3.new(x1,y1,z1)
	local scaler2 = 1
	local speeder = FastSpeed/10
	if type == "Add" then
		scaler2 = 1*value
	elseif type == "Divide" then
		scaler2 = 1/value
	end
	coroutine.resume(coroutine.create(function()
		for i = 0,10/bonuspeed,.1 do
			swait()
			if type == "Add" then
				scaler2 = scaler2 - .01*value/bonuspeed
			elseif type == "Divide" then
				scaler2 = scaler2 - .01/value*bonuspeed
			end
			rng.Color = GUN.NeonParts.Color
			speeder = speeder - .01*FastSpeed*bonuspeed/10
			rng.CFrame = rng.CFrame + rng.CFrame.lookVector*speeder*bonuspeed
			rng.Transparency = rng.Transparency + .01*bonuspeed
			rngm.Scale = rngm.Scale - Vector3.new(scaler2*bonuspeed,scaler2*bonuspeed,scaler2*bonuspeed)
		end
		rng:Destroy()
	end))
end



function Lightning(Part0,Part1,Timess,Offset,Color,Timer,sSize,eSize,Trans,Boomer,sBoomer,Trans2)
  local magz = (Part0 - Part1).Magnitude
	local Times = math.floor(math.clamp(magz/10,1,20))
  local curpos = Part0
  local trz = {
    -Offset,
    Offset
  }
  for i = 1,Times do
    local li = Instance.new("Part",Effects)
    li.Name = RandomString()
    li.TopSurface = 0
    li.Material = "Neon"
    li.BottomSurface = 0
    li.Anchored = true
    li.Locked = true
    li.Transparency = 0
    li.Color = Color
    li.formFactor = "Custom"
    li.CanCollide = false
    li.Size = Vector3.new(0.1,0.1,magz/Times)
    local Offzet = Vector3.new(trz[math.random(1,2)],trz[math.random(1,2)],trz[math.random(1,2)])
    local trolpos = CFrame.new(curpos,Part1) * CFrame.new(0,0,magz/Times).p + Offzet
    if Times == i then
      local magz2 = (curpos - Part1).Magnitude
      li.Size = Vector3.new(0.1,0.1,magz2)
      li.CFrame = CFrame.new(curpos,Part1) * CFrame.new(0,0,-magz2/2)
    else
      li.CFrame = CFrame.new(curpos,trolpos) * CFrame.new(0,0,magz/Times/2)
    end
    curpos = li.CFrame * CFrame.new(0,0,magz/Times/2).p
    li:Destroy()
	Effect({Time = Timer,EffectType = "Box",Size = Vector3.new(sSize,sSize,li.Size.Z),Size2 = Vector3.new(eSize,eSize,li.Size.Z),Transparency = Trans,Transparency2 = Trans2 or 1,CFrame = li.CFrame,MoveToPos = nil,RotationX = nil,RotationY = nil,RotationZ = nil,Material = "Neon",Color = li.Color,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = Boomer,Boomerang = 0,SizeBoomerang = sBoomer})
  end
end

function FireArc(Part,ToLocation,AmountOfTime,Height,DoesCourontine)
    if DoesCourontine == false then
        local Direction = CFrame.new(Part.Position,ToLocation)
        local Distance = (Part.Position - ToLocation).Magnitude
        for i = 1,AmountOfTime do
            swait()
            Part.CFrame = Direction*CFrame.new(0,(AmountOfTime/200)+((AmountOfTime/Height)-((i*2)/Height)),-Distance/AmountOfTime)
            Direction = Part.CFrame
        end
    elseif DoesCourontine == true then
        coroutine.resume(coroutine.create(function()
            local Direction = CFrame.new(Part.Position,ToLocation)
            local Distance = (Part.Position - ToLocation).Magnitude
            for i = 1,AmountOfTime do
                swait()
                Part.CFrame = Direction*CFrame.new(0,(AmountOfTime/200)+((AmountOfTime/Height)-((i*2)/Height)),-Distance/AmountOfTime)
                Direction = Part.CFrame
            end
        end))
    end
end

function MakeForm(PART,TYPE)
	if TYPE == "Cyl" then
		local MSH = Instance.new("CylinderMesh",PART)
	elseif TYPE == "Ball" then
		local MSH = Instance.new("SpecialMesh",PART)
		MSH.MeshType = "Sphere"
	elseif TYPE == "Wedge" then
		local MSH = Instance.new("SpecialMesh",PART)
		MSH.MeshType = "Wedge"
	end
end
function MakeForm(PART,TYPE)
	if TYPE == "Cyl" then
		local MSH = Instance.new("CylinderMesh",PART)
	elseif TYPE == "Ball" then
		local MSH = Instance.new("SpecialMesh",PART)
		MSH.MeshType = "Sphere"
	elseif TYPE == "Wedge" then
		local MSH = Instance.new("SpecialMesh",PART)
		MSH.MeshType = "Wedge"
	end
end

function AttackGyro()
	local GYRO = Instance.new("BodyGyro",RootPart)
	GYRO.D = 25
	GYRO.P = 20000
	GYRO.MaxTorque = Vector3.new(0,4000000,0)
	GYRO.CFrame = CFrame.new(RootPart.Position,Mouse.Hit.p)
	coroutine.resume(coroutine.create(function()
		repeat if stopeverything then wait(math.huge) end
			swait()
			GYRO.CFrame = CFrame.new(RootPart.Position,Mouse.Hit.p)
		until attack == false
		GYRO:Destroy()
	end))
end

function WACKYEFFECT(Table)
	local TYPE = (Table.EffectType or "Sphere")
	local SIZE = (Table.Size or Vector3.new(1,1,1))
	local ENDSIZE = (Table.Size2 or Vector3.new(0,0,0))
	local TRANSPARENCY = (Table.Transparency or 0)
	local ENDTRANSPARENCY = (Table.Transparency2 or 1)
	local CFRAME = (Table.CFrame or Torso.CFrame)
	local MOVEDIRECTION = (Table.MoveToPos or nil)
	local ROTATION1 = (Table.RotationX or 0)
	local ROTATION2 = (Table.RotationY or 0)
	local ROTATION3 = (Table.RotationZ or 0)
	local MATERIAL = (Table.Material or "Neon")
	local COLOR = (Table.Color or shade)
	local hOK,sOK,vOK = Color3.toHSV(COLOR)
	local RAINBOWPART = false
	if sOK > .1 then
		RAINBOWPART = true
	end
	local TIME = (Table.Time or 45)
	local SOUNDID = (Table.SoundID or nil)
	local SOUNDPITCH = (Table.SoundPitch or nil)
	local SOUNDVOLUME = (Table.SoundVolume or nil)
	coroutine.resume(coroutine.create(function()
		local PLAYSSOUND = false
		local SOUND = nil
		local EFFECT = CreatePart(3,Effects,MATERIAL,0,TRANSPARENCY,shade,"Effect",Vector3.new(1,1,1),true)
		if SOUNDID ~= nil and SOUNDPITCH ~= nil and SOUNDVOLUME ~= nil then
			PLAYSSOUND = true
			SOUND = CreateSound(SOUNDID,EFFECT,SOUNDVOLUME,SOUNDPITCH,false)
		end
		EFFECT.Color = COLOR
		if RAINBOWPART then
			coroutine.resume(coroutine.create(function()
				while not stopeverything and EFFECT:IsDescendantOf(game) do
					EFFECT.Color = GUN.NeonParts.Color
					swait()
				end
			end))
		end
		local MSH = nil
		if TYPE == "Sphere" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"Sphere","","",SIZE,Vector3.new(0,0,0))
		elseif TYPE == "Block" then
			MSH = Instance.new("BlockMesh",EFFECT)
			MSH.Scale = Vector3.new(SIZE.X,SIZE.Y,SIZE.Z)
		elseif TYPE == "Wave" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","20329976","",SIZE,Vector3.new(0,0,-SIZE.X/8))
		elseif TYPE == "Ring" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","559831844","",Vector3.new(SIZE.X,SIZE.X,0.1),Vector3.new(0,0,0))
		elseif TYPE == "Slash" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","662586858","",Vector3.new(SIZE.X/10,0,SIZE.X/10),Vector3.new(0,0,0))
		elseif TYPE == "Round Slash" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","662585058","",Vector3.new(SIZE.X/10,0,SIZE.X/10),Vector3.new(0,0,0))
		elseif TYPE == "Swirl" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","1051557","",SIZE,Vector3.new(0,0,0))
		elseif TYPE == "Skull" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","4770583","",SIZE,Vector3.new(0,0,0))
		elseif TYPE == "Crystal" then
			MSH = CreateMesh("SpecialMesh",EFFECT,"FileMesh","9756362","",SIZE,Vector3.new(0,0,0))
		end
		if MSH ~= nil then
			local MOVESPEED = nil
			if MOVEDIRECTION ~= nil then
				MOVESPEED = (CFRAME.p - MOVEDIRECTION).Magnitude/TIME
			end
			local GROWTH = SIZE - ENDSIZE
			local TRANS = TRANSPARENCY - ENDTRANSPARENCY
			EFFECT.CFrame = CFRAME
			for LOOP = 1,TIME+1 do
				swait()
				MSH.Scale = MSH.Scale - GROWTH/TIME
				if TYPE == "Wave" then
					MSH.Offset = Vector3.new(0,0,-MSH.Scale.X/8)
				end
				EFFECT.Transparency = EFFECT.Transparency - TRANS/TIME
				EFFECT.CFrame = EFFECT.CFrame*CFrame.Angles(math.rad(ROTATION1),math.rad(ROTATION2),math.rad(ROTATION3))
				if MOVEDIRECTION ~= nil then
					local ORI = EFFECT.Orientation
					EFFECT.CFrame = CFrame.new(EFFECT.Position,MOVEDIRECTION)*CFrame.new(0,0,-MOVESPEED)
					EFFECT.Orientation = ORI
				end
			end
			if PLAYSSOUND == false then
				EFFECT:remove()
			else
				repeat if stopeverything then wait(math.huge) end swait() until SOUND.Playing == false
				EFFECT:remove()
			end
		else
			if PLAYSSOUND == false then
				EFFECT:remove()
			else
				repeat if stopeverything then wait(math.huge) end swait() until SOUND.Playing == false
				EFFECT:remove()
			end
		end
	end))
end


coroutine.resume(coroutine.create(function()
	while not stopeverything do
		for i = 0,1,(1/60) do
			swait()
			if not alreadyfixing then
				GUN.NeonParts.Color = Color3.fromHSV(i,1,1)
				if taunt.Value == "iNSaNiTY" then
					GUN.NeonParts.Color = Color3.fromHSV(math.random(0,19)/20,1,1)
				elseif taunt.Value == "Err0r" then
					GUN.NeonParts.Color = Color3.fromRGB(0,math.clamp(eee.PlaybackLoudness-255,0,255),0)
				elseif taunt.Value == "FAST BOIII" then
					GUN.NeonParts.Color = Color3.fromRGB(0,0,math.clamp(eee.PlaybackLoudness-191,0,255))
				elseif taunt.Value == "Glitch" then
					GUN.NeonParts.Color = Color3.fromHSV(i,1,math.clamp((eee.PlaybackLoudness/255)-.5,0,1))
				elseif taunt.Value == "Alastor" then
					GUN.NeonParts.Color = Color3.new(eee.PlaybackLoudness/500,0,0)
				elseif taunt.Value == "kArmA" then
					GUN.NeonParts.Color = Color3.new(1,1,1)
				elseif taunt.Value == "petfroge" then
					GUN.NeonParts.Color = BrickColor.Random().Color
				end
			end
		end
	end
end))

function attackone()
	attack = true
	walkspeed = 16
	AttackGyro()
	for i = 0,.5,.05 do
		swait()
		if HipVal ~= 0 then
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)) * CFrame.Angles(math.rad(0),math.rad(0),math.rad(30)),.7/3)
			Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(15),math.rad(0),math.rad(-30)),1/3)
			RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,.5,0) * CFrame.Angles(math.rad(90),math.rad(0),math.rad(30)) * rscp,1/3)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,.5,0) * CFrame.Angles(math.rad(30),math.rad(0),math.rad(0)) * lscp,1/3)
			RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
			LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
			GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
		else
			RootJoint.C0 = Clerp(RootJoint.C0,rc0 * CFrame.new() * CFrame.Angles(math.rad(0),math.rad(0),math.rad(30)),1 / 3)
			Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(15),math.rad(0),math.rad(-30)),1 / 3)
			RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,0.5,0) * CFrame.Angles(math.rad(90),math.rad(0),math.rad(30)) * rscp,1 / 3)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,0.5,0) * CFrame.Angles(math.rad(30),math.rad(0),math.rad(0)) * lscp,1 / 3)
			RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-1,0) * CFrame.Angles(math.rad(-5),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(-4),math.rad(0),math.rad(0)),1 / 3)
			LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(0),math.rad(-70),math.rad(0)) * CFrame.Angles(math.rad(-5),math.rad(0),math.rad(0)),1 / 3)
			GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(0.05,-1,-0.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1 / 2)
		end
	end
	Effect({Time = 25,EffectType = "Box",Size = Vector3.new(),Size2 = Vector3.new(3,3,3),Transparency = 0,Transparency2 = 1,CFrame = Holetwo.CFrame,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = 642890855,SoundPitch = .81,SoundVolume = 10,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
	Effect({Time = 25,EffectType = "Box",Size = Vector3.new(),Size2 = Vector3.new(3,3,3),Transparency = 0,Transparency2 = 1,CFrame = Holetwo.CFrame,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
	for i = 0,2 do
		Effect({Time = math.random(25,50),EffectType = "Round Slash",Size = Vector3.new(),Size2 = Vector3.new(.1,0,.1),Transparency = 0,Transparency2 = 1,CFrame = Holetwo.CFrame*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360))),MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 15})
		Effect({Time = math.random(25,50),EffectType = "Round Slash",Size = Vector3.new(),Size2 = Vector3.new(.1,0,.1),Transparency = 0,Transparency2 = 1,CFrame = Holetwo.CFrame*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360))),MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 15})
	end
	local mousehit = Mouse.Hit
	local DISTANCE = (Holetwo.Position - mousehit.p).Magnitude
	local killbeam = CreatePart(3,Effects,"Neon",0,0,shade,"Kill Beam",Vector3.new(1,DISTANCE,1))
	killbeam.CFrame = CFrame.new(Holetwo.Position,mousehit.p) * CFrame.new(0,0,-DISTANCE/2) * CFrame.Angles(math.rad(90),math.rad(0),math.rad(0))
	MakeForm(killbeam,"Cyl")
	coroutine.resume(coroutine.create(function()
		for i = 1,25 do
			swait()
			killbeam.Transparency = i/25
		end
		killbeam:Destroy()
	end))
	for i = 1,4 do
		coroutine.resume(coroutine.create(function()
			Lightning(Holetwo.Position,mousehit.p,15,3.5,Color3.new(1,0,0),25,0,1,0,true,55)
		end))
	end
	coroutine.resume(coroutine.create(function()
		Lightning(Holetwo.Position,mousehit.p,15,3.5,Color3.new(1,0,0),25,0,1,0,true,55)
		Effect({Time = 25,EffectType = "Box",Size = Vector3.new(),Size2 = Vector3.new(3,3,3),Transparency = 0,Transparency2 = 1,CFrame = mousehit,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = 821439273,SoundPitch = .8,SoundVolume = 10,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
		Effect({Time = 25,EffectType = "Box",Size = Vector3.new(),Size2 = Vector3.new(3,3,3),Transparency = 0,Transparency2 = 1,CFrame = mousehit,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
		for i = 0,2 do
			for a = 0, 14 do
				EFFECT1(3,math.random(4,8),"Add",mousehit*CFrame.Angles(math.rad(math.random(-360,360)),math.rad(math.random(-360,360)),math.rad(math.random(-360,360))),3,3,3,0.03,GUN.NeonParts.Color,0)
			end
		end
		mdmg(mousehit.p,10)
	end))
	for i = 0,.5,.075 do
		swait()
		if HipVal ~= 0 then
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)) * CFrame.Angles(math.rad(0),math.rad(0),math.rad(30)),.7/3)
		Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(10),math.rad(0),math.rad(-60)),1/3)
		RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,.5,0) * CFrame.Angles(math.rad(160),math.rad(-20),math.rad(60)) * rscp,1/3)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,.5,0) * CFrame.Angles(math.rad(40),math.rad(5),math.rad(5)) * lscp,1/3)
		RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
		LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
		GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
		else
			RootJoint.C0 = Clerp(RootJoint.C0,rc0 * CFrame.new() * CFrame.Angles(math.rad(-5),math.rad(0),math.rad(60)),1 / 3)
			Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(10),math.rad(0),math.rad(-60)),1 / 3)
			RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,0.5,0) * CFrame.Angles(math.rad(160),math.rad(-20),math.rad(60)) * rscp,1 / 3)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,0.5,0) * CFrame.Angles(math.rad(40),math.rad(5),math.rad(5)) * lscp,1 / 3)
			RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-1,0) * CFrame.Angles(math.rad(-5),math.rad(75),math.rad(0)) * CFrame.Angles(math.rad(-4),math.rad(0),math.rad(0)),1 / 3)
			LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(0),math.rad(-65),math.rad(0)) * CFrame.Angles(math.rad(-5),math.rad(0),math.rad(0)),1 / 3)
			GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(0.05,-1,-0.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1 / 2)
		end	
	end
	walkspeed = 50
	attack = false
end
-------------------------------------------------------------------

function Ka_Boom()
	attack = true
	walkspeed = 0
	local die = CreateSound(1566051529,RootPart,3,1)
	die.EmitterSize = 100
	swait(5)
	for i = 1,3 do
		for i = 0,1.5,.1 do
			swait()
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)) * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-5)),.7/3)
			Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(15),math.rad(0),math.rad(-5)),1/3)
			RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,.5,0) * CFrame.Angles(math.rad(175),math.rad(-10),math.rad(10)) * rscp,1/3)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,.5,0) * CFrame.Angles(math.rad(-10),math.rad(-10),math.rad(-5)) * lscp,1/3)
			RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
			LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
			GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
		end
		coroutine.resume(coroutine.create(function()
			Effect({Time = 25,EffectType = "Box",Size = Vector3.new(),Size2 = Vector3.new(3,3,3),Transparency = 0,Transparency2 = 1,CFrame = Holetwo.CFrame,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = 642890855,SoundPitch = .65,SoundVolume = 6,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
			Effect({Time = 25,EffectType = "Box",Size = Vector3.new(),Size2 = Vector3.new(3,3,3),Transparency = 0,Transparency2 = 1,CFrame = Holetwo.CFrame,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
			local skypos = Holetwo.CFrame * CFrame.new(-400,0,0)
			local DISTANCE = (Holetwo.Position - skypos.p).Magnitude
			local killbeam = CreatePart(3,Effects,"Neon",0,0,shade,"Kill Beam",Vector3.new(1,DISTANCE,1))
			killbeam.CFrame = CFrame.new(Holetwo.Position,skypos.p) * CFrame.new(0,0,-DISTANCE/2) * CFrame.Angles(math.rad(90),math.rad(0),math.rad(0))
			MakeForm(killbeam,"Cyl")
			coroutine.resume(coroutine.create(function()
				for i = 1,25 do
					swait()
					killbeam.Transparency = i/25
				end
				killbeam:Destroy()
			end))
			for i = 1,4 do
				coroutine.resume(coroutine.create(function()
					Lightning(Holetwo.Position,skypos.p,15,3.5,Color3.new(0,0,1),25,0,1,0,true,55)
				end))
			end
			for i = 0,2 do
				Effect({Time = math.random(25,50),EffectType = "Round Slash",Size = Vector3.new(),Size2 = Vector3.new(.1,0,.1),Transparency = 0,Transparency2 = 1,CFrame = Holetwo.CFrame*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360))),MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 15})
				Effect({Time = math.random(25,50),EffectType = "Round Slash",Size = Vector3.new(),Size2 = Vector3.new(.1,0,.1),Transparency = 0,Transparency2 = 1,CFrame = Holetwo.CFrame*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360))),MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 15})
			end
			Lightning(Holetwo.Position,skypos.p,15,3.5,Color3.new(0,0,1),25,0,1,0,true,55)
			Effect({Time = 25,EffectType = "Box",Size = Vector3.new(),Size2 = Vector3.new(3,3,3),Transparency = 0,Transparency2 = 1,CFrame = skypos,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = 821439273,SoundPitch = .8,SoundVolume = 10,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
			Effect({Time = 25,EffectType = "Box",Size = Vector3.new(),Size2 = Vector3.new(3,3,3),Transparency = 0,Transparency2 = 1,CFrame = skypos,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
			for i = 0,2 do
				Effect({Time = math.random(25,50),EffectType = "Round Slash",Size = Vector3.new(),Size2 = Vector3.new(.1,0,.1),Transparency = 0,Transparency2 = 1,CFrame = skypos*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360))),MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 15})
				Effect({Time = math.random(25,50),EffectType = "Round Slash",Size = Vector3.new(),Size2 = Vector3.new(.1,0,.1),Transparency = 0,Transparency2 = 1,CFrame = skypos*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360))),MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 15})
			end
		end))
		for i = 1,42 do
			swait()
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)),.7/3)
			Neck.C0 = Clerp(Neck.C0,NECKC0 * CFrame.new() * CFrame.Angles(math.rad(20),math.rad(0),math.rad(0)),.7/3)
			RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,.5,0) * CFrame.Angles(math.rad(135 + 8.5 * math.cos(sine/50)),math.rad(0),math.rad(25)) * RIGHTSHOULDERC0,.7/3)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,.5,0) * CFrame.Angles(math.rad(25 + 8.5 * math.cos(sine/50)),math.rad(0),math.rad(-25 - 5 * math.cos(sine/25))) * LEFTSHOULDERC0,.7/3)
			RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
			LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
			GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
		end
	end
	for i = 1,15 do
		swait()
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)),.7/3)
		Neck.C0 = Clerp(Neck.C0,NECKC0 * CFrame.new() * CFrame.Angles(math.rad(20),math.rad(0),math.rad(0)),.7/3)
		RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,.5,0) * CFrame.Angles(math.rad(135 + 8.5 * math.cos(sine/50)),math.rad(0),math.rad(25)) * RIGHTSHOULDERC0,.7/3)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,.5,0) * CFrame.Angles(math.rad(25 + 8.5 * math.cos(sine/50)),math.rad(0),math.rad(-25 - 5 * math.cos(sine/25))) * LEFTSHOULDERC0,.7/3)
		RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
		LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
		GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
	end
	local BEAM = CreatePart(3,Effects,"Neon",0,0,Color3.new(0,0,1),"Beam",Vector3.new())
	local BEAM2 = CreatePart(3,Effects,"Neon",0,0,Color3.new(0,0,1),"Beam",Vector3.new())
	MakeForm(BEAM,"Ball")
	MakeForm(BEAM2,"Ball")
	BEAM.CFrame = CFrame.new(RootPart.Position)
	BEAM2.CFrame = CFrame.new(RootPart.Position)
	local boooom = CreateSound(415700134,RootPart,10,1,false)
	boooom.EmitterSize = 100
	for i=1,140 do
		swait()
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)),.7/3)
		Neck.C0 = Clerp(Neck.C0,NECKC0 * CFrame.new() * CFrame.Angles(math.rad(20),math.rad(0),math.rad(0)),.7/3)
		RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,.5,0) * CFrame.Angles(math.rad(135 + 8.5 * math.cos(sine/50)),math.rad(0),math.rad(25)) * RIGHTSHOULDERC0,.7/3)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,.5,0) * CFrame.Angles(math.rad(25 + 8.5 * math.cos(sine/50)),math.rad(0),math.rad(-25 - 5 * math.cos(sine/25))) * LEFTSHOULDERC0,.7/3)
		RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
		LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
		GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
		BEAM.Size = BEAM.Size + Vector3.new(.7,8,.7)
		BEAM2.Size = BEAM2.Size + Vector3.new(2,2,2)
		BEAM.Color = GUN.NeonParts.Color
		BEAM2.Color = GUN.NeonParts.Color
		BEAM.CFrame = CFrame.new(RootPart.Position)
		BEAM2.CFrame = CFrame.new(RootPart.Position)
		WACKYEFFECT({TIME = 5+i,EffectType = "Swirl",Size = BEAM2.Size*1.15,Size2 = Vector3.new(0,BEAM.Size.Y,0),Transparency = .8,Transparency2 = 1,CFrame = BEAM.CFrame * CFrame.Angles(math.rad(0),math.rad(i*5),math.rad(0)),MoveToPos = nil,RotationX = 0,RotationY = i/8,RotationZ = 0,Material = "Neon",Color = GUN.NeonParts.Color,SoundID = nil,SoundPitch = nil,SoundVolume = nil})
	end
	mdmg(RootPart.Position,BEAM2.Size.Y/2)
	Effect({TIME = 75,EffectType = "Sphere",Size = BEAM.Size,Size2 = Vector3.new(0,BEAM.Size.Y,0),Transparency = 0,Transparency2 = 0,CFrame = BEAM.CFrame,MoveToPos = nil,RotationX = 0,RotationY = 0,RotationZ = 0,Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil})
	Effect({TIME = 75,EffectType = "Sphere",Size = BEAM2.Size,Size2 = Vector3.new(),Transparency = 0,Transparency2 = .6,CFrame = BEAM2.CFrame,MoveToPos = nil,RotationX = 0,RotationY = 0,RotationZ = 0,Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil})
	for i,v in pairs(Effects:GetChildren()) do
		v.Color = shade
		v:GetPropertyChangedSignal("Color"):Connect(function()
			if stopeverything then wait(math.huge) end
			v.Color = shade
		end)
	end
	BEAM2:Destroy()
	BEAM:Destroy()
	attack = false
	walkspeed = 50
end

-----------------------------------------------------------

function attacktwo()
	attack = true
	walkspeed = 0
	AttackGyro()
	local gBullet = CreatePart(3,Effects,"Neon",0,0,Color3.new(0,0,1),"AbsoluteNoob",Vector3.new())
	MakeForm(gBullet,"Ball")
	gBullet.CFrame = LeftArm.CFrame*CFrame.new(0,-1.5,0)
	CreateSound(2785493,gBullet,10,.8)
	for i = 0,1.25,.025 do
		swait()
		Effect({Time = math.random(35,55),EffectType = "Sphere",Size = Vector3.new(.5,.5,.5),Size2 = Vector3.new(1,1,1),Transparency = 0,Transparency2 = 1,CFrame = LeftArm.CFrame*CFrame.new(0,-1.5,0),MoveToPos = LeftArm.CFrame*CFrame.new(0,-1.5,0)*CFrame.new(math.random(-10,10),math.random(-10,10),math.random(-10,10)).p,RotationX = nil,RotationY = nil,RotationZ = nil,Material = "Neon",Color = Color3.new(1,0,0),SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 50,SizeBoomerang = 50})
		gBullet.Size = gBullet.Size * 1.085
		gBullet.CFrame = LeftArm.CFrame*CFrame.new(0,-1.5,0)
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)) * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-30)),.7/3)
		Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(-5 - 3 * math.cos(sine/12)),math.rad(0),math.rad(30)),1/3)
		RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,.5,0) * CFrame.Angles(math.rad(135 + 8.5 * math.cos(sine/49)),math.rad(0),math.rad(25)) * RIGHTSHOULDERC0,.7/3)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,.5 + .1 * math.cos(sine/12),-0) * CFrame.Angles(math.rad(85 - 1.5 * math.cos(sine/12)),math.rad(0 - 6 * math.cos(sine/12)),math.rad(-30 - 6 * math.cos(sine/12))) * lscp,1/3)
		RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
		LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
		GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
	end
	local bullets = {}
	for i = 1,math.random(27,41) do
		swait()
		local Bullet = CreatePart(3,Effects,"Neon",0,0,Color3.new(0,0,1),"AbsoluteBEAN",Vector3.new(.6,.6,.6))
		MakeForm(Bullet,"Ball")
		Bullet.CFrame = gBullet.CFrame
		Effect({Time = math.random(5,20),EffectType = "Sphere",Size = Vector3.new(3,3,3)*math.random(-3,2),Size2 = Vector3.new(6,6,6)*math.random(-3,2),Transparency = .4,Transparency2 = 1,CFrame = Bullet.CFrame,MoveToPos = nil,RotationX = nil,RotationY = nil,RotationZ = nil,Material = "Neon",Color = Color3.new(1,0,0),SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 25})
		table.insert(bullets,Bullet)
	end
	local oofing = false
	for b = 1,#bullets do
		swait()
		local part,pos = rayCast(LeftArm.CFrame*CFrame.new(0,-1.5,0).p,((Mouse.Hit.p+Vector3.new(math.random(-15,15),math.random(-7,7),math.random(-15,15))) - LeftArm.CFrame*CFrame.new(0,-1.5,0).p),500,Character)
		coroutine.resume(coroutine.create(function()
			FireArc(bullets[b],pos,math.random(17,31),math.random(9,15),false)
			Effect({Time = math.random(25,35),EffectType = "Sphere",Size = Vector3.new(.6,.6,.6),Size2 = Vector3.new(1.6,1.6,1.6),Transparency = 0,Transparency2 = 1,CFrame = bullets[b].CFrame,MoveToPos = nil,RotationX = nil,RotationY = nil,RotationZ = nil,Material = "Neon",Color = Color3.new(1,0,0),SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 25})
			swait(math.random(55,65))
			for i = 1,3 do
				Effect({Time = math.random(45,65),EffectType = "Sphere",Size = Vector3.new(.6,6,.6)*math.random(-1.05,1.25),Size2 = Vector3.new(1.6,10,1.6)*math.random(-1.05,1.25),Transparency = 0,Transparency2 = 1,CFrame = bullets[b].CFrame*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360))),MoveToPos = nil,RotationX = nil,RotationY = nil,RotationZ = nil,Material = "Neon",Color = Color3.new(1,0,0),SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 20,SizeBoomerang = 35})
			end
			for i = 0,10 do
				swait()
				bullets[b].Transparency = bullets[b].Transparency + .1
			end
			oofing = not oofing
			if oofing then
				mdmg(bullets[b].Position,10)
			end
			local EEEBRUHEEE = CreateSound(168513088,bullets[b],3.5,1.1,false)
			bullets[b].Transparency = 1
			EEEBRUHEEE.Ended:Connect(function()
				if stopeverything then wait(math.huge) end
				bullets[b]:Destroy()
			end)
		end))
	end
	for i = 0,10 do
		swait()
		gBullet.Transparency = gBullet.Transparency + .1
	end
	gBullet:Destroy()
	walkspeed = 50
	attack = false
end

---------------------------------------------------

function hedshoot()
	attack = true
	walkspeed = 16
	CreateSound(235097614,RootPart,6,1.5,false)
	for i = 0,.5,.05 do
		swait()
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)) * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-60)),.7/3)
		Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(0),math.rad(0),math.rad(60)),1/3)
		RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.25,.5,-.25) * CFrame.Angles(math.rad(90),math.rad(0),math.rad(-60)) * rscp,1/3)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.25,.5,-.25) * CFrame.Angles(math.rad(95),math.rad(0),math.rad(10)) * lscp,1/3)
		RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
		LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
		GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(0,-.5,0) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
	end
	Effect({Time = 25,EffectType = "Box",Size = Vector3.new(2,2,2),Size2 = Vector3.new(5,5,5),Transparency = 0,Transparency2 = 1,CFrame = RootPart.CFrame,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = 642890855,SoundPitch = .65,SoundVolume = 10,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
	Effect({Time = 25,EffectType = "Box",Size = Vector3.new(2,2,2),Size2 = Vector3.new(5,5,5),Transparency = 0,Transparency2 = 1,CFrame = RootPart.CFrame,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
	Effect({Time = math.random(25,45),EffectType = "Sphere",Size = Vector3.new(2,100,2),Size2 = Vector3.new(6,100,6),Transparency = 0,Transparency2 = 1,CFrame = RootPart.CFrame*CFrame.new(math.random(-1,1),math.random(-1,1),-50)*CFrame.Angles(math.rad(math.random(89,91)),math.rad(math.random(-1,1)),math.rad(math.random(-1,1))),MoveToPos = nil,RotationX = nil,RotationY = nil,RotationZ = nil,Material = "Neon",Color = Color3.new(1,0,0),SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 45})
	Effect({Time = math.random(25,45),EffectType = "Sphere",Size = Vector3.new(3,100,3),Size2 = Vector3.new(9,100,9),Transparency = 0,Transparency2 = 1,CFrame = RootPart.CFrame*CFrame.new(math.random(-1,1),math.random(-1,1),-50)*CFrame.Angles(math.rad(math.random(89,91)),math.rad(math.random(-1,1)),math.rad(math.random(-1,1))),MoveToPos = nil,RotationX = nil,RotationY = nil,RotationZ = nil,Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 45})
	mdmg(RootPart.Position,14)
	for i = 1,4 do
		RootPart.CFrame = RootPart.CFrame * CFrame.new(0,0,-25)
		mdmg(RootPart.Position,14)
		coroutine.resume(coroutine.create(function()
			Lightning(RootPart.CFrame*CFrame.new(math.random(-2.5,2.5),math.random(-5,5),math.random(-15,15)).p,RootPart.CFrame*CFrame.new(math.random(-2.5,2.5),math.random(-5,5),math.random(-15,15)).p,6,25,shade,math.random(30,45),.5,1.5,0,true,60) 
		end))	
		coroutine.resume(coroutine.create(function()
			Lightning(RootPart.CFrame*CFrame.new(math.random(-2.5,2.5),math.random(-5,5),math.random(-15,15)).p,RootPart.CFrame*CFrame.new(math.random(-2.5,2.5),math.random(-5,5),math.random(-15,15)).p,6,25,Color3.new(0,0,1),math.random(30,45),.5,1.5,0,true,60)
		end))
	end
	Effect({Time = 25,EffectType = "Box",Size = Vector3.new(2,2,2),Size2 = Vector3.new(5,5,5),Transparency = 0,Transparency2 = 1,CFrame = RootPart.CFrame,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
	Effect({Time = 25,EffectType = "Box",Size = Vector3.new(2,2,2),Size2 = Vector3.new(5,5,5),Transparency = 0,Transparency2 = 1,CFrame = RootPart.CFrame,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
	for i = 0,.5,.1 do
		swait()
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)) * CFrame.Angles(math.rad(0),math.rad(0),math.rad(90)),.7/3)
		Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-90)),1/3)
		RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,.5,0) * CFrame.Angles(math.rad(90),math.rad(0),math.rad(90)) * rscp,1/3)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,.5,0) * CFrame.Angles(math.rad(40),math.rad(5),math.rad(5)) * lscp,1/3)
		RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
		LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
		GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
	end
	attack = false
	walkspeed = 50
end

--------------------------------------------------

local stillraining = false

function painlessrain()
	if stillraining then
		return
	else
		stillraining = true
	end
	attack = true
	walkspeed = 16
	coroutine.wrap(function()
		for i = 0,2 do
			swait(12)
			CreateSound(199145095,GUN.Joint,10,1)
		end
	end)()
	for i = 0,2,.1 do
		swait()
		if HipVal ~= 0 then
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)) * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-10)),.7/3)
		Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(25),math.rad(0),math.rad(-20)),1/3)
		RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,.5,0) * CFrame.Angles(math.rad(35),math.rad(-35),math.rad(20)) * rscp,1/3)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,.5,0) * CFrame.Angles(math.rad(-20),math.rad(-5),math.rad(-10)) * lscp,1/3)
		RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
		LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
		GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(doe * 22),math.rad(0),math.rad(0)),1/2)
		else
			RootJoint.C0 = Clerp(RootJoint.C0,rc0 * CFrame.new() * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-10)),1 / 3)
			Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new(0,0,0 + ((1) - 1)) * CFrame.Angles(math.rad(25),math.rad(0),math.rad(-20)),1 / 3)
			RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,0.5,0) * CFrame.Angles(math.rad(35),math.rad(-35),math.rad(20)) * rscp,1 / 3)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,0.5,0) * CFrame.Angles(math.rad(-20),math.rad(-5),math.rad(-10)) * lscp,1 / 3)
			RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-1,0) * CFrame.Angles(math.rad(-5),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(-4),math.rad(0),math.rad(0)),1 / 3)
			LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(0),math.rad(-70),math.rad(0)) * CFrame.Angles(math.rad(-5),math.rad(0),math.rad(0)),1 / 3)
			GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(0.05,-1,-0.15) * CFrame.Angles(math.rad(doe * 22),math.rad(0),math.rad(0)),1 / 2)
		end	
		end
	for i = 0,1.5,.1 do
		swait()
		if HipVal ~= 0 then
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)) * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-5)),.7/3)
		Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(15),math.rad(0),math.rad(-5)),1/3)
		RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,.5,0) * CFrame.Angles(math.rad(175),math.rad(-10),math.rad(10)) * rscp,1/3)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,.5,0) * CFrame.Angles(math.rad(-10),math.rad(-10),math.rad(-5)) * lscp,1/3)
		RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
		LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
		GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
			else
				RootJoint.C0 = Clerp(RootJoint.C0,rc0 * CFrame.new() * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-10)),1 / 3)
				Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new(0,0,0 + ((1) - 1)) * CFrame.Angles(math.rad(25),math.rad(0),math.rad(-20)),1 / 3)
				RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,0.5,0) * CFrame.Angles(math.rad(35),math.rad(-35),math.rad(20)) * rscp,1 / 3)
				LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,0.5,0) * CFrame.Angles(math.rad(-20),math.rad(-5),math.rad(-10)) * lscp,1 / 3)
				RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-1,0) * CFrame.Angles(math.rad(-5),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(-4),math.rad(0),math.rad(0)),1 / 3)
				LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(0),math.rad(-70),math.rad(0)) * CFrame.Angles(math.rad(-5),math.rad(0),math.rad(0)),1 / 3)
				GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(0.05,-1,-0.15) * CFrame.Angles(math.rad(doe * 22),math.rad(0),math.rad(0)),1 / 2)
			end	
	end
	for i = 0,.5,.1 do
		swait()
		if HipVal ~= 0 then
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)) * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-5)),.7/3)
		Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(15),math.rad(0),math.rad(-5)),1/3)
		RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,-.2,0) * CFrame.Angles(math.rad(175),math.rad(-10),math.rad(10)) * rscp,1/3)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,.5,0) * CFrame.Angles(math.rad(-10),math.rad(-10),math.rad(-5)) * lscp,1/3)
		RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
		LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
		GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
			else
				RootJoint.C0 = Clerp(RootJoint.C0,rc0 * CFrame.new() * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-5)),1 / 3)
				Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new(0,0,0 + ((1) - 1)) * CFrame.Angles(math.rad(15),math.rad(0),math.rad(-5)),1 / 3)
				RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,0.5,0) * CFrame.Angles(math.rad(175),math.rad(-10),math.rad(10)) * rscp,1 / 3)
				LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,0.5,0) * CFrame.Angles(math.rad(-10),math.rad(-10),math.rad(-5)) * lscp,1 / 3)
				RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-1,0) * CFrame.Angles(math.rad(-5),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(-4),math.rad(0),math.rad(0)),1 / 3)
				LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(0),math.rad(-70),math.rad(0)) * CFrame.Angles(math.rad(-5),math.rad(0),math.rad(0)),1 / 3)
				GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(0.05,-1,-0.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1 / 2)
			end		
		end
	local skypos = Holetwo.CFrame * CFrame.new(-400,0,0)
	local DISTANCE = (Holetwo.Position - skypos.p).Magnitude
	local killbeam = CreatePart(3,Effects,"Neon",0,0,shade,"Kill Beam",Vector3.new(1,DISTANCE,1))
	killbeam.CFrame = CFrame.new(Holetwo.Position,skypos.p) * CFrame.new(0,0,-DISTANCE/2) * CFrame.Angles(math.rad(90),math.rad(0),math.rad(0))
	MakeForm(killbeam,"Cyl")
	coroutine.resume(coroutine.create(function()
		for i = 1,25 do
			swait()
			killbeam.Transparency = i/25
		end
		killbeam:Destroy()
	end))
	for i = 1,4 do
		coroutine.resume(coroutine.create(function()
			Lightning(Holetwo.Position,skypos.p,15,3.5,Color3.new(1,0,0),25,0,1,0,true,55)
		end))
	end
	for i = 0,2 do
	end
	for i = 0,.5,.1 do
		swait()
		if HipVal ~= 0 then
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)) * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-5)),.7/3)
		Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(15),math.rad(0),math.rad(-5)),1/3)
		RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,.5,0) * CFrame.Angles(math.rad(175),math.rad(-10),math.rad(10)) * rscp,1/3)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,.5,0) * CFrame.Angles(math.rad(-5),math.rad(-5),math.rad(0)) * lscp,1/3)
		RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
		LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
		GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
		else
			RootJoint.C0 = Clerp(RootJoint.C0,rc0 * CFrame.new() * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-5)),1 / 3)
			Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new(0,0,0 + ((1) - 1)) * CFrame.Angles(math.rad(15),math.rad(0),math.rad(-5)),1 / 3)
			RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,0.5,0) * CFrame.Angles(math.rad(175),math.rad(-10),math.rad(10)) * rscp,1 / 3)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,0.5,0) * CFrame.Angles(math.rad(-5),math.rad(-5),math.rad(0)) * lscp,1 / 3)
			RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-1,0) * CFrame.Angles(math.rad(-5),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(-4),math.rad(0),math.rad(0)),1 / 3)
			LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(0),math.rad(-70),math.rad(0)) * CFrame.Angles(math.rad(-5),math.rad(0),math.rad(0)),1 / 3)
			GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(0.05,-1,-0.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1 / 2)
		end	
		end	
	attack = false
	walkspeed = 50
	for i = 0,2 do
	end
	for i = 1,5 do
		local Sky = RootPart.CFrame*CFrame.new(0,500,0)
		local MoPos = Mouse.Hit.p
		local DISTANCE = (Sky.p - MoPos).Magnitude
		for i = 1,4 do
			coroutine.resume(coroutine.create(function()

			end))
		end
		local killbeam = CreatePart(3,Effects,"Neon",0,0,shade,"Kill Beam",Vector3.new(1,DISTANCE,1))
		killbeam.CFrame = CFrame.new(Sky.p,MoPos) * CFrame.new(0,0,-DISTANCE/2) * CFrame.Angles(math.rad(90),math.rad(0),math.rad(0))
		MakeForm(killbeam,"Cyl")
		coroutine.resume(coroutine.create(function()
			for i = 1,25 do
				swait()
				killbeam.Transparency = i/25
			end
			killbeam:Destroy()
		end))
		Effect({Time = 25,EffectType = "Box",Size = Vector3.new(),Size2 = Vector3.new(3,3,3),Transparency = 0,Transparency2 = 1,CFrame = CFrame.new(MoPos),MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = 821439273,SoundPitch = .8,SoundVolume = 10,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
		Effect({Time = 25,EffectType = "Box",Size = Vector3.new(),Size2 = Vector3.new(3,3,3),Transparency = 0,Transparency2 = 1,CFrame = CFrame.new(MoPos),MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
		for i = 0,2 do
			--Effect({Time = math.random(25,50),EffectType = "Round Slash",Size = Vector3.new(),Size2 = Vector3.new(.1,0,.1),Transparency = 0,Transparency2 = 1,CFrame = CFrame.new(MoPos)*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360))),MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 15})
			--Effect({Time = math.random(25,50),EffectType = "Round Slash",Size = Vector3.new(),Size2 = Vector3.new(.1,0,.1),Transparency = 0,Transparency2 = 1,CFrame = CFrame.new(MoPos)*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360))),MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 15})
			for a = 0, 14 do
				EFFECT1(3,math.random(4,8),"Add",CFrame.new(MoPos)*CFrame.Angles(math.rad(math.random(-360,360)),math.rad(math.random(-360,360)),math.rad(math.random(-360,360))),3,3,3,0.03,GUN.NeonParts.Color,0)
			end
		end
		mdmg(MoPos,5)
	end
	stillraining = false
end

-------------------------------------------------
function SingularityBeam()
	attack = true
	cannecksnap = false
	walkspeed = 0
	AttackGyro()
	for i = 0,.5,.05 do
		swait()
		if HipVal ~= 0 then
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,0 - .5 * math.sin(sine/50)) * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-60)),.7/3)
		Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(0),math.rad(0),math.rad(60)),1/3)
		RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.25,.5,-.25) * CFrame.Angles(math.rad(90),math.rad(0),math.rad(-60)) * rscp,1/3)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.25,.5,-.25) * CFrame.Angles(math.rad(95),math.rad(0),math.rad(10)) * lscp,1/3)
		RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-.5,-.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),.7/3)
		LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),.7/3)
		GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(0,-.5,0) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
		else
			RootJoint.C0 = Clerp(RootJoint.C0,rc0 * CFrame.new() * CFrame.Angles(math.rad(0),math.rad(0),math.rad(-60)),1 / 3)
			Neck.C0 = Clerp(Neck.C0,nc0 * CFrame.new() * CFrame.Angles(math.rad(0),math.rad(0),math.rad(60)),1 / 3)
			RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.25,0.5,-.25) * CFrame.Angles(math.rad(90),math.rad(0),math.rad(-60)) * rscp,1 / 3)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.25,0.5,-.25) * CFrame.Angles(math.rad(95),math.rad(0),math.rad(10)) * lscp,1 / 3)
			RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-1,0) * CFrame.Angles(math.rad(-5),math.rad(75),math.rad(0)) * CFrame.Angles(math.rad(-4),math.rad(0),math.rad(0)),1 / 3)
			LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(0),math.rad(-65),math.rad(0)) * CFrame.Angles(math.rad(-5),math.rad(0),math.rad(0)),1 / 3)
			GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(0,-.5,0) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1 / 2)
		end	
		end
		local HoleDist = (Hole.Position - Holetwo.Position).Magnitude
		local chargebeam = CreatePart(3,Effects,"Neon",0,0,shade,"Charge Beam",Vector3.new(.25,HoleDist,.25),false)
		MakeForm(chargebeam,"Cyl")
		chargebeam.CFrame = CFrame.new(Hole.Position,Holetwo.Position) * CFrame.new(0,0,-HoleDist/2) * CFrame.Angles(math.rad(90),math.rad(0),math.rad(0))
		local chargeweld = weldBetween(GUN.Joint,chargebeam)
		local chargeball = CreatePart(3,Effects,"Neon",0,0,shade,"Charge Ball",Vector3.new(.5,.5,.5),false)
		chargeball.Shape = "Ball"
		chargeball.CFrame = Holetwo.CFrame
		weldBetween(Holetwo,chargeball)
		CreateSound(342793847,Hole,10,1,false)
		local bigball = game:GetService("TweenService"):Create(chargeball,TweenInfo.new(3.86,Enum.EasingStyle.Linear),{Size = Vector3.new(2.5,2.5,2.5)})
		bigball:Play()
		bigball.Completed:Wait()
		chargebeam:Destroy()
		local KillDist = (Holetwo.Position - Mouse.Hit.p).Magnitude
		coroutine.resume(coroutine.create(function()
			repeat if stopeverything then wait(math.huge) end KillDist = (Holetwo.Position - Mouse.Hit.p).Magnitude Swait() until not attack
		end))
		local killbeam = CreatePart(3,Effects,"Neon",0,0,shade,"Kill Beam",Vector3.new(2.5,KillDist,2.5))
		MakeForm(killbeam,"Cyl")
		killbeam.Touched:Connect(function(victim)
			if stopeverything then wait(math.huge) end
			mdmg(victim.Position,5)
		end)
		coroutine.resume(coroutine.create(function()
			while not stopeverything and killbeam:IsDescendantOf(game) do
				mdmg(Mouse.Hit.p,5)
				swait()
			end
		end))
	coroutine.resume(coroutine.create(function()
		local isdoingathing = false
		while not stopeverything and killbeam:IsDescendantOf(game) do
			isdoingathing = not isdoingathing
			if lplr.Name == USERNAME then
				RootPart.CFrame = RootPart.CFrame * CFrame.new(0,0,.1)
			end
			killbeam.Size = Vector3.new(2.5,KillDist,2.5)
			killbeam.CFrame = CFrame.new(Holetwo.Position,Mouse.Hit.p) * CFrame.new(0,0,-KillDist/2) * CFrame.Angles(math.rad(90),math.rad(0),math.rad(0))
			if isdoingathing then
				coroutine.resume(coroutine.create(function()
					Lightning(Holetwo.Position,Mouse.Hit.p,15,3,Color3.new(1,0,0),10,0,1,0,true,55)
				end))
				for a = 0, 14 do
					EFFECT1(3,math.random(4,8),"Add",Mouse.Hit*CFrame.Angles(math.rad(math.random(-360,360)),math.rad(math.random(-360,360)),math.rad(math.random(-360,360))),3,3,3,0.03,GUN.NeonParts.Color,0)
				end
				Effect({Time = 10,EffectType = "Round Slash",Size = Vector3.new(),Size2 = Vector3.new(.1,0,.1),Transparency = 0,Transparency2 = 1,CFrame = Holetwo.CFrame*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360))),MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 15})
				Effect({Time = 10,EffectType = "Round Slash",Size = Vector3.new(),Size2 = Vector3.new(.1,0,.1),Transparency = 0,Transparency2 = 1,CFrame = Holetwo.CFrame*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360))),MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 15})
				Effect({Time = 10,EffectType = "Box",Size = Vector3.new(),Size2 = Vector3.new(3,3,3),Transparency = 0,Transparency2 = 1,CFrame = Mouse.Hit,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = Color3.new(1,0,0),SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
				Effect({Time = 10,EffectType = "Box",Size = Vector3.new(),Size2 = Vector3.new(3,3,3),Transparency = 0,Transparency2 = 1,CFrame = Mouse.Hit,MoveToPos = nil,RotationX = math.random(-1,1),RotationY = math.random(-1,1),RotationZ = math.random(-1,1),Material = "Neon",Color = shade,SoundID = nil,SoundPitch = nil,SoundVolume = nil,UseBoomerangMath = true,Boomerang = 0,SizeBoomerang = 50})
			end
			Swait()
		end
	end))
	CreateSound(138677306,Holetwo,10,1,false)
	CreateSound(415700134,Holetwo,10,1,false)
	Swait(150)
	CreateSound(3264923,Holetwo,10,1,false)
	Swait(30)
	chargeball:Destroy()
	killbeam:Destroy()
	walkspeed = 50
	attack = false
	cannecksnap = true
end


local FLYING = false
iyflyspeed = 1
function sFLY()
	if not ISFLYING then
		FLYING = false
	else
		local CONTROL = {F = 0,B = 0,L = 0,R = 0,Q = 0,E = 0}
		local lCONTROL = {F = 0,B = 0,L = 0,R = 0,Q = 0,E = 0}
		local SPEED = 0			
		local function FLY()
			FLYING = true
			BG = Instance.new('BodyGyro',RootPart)
			BV = Instance.new('BodyVelocity',RootPart)
			BG.MaxTorque = Vector3.new(math.huge,math.huge,math.huge)
			BG.P = 1e4
			BG.CFrame = RootPart.CFrame
			BV.Velocity = Vector3.new(0,0,0)
			BV.MaxForce = Vector3.new(math.huge,math.huge,math.huge)
			coroutine.resume(coroutine.create(function()
				repeat if stopeverything then wait(math.huge) end
					game:GetService("RunService").RenderStepped:Wait()
					if not alreadyfixing then
						if CONTROL.L + CONTROL.R ~= 0 or CONTROL.F + CONTROL.B ~= 0 or CONTROL.Q + CONTROL.E ~= 0 then
							SPEED = 50
						elseif not (CONTROL.L + CONTROL.R ~= 0 or CONTROL.F + CONTROL.B ~= 0 or CONTROL.Q + CONTROL.E ~= 0) and SPEED ~= 0 then
							SPEED = 0
						end
						if (CONTROL.L + CONTROL.R) ~= 0 or (CONTROL.F + CONTROL.B) ~= 0 or (CONTROL.Q + CONTROL.E) ~= 0 then
							BV.Velocity = ((workspace.CurrentCamera.CoordinateFrame.lookVector * (CONTROL.F + CONTROL.B)) + ((workspace.CurrentCamera.CoordinateFrame * CFrame.new(CONTROL.L + CONTROL.R,(CONTROL.F + CONTROL.B + CONTROL.Q + CONTROL.E) * 0.2,0).p) - workspace.CurrentCamera.CoordinateFrame.p)) * SPEED
							lCONTROL = {F = CONTROL.F,B = CONTROL.B,L = CONTROL.L,R = CONTROL.R}
						elseif (CONTROL.L + CONTROL.R) == 0 and (CONTROL.F + CONTROL.B) == 0 and (CONTROL.Q + CONTROL.E) == 0 and SPEED ~= 0 then
							BV.Velocity = ((workspace.CurrentCamera.CoordinateFrame.lookVector * (lCONTROL.F + lCONTROL.B)) + ((workspace.CurrentCamera.CoordinateFrame * CFrame.new(lCONTROL.L + lCONTROL.R,(lCONTROL.F + lCONTROL.B + CONTROL.Q + CONTROL.E) * 0.2,0).p) - workspace.CurrentCamera.CoordinateFrame.p)) * SPEED
						else
							BV.Velocity = Vector3.new(0,0,0)
						end
						BG.CFrame = workspace.CurrentCamera.CoordinateFrame
					end
				until not FLYING
				CONTROL = {F = 0,B = 0,L = 0,R = 0,Q = 0,E = 0}
				lCONTROL = {F = 0,B = 0,L = 0,R = 0,Q = 0,E = 0}
				SPEED = 0
				if not alreadyfixing then
					for i,v in pairs(RootPart:GetChildren()) do
						if v:IsA("BodyMover") then
							v:Destroy()
						end
					end
					RootPart.CFrame = CFrame.new(RootPart.Position)
				end
			end))
		end
		local IYMouse = Player:GetMouse()
		IYMouse.KeyDown:connect(function(KEY)
			if stopeverything then wait(math.huge) end
			if KEY:lower() == 'w' then
				CONTROL.F = iyflyspeed
			elseif KEY:lower() == 's' then
				CONTROL.B = - iyflyspeed
			elseif KEY:lower() == 'a' then
				CONTROL.L = - iyflyspeed
			elseif KEY:lower() == 'd' then 
				CONTROL.R = iyflyspeed
			elseif KEY:lower() == 'e' then
				CONTROL.Q = iyflyspeed*2
			elseif KEY:lower() == 'q' then
				CONTROL.E = -iyflyspeed*2
			end
		end)
		IYMouse.KeyUp:connect(function(KEY)
			if stopeverything then wait(math.huge) end
			if KEY:lower() == 'w' then
				CONTROL.F = 0
			elseif KEY:lower() == 's' then
				CONTROL.B = 0
			elseif KEY:lower() == 'a' then
				CONTROL.L = 0
			elseif KEY:lower() == 'd' then
				CONTROL.R = 0
			elseif KEY:lower() == 'e' then
				CONTROL.Q = 0
			elseif KEY:lower() == 'q' then
				CONTROL.E = 0
			end
		end)
		FLY()
	end
end
function sphere(bonuspeed,type,pos,scale,value,color)
	local type = type
	local rng = Instance.new("Part",Effects)
	rng.Anchored = true
	rng.BrickColor = color
	rng.CanCollide = false
	rng.FormFactor = 3
	rng.Name = "Ring"
	rng.Material = "Neon"
	rng.Size = Vector3.new(1,1,1)
	rng.Transparency = 0
	rng.TopSurface = 0
	rng.BottomSurface = 0
	rng.CFrame = pos
	local rngm = Instance.new("SpecialMesh",rng)
	rngm.MeshType = "Sphere"
	rngm.Scale = scale
	local scaler2 = 1
	if type == "Add" then
		scaler2 = 1*value
	elseif type == "Divide" then
		scaler2 = 1/value
	end
	coroutine.resume(coroutine.create(function()
		for i = 0,10/bonuspeed,0.1 do
			swait()
			if type == "Add" then
				scaler2 = scaler2 - 0.01*value/bonuspeed
			elseif type == "Divide" then
				scaler2 = scaler2 - 0.01/value*bonuspeed
			end
			rng.BrickColor = BrickColor.random()
			rng.Transparency = rng.Transparency + 0.01*bonuspeed
			rngm.Scale = rngm.Scale + Vector3.new(scaler2*bonuspeed,scaler2*bonuspeed,scaler2*bonuspeed)
		end
		rng:Destroy()
	end))
end

function sphere2(bonuspeed,type,pos,scale,value,value2,value3,color)
	local type = type
	local rng = Instance.new("Part",Effects)
	rng.Anchored = true
	rng.BrickColor = color
	rng.CanCollide = false
	rng.FormFactor = 3
	rng.Name = "Ring"
	rng.Material = "Neon"
	rng.Size = Vector3.new(1,1,1)
	rng.Transparency = 0
	rng.TopSurface = 0
	rng.BottomSurface = 0
	rng.CFrame = pos
	local rngm = Instance.new("SpecialMesh",rng)
	rngm.MeshType = "Sphere"
	rngm.Scale = scale
	local scaler2 = 1
	local scaler2b = 1
	local scaler2c = 1
	if type == "Add" then
		scaler2 = 1*value
		scaler2b = 1*value2
		scaler2c = 1*value3
	elseif type == "Divide" then
		scaler2 = 1/value
		scaler2b = 1/value2
		scaler2c = 1/value3
	end
	coroutine.resume(coroutine.create(function()
		for i = 0,10/bonuspeed,0.1 do
			swait()
			if type == "Add" then
				scaler2 = scaler2 - 0.01*value/bonuspeed
				scaler2b = scaler2b - 0.01*value/bonuspeed
				scaler2c = scaler2c - 0.01*value/bonuspeed
			elseif type == "Divide" then
				scaler2 = scaler2 - 0.01/value*bonuspeed
				scaler2b = scaler2b - 0.01/value*bonuspeed
				scaler2c = scaler2c - 0.01/value*bonuspeed
			end
			rng.Transparency = rng.Transparency + 0.01*bonuspeed
			rngm.Scale = rngm.Scale + Vector3.new(scaler2*bonuspeed,scaler2b*bonuspeed,scaler2c*bonuspeed)
		end
		rng:Destroy()
	end))
end

function PixelBlockX(bonuspeed,FastSpeed,type,pos,x1,y1,z1,value,color,outerpos)
	local type = type
	local rng = Instance.new("Part",Effects)
	rng.Anchored = true
	rng.BrickColor = color
	rng.CanCollide = false
	rng.FormFactor = 3
	rng.Name = "Ring"
	rng.Material = "Neon"
	rng.Size = Vector3.new(1,1,1)
	rng.Transparency = 0
	rng.TopSurface = 0
	rng.BottomSurface = 0
	rng.CFrame = pos
	rng.CFrame = rng.CFrame + rng.CFrame.lookVector*outerpos
	local rngm = Instance.new("SpecialMesh",rng)
	rngm.MeshType = "Brick"
	rngm.Scale = Vector3.new(x1,y1,z1)
	local scaler2 = 1
	local speeder = FastSpeed/10
	if type == "Add" then
		scaler2 = 1*value
	elseif type == "Divide" then
		scaler2 = 1/value
	end
	coroutine.resume(coroutine.create(function()
		for i = 0,10/bonuspeed,0.1 do
			swait()
			if type == "Add" then
				scaler2 = scaler2 - 0.01*value/bonuspeed
			elseif type == "Divide" then
				scaler2 = scaler2 - 0.01/value*bonuspeed
			end
			rng.BrickColor = BrickColor.random()
			speeder = speeder - 0.01*FastSpeed*bonuspeed/10
			rng.CFrame = rng.CFrame + rng.CFrame.lookVector*speeder*bonuspeed
			rng.Transparency = rng.Transparency + 0.01*bonuspeed
			rngm.Scale = rngm.Scale - Vector3.new(scaler2*bonuspeed,scaler2*bonuspeed,scaler2*bonuspeed)
		end
		rng:Destroy()
	end))
end

function sphereMK(bonuspeed,FastSpeed,type,pos,x1,y1,z1,value,color,outerpos)
	local type = type
	local rng = Instance.new("Part",Effects)
	rng.Anchored = true
	rng.BrickColor = color
	rng.CanCollide = false
	rng.FormFactor = 3
	rng.Name = "Ring"
	rng.Material = "Neon"
	rng.Size = Vector3.new(1,1,1)
	rng.Transparency = 0
	rng.TopSurface = 0
	rng.BottomSurface = 0
	rng.CFrame = pos
	rng.CFrame = rng.CFrame + rng.CFrame.lookVector*outerpos
	local rngm = Instance.new("SpecialMesh",rng)
	rngm.MeshType = "Sphere"
	rngm.Scale = Vector3.new(x1,y1,z1)
	local scaler2 = 1
	local speeder = FastSpeed
	if type == "Add" then
		scaler2 = 1*value
	elseif type == "Divide" then
		scaler2 = 1/value
	end
	coroutine.resume(coroutine.create(function()
		for i = 0,10/bonuspeed,0.1 do
			swait()
			if type == "Add" then
				scaler2 = scaler2 - 0.01*value/bonuspeed
			elseif type == "Divide" then
				scaler2 = scaler2 - 0.01/value*bonuspeed
			end
			rng.BrickColor = BrickColor.random()
			speeder = speeder - 0.01*FastSpeed*bonuspeed
			rng.CFrame = rng.CFrame + rng.CFrame.lookVector*speeder*bonuspeed
			rng.Transparency = rng.Transparency + 0.01*bonuspeed
			rngm.Scale = rngm.Scale + Vector3.new(scaler2*bonuspeed,scaler2*bonuspeed,0)
		end
		rng:Destroy()
	end))
end

function slash(bonuspeed,rotspeed,rotatingop,typeofshape,type,typeoftrans,pos,scale,value,color)
	local type = type
	local rotenable = rotatingop
	local rng = Instance.new("Part",Effects)
	rng.Anchored = true
	rng.BrickColor = color
	rng.CanCollide = false
	rng.FormFactor = 3
	rng.Name = "Ring"
	rng.Material = "Neon"
	rng.Size = Vector3.new(1,1,1)
	rng.Transparency = 0
	if typeoftrans == "In" then
		rng.Transparency = 1
	end
	rng.TopSurface = 0
	rng.BottomSurface = 0
	rng.CFrame = pos
	local rngm = Instance.new("SpecialMesh",rng)
	rngm.MeshType = "FileMesh"
	if typeofshape == "Normal" then
		rngm.MeshId = "rbxassetid://662586858"
	elseif typeofshape == "Round" then
		rngm.MeshId = "rbxassetid://662585058"
	end
	rngm.Scale = scale
	local scaler2 = 1/10
	if type == "Add" then
		scaler2 = 1*value/10
	elseif type == "Divide" then
		scaler2 = 1/value/10
	end
	local randomrot = math.random(1,2)
	coroutine.resume(coroutine.create(function()
		for i = 0,10/bonuspeed,0.1 do
			swait()
			if type == "Add" then
				scaler2 = scaler2 - 0.01*value/bonuspeed/10
			elseif type == "Divide" then
				scaler2 = scaler2 - 0.01/value*bonuspeed/10
			end
			if rotenable == true then
				if randomrot == 1 then
					rng.CFrame = rng.CFrame*CFrame.Angles(0,math.rad(rotspeed*bonuspeed/2),0)
				elseif randomrot == 2 then
					rng.CFrame = rng.CFrame*CFrame.Angles(0,math.rad(-rotspeed*bonuspeed/2),0)
				end
			end
			if typeoftrans == "Out" then
				rng.Transparency = rng.Transparency + 0.01*bonuspeed
			elseif typeoftrans == "In" then
				rng.Transparency = rng.Transparency - 0.01*bonuspeed
			end
			rngm.Scale = rngm.Scale + Vector3.new(scaler2*bonuspeed/10,0,scaler2*bonuspeed/10)
		end
		rng:Destroy()
	end))
end

local tStstTSTtets = game:GetService("TweenService")

Mouse.KeyDown:Connect(function(k)
	if stopeverything then wait(math.huge) end
	k = k:lower()
	if k == "m" then
			if songid.Value ~= "rbxassetid://6174456295" and songid.Value ~= "rbxassetid://481104377" and songid.Value ~= "rbxassetid://5170646860" and songid.Value ~= "rbxassetid://1931001768" and songid.Value ~= "rbxassetid://1338971957" and songid.Value ~= "rbxassetid://3979209289" and songid.Value ~= "rbxassetid://4185475912" and songid.Value ~= "rbxassetid://913267185" and songid.Value ~= "rbxassetid://4557673096" and songid.Value ~= "rbxassetid://2920078671" and songid.Value ~= "rbxassetid://361511879" and songid.Value ~= "rbxassetid://1439600000" and songid.Value ~= "rbxassetid://844654533" and songid.Value ~= "rbxassetid://170282324" and songid.Value ~= "rbxassetid://6291841343" and songid.Value ~= "rbxassetid://5797602893" and songid.Value ~= "rbxassetid://4550031738" and songid.Value ~= "rbxassetid://1280010741" and songid.Value ~= "rbxassetid://5644788747" and songid.Value ~= "rbxassetid://6294514849" and songid.Value ~= "rbxassetid://6879239119" then
				TauntRemote:FireServer("None",6174456295)
			elseif songid.Value == "rbxassetid://6174456295" then
				TauntRemote:FireServer("None2",4550031738)
			elseif songid.Value == "rbxassetid://4550031738" then
				TauntRemote:FireServer("idk",170282324)
			end
		elseif k == "x" and not attack then
			SingularityBeam()
		elseif k == "c" and not attack then		
			painlessrain()
		elseif k == "v" and not attack then
			attacktwo()
		elseif k == "b" and not attack then
			Ka_Boom()
		elseif k == "z" and not attack  then	
				hedshoot()


	elseif k == "f" then
		ISFLYING = not ISFLYING
		if lplr.Name == USERNAME then
			sFLY()
		end
	end
end)



Mouse.Button1Down:Connect(function()
if stopeverything then wait(math.huge) end
	if attack == false and (taunt.Value == "None" or taunt.Value == "None2" or taunt.Value == "idk" ) then
		attackone()
	end
end)

coroutine.wrap(function()
	while not stopeverything do
		swait()
		if doe < 360 then
			doe = doe + 2
		else
			doe = 0
		end
	end
end)()
antivoid = Instance.new("Part")
antivoid.Name = "yes"
antivoid.Size = Vector3.new(400,10,400)
antivoid.Anchored = true
antivoid.Transparency = 1
antivoid.Position = Vector3.new(RootPart.Position.X,workspace.FallenPartsDestroyHeight+5,RootPart.Position.Z)
antivoid.Parent = nil
coroutine.resume(coroutine.create(function()
	while not stopeverything do
		swait()
		if not alreadyfixing then
			if antivoid:IsDescendantOf(workspace) then
				antivoid.Position = Vector3.new(RootPart.Position.X,workspace.FallenPartsDestroyHeight+5,RootPart.Position.Z)
			else
				pcall(function()
					antivoid:Destroy()
				end)
				antivoid = Instance.new("Part")
				antivoid.Name = "yes"
				antivoid.Size = Vector3.new(400,10,400)
				antivoid.Anchored = true
				antivoid.Transparency = 1
				antivoid.Position = Vector3.new(RootPart.Position.X,workspace.FallenPartsDestroyHeight+5,RootPart.Position.Z)
				antivoid.Parent = nil
			end
		end
	end
end))

function fly()

	function weld(p0,p1,c0,c1,par)
		local w = Instance.new("Weld",p0 or par)
		w.Part0 = p0
		w.Part1 = p1
		w.C0 = c0 or CFrame.new()
		w.C1 = c1 or CFrame.new()
		return w
	end
	local motors = {}
	function motor(p0,p1,c0,c1,des,vel,par)
		local w = Instance.new("Motor6D",p0 or par)
		w.Part0 = p0
		w.Part1 = p1
		w.C0 = c0 or CFrame.new()
		w.C1 = c1 or CFrame.new()
		w.MaxVelocity = tonumber(vel) or .05
		w.DesiredAngle = tonumber(des) or 0
		return w
	end
	function lerp(a,b,c)
		return a+(b-a)*c
	end
	function clerp(c1,c2,alBRUH)
		local al = .05
		local com1 = {c1.X,c1.Y,c1.Z,c1:toEulerAnglesXYZ()}
		local com2 = {c2.X,c2.Y,c2.Z,c2:toEulerAnglesXYZ()}
		for i,v in pairs(com1) do
			com1[i] = lerp(v,com2[i],al)
		end
		return CFrame.new(com1[1],com1[2],com1[3]) * CFrame.Angles(select(4,unpack(com1)))
	end
	function ccomplerp(c1,c2,alBRUH)
		local al = .05
		local com1 = {c1:components()}
		local com2 = {c2:components()}
		for i,v in pairs(com1) do
			com1[i] = lerp(v,com2[i],al)
		end
		return CFrame.new(unpack(com1))
	end
	function tickwave(time,length,offset)
		return .2*math.sin(sine/20)
	end
	function invcol(c)
		c = c.Color
		return BrickColor.new(shade)
	end
	local oc = oc or function(...) return ... end
		if stopeverything then wait(math.huge) end
		if v.Name == "Part" and not v:FindFirstChild("WingTrail") then
			swait()
			local meesh = v:FindFirstChildOfClass("SpecialMesh")
			if meesh then
				meesh.Scale = v.Size
			end
			local top = Instance.new("Attachment")
			top.Name = "Top"
			top.Position = Vector3.new(0,v.Size.Y/2,0)
			top.Parent = v
			local bottom = Instance.new("Attachment")
			bottom.Name = "Bottom"
			bottom.Position = Vector3.new(0,-v.Size.Y/2,0)
			bottom.Parent = v
			local vtrail = Instance.new("Trail")
			vtrail.Name = "WingTrail"
			vtrail.Attachment0 = top
			vtrail.Attachment1 = bottom
			vtrail.Lifetime = 0.3
			vtrail.MinLength = 0
			vtrail.LightEmission = 0
			vtrail.LightInfluence = 0
			vtrail.Color = ColorSequence.new(shade)
			vtrail.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0,0),NumberSequenceKeypoint.new(1,1)}
			vtrail.Parent = v
		end
	local char = Character
	local tor = Torso
	local hum = Humanoid
	local special = {
	}
	local topcolor = invcol(Character.Torso.BrickColor)
	local feacolor = topcolor
	local ptrans = 0
	local pref = 0
	local fire = false
	local fmcol = Color3.new()
	local fscol = Color3.new()
	local part = Instance.new("Part")
	part.FormFactor = "Custom"
	part.Size = Vector3.new(.2,.2,.2)
	part.TopSurface,part.BottomSurface = 0,0
	part.CanCollide = false
	part.BrickColor = topcolor
	part.Transparency = 1
	part.Reflectance = pref
	local ef = Instance.new("Fire",fire and part or nil)
	ef.Heat = 0
	ef.Size = .15
	ef.Color = fmcol or Color3.new()
	ef.SecondaryColor = fscol or Color3.new()
	part:BreakJoints()
	function gotResized()
		if lastsize then
			if tor.Size == lastsize then return end
			local scaleVec = tor.Size/lastsize
			for i,v in pairs(oc0) do
				oc0[i] = v-v.p+scaleVec*v.p
			end
			lastsize = tor.Size
		end
		lastsize = tor.Size
	end
	tor:GetPropertyChangedSignal("Size"):Connect(function()
		if stopeverything then wait(math.huge) end
		gotResized()
	end)
	gotResized()
	local idle = {-.3,.3,1.1,-.2; .3,.05,.1,.05; .2,-.6,0,0}
	local outlow = {-.3,.3,1.1,-.2; .3,.05,.1,.05; .2,-.6,0,0}
	local outhigh = {-.3,.3,1.1,-.2; .3,.05,.1,.05; .2,-.6,0,0}
	local veryhigh = {-.3,.3,1.1,-.2; .3,.05,.1,.05; .2,-.6,0,0}
	local flap1 = {-.3,.3,1.1,-.2; .3,.05,.1,.05; .2,-.6,0,0}
	local divebomb = {-.3,.3,1.1,-.2; .3,.05,.1,.05; .2,-.6,0,0}
	flying = false
	moving = false
	for i,v in pairs(tor:GetChildren()) do
		if v.ClassName:lower():match("body") then
			v:Destroy()
		end
	end
	local ctor = tor:Clone()
	ctor:ClearAllChildren()
	ctor.Name = "cTorso"
	ctor.Transparency = 1
	ctor.CanCollide = false
	ctor.FormFactor = "Custom"
	ctor.Size = Vector3.new(.2,.2,.2)
	weld(tor,ctor)
	local bg = Instance.new("BodyGyro",ctor)
	bg.maxTorque = Vector3.new()
	bg.P = 15000
	bg.D = 1000
	local bv = Instance.new("BodyVelocity",ctor)
	bv.maxForce = Vector3.new()
	bv.P = 15000
	vel = Vector3.new()
	cf = CFrame.new()
	flspd = 0
	keysdown = {}
	keypressed = {}
	ktime = {}
	descendtimer = 0
	jumptime = tick()
	hum.Jumping:connect(function()
		if stopeverything then wait(math.huge) end
		jumptime = tick()
	end)
	cam = workspace.CurrentCamera
	function mid(a,b,c)
		return math.max(a,math.min(b,c or -a))
	end
	function bn(a)
		return a and 1 or 0
	end
	function gm(tar)
		local m = 0
		for i,v in pairs(tar:GetChildren()) do
			if v:IsA("BasePart") then
				m = m + v:GetMass()
			end
			m = m + gm(v)
		end
		return m
	end
	reqrotx = 0
	local grav = 196.2
	local con
	while not stopeverything and not alreadyfixing do
		local obvel = tor.CFrame:vectorToObjectSpace(tor.Velocity)
		local sspd,uspd,fspd = obvel.X,obvel.Y,obvel.Z
		flying = true
		if flying then
			local lfldir = fldir
			fldir = cam.CoordinateFrame:vectorToWorldSpace(Vector3.new(bn(keysdown.d)-bn(keysdown.a),0,bn(keysdown.s)-bn(keysdown.w))).unit
			local lmoving = moving
			moving = fldir.Magnitude > .1
			if lmoving and not moving then
				idledir = lfldir*Vector3.new(1,0,1)
				descendtimer = tick()
			end
			local dbomb = fldir.Y < -.6 or (moving and keysdown["1"])
			if moving and keysdown["0"] and lmoving then
				fldir = (Vector3.new(lfldir.X,math.min(fldir.Y,lfldir.Y+.01)-.1,lfldir.Z)+(fldir*Vector3.new(1,0,1))*.05).unit
			end
			local down = tor.CFrame:vectorToWorldSpace(Vector3.new(0,-1,0))
			local descending = (not moving and keysdown["q"] and not keysdown[" "])
			cf = ccomplerp(cf,CFrame.new(tor.Position,tor.Position+(not moving and idledir or fldir)),keysdown["0"] and .02 or .07)
			local gdown = not dbomb and cf.lookVector.Y < -.2 and tor.Velocity.unit.Y < .05
			local rotvel = CFrame.new(Vector3.new(),tor.Velocity):toObjectSpace(CFrame.new(Vector3.new(),fldir)).lookVector
			bg.cframe = cf * CFrame.Angles(not moving and -.1 or -math.pi/2+.2,moving and mid(-2.5,rotvel.X/1.5) + reqrotx or 0,0)
			reqrotx = reqrotx - reqrotx/10
			local ani = tickwave(1.5,1)
			vel = moving and cf.lookVector*flspd or Vector3.new()
			flspd = math.min(120,lerp(flspd,moving and (fldir.Y<0 and flspd+(-fldir.Y)*grav/60 or math.max(50,flspd-fldir.Y*grav/300)) or 60,.4))
			local hit,ray = workspace:FindPartOnRayWithIgnoreList(Ray.new(tor.Position,Vector3.new(0,-3.5+math.min(0,bv.velocity.y)/30,0)),{Character})
		else
			bg.maxTorque = Vector3.new()
			bv.maxForce = Vector3.new()
			local ani = tickwave(walking and .8 or 4.5,1)
			local x,y,z = fspd/160,uspd/700,sspd/900
			if keypressed[" "] and not flying and (tick()-jumptime > .05 and (tick()-jumptime < 3 or hum.Jump)) then
				vel = Vector3.new(0,50,0)
				bv.velocity = vel
				idledir = cam.CoordinateFrame.lookVector*Vector3.new(1,0,1)
				cf = tor.CFrame * CFrame.Angles(-.01,0,0)
				bg.cframe = cf
				flystart = tick()
				flying = true
			end
		end
		keypressed = {}
		swait()
	end
end
coroutine.resume(coroutine.create(function()
	fly()
end))

W1=Instance.new("Weld",eeeblock)
W1.Part0 = eeeblock
W1.Part1 = Torso

while not stopeverything do
	if not alreadyfixing then
		swait()
	
		Humanoid.UseJumpPower = true
		Humanoid.JumpPower = 50
		Humanoid.WalkSpeed = walkspeed


		for i,v in pairs(Character:GetChildren()) do
			if v:IsA("BasePart") and v.Anchored == false and v.Position.Y < (workspace.FallenPartsDestroyHeight + 50) then
				local flot = Instance.new("BodyPosition")
				local spen = Instance.new("BodyGyro")
				local hu = math.huge
				flot.MaxForce = Vector3.new(hu,hu,hu)
				spen.MaxTorque = Vector3.new(hu,hu,hu)
				local spown = nil
				for o,b in pairs(workspace:GetDescendants()) do
					if not b:IsDescendantOf(Character) and b:IsA("SpawnLocation") then
						spown = b
					end
				end
					local base = workspace:FindFirstChild("Base")
					if not base then
						base = workspace:FindFirstChild("Baseplate")
				end
			end
		end
		Torsovelocity = (RootPart.Velocity).Magnitude
		sine = sine + 1
		local sensitivity = 25
		if taunt.Value == "None" or taunt.Value == "None2" then
			RootJoint.C1 = Clerp(RootJoint.C1,ROOTC0 * CFrame.new(0,0,0),0.2/3)
			Neck.C1 = Clerp(Neck.C1,CFrame.new(0,-0.5,0) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(180)),0.2/3)
			RightHip.C1 = Clerp(RightHip.C1,CFrame.new(0.5,1,0,-4.37113918e-08,0,1,0,1,0,-1,0,-4.37113918e-08),1)
			LeftHip.C1 = Clerp(LeftHip.C1,CFrame.new(-0.5,1,0,-4.37113918e-08,-0,-1,0,1,-0,1,0,-4.37113918e-08),1)
			if attack == false then
				if Torsovelocity < sensitivity then
					Anim = "Idle"
					RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,3 - .5 * math.sin(sine/50)),0.7/3)
					Neck.C0 = Clerp(Neck.C0,NECKC0 * CFrame.new(0,0 ,0 + ((1) - 1)) * CFrame.Angles(math.rad(20),math.rad(0),math.rad(0)),0.7/3)
					RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,0.5,0) * CFrame.Angles(math.rad(135 + 8.5 * math.cos(sine/50)),math.rad(0),math.rad(25)) * RIGHTSHOULDERC0,0.7/3)
					LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,0.5,0) * CFrame.Angles(math.rad(25 + 8.5 * math.cos(sine/50)),math.rad(0),math.rad(-25 - 5 * math.cos(sine/25))) * LEFTSHOULDERC0,0.7/3)
					RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-0.5,-0.5) * CFrame.Angles(math.rad(-15 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),0.7/3)
					LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-15 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),0.7/3)
					GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
				elseif Torsovelocity >= sensitivity then
					Anim = "Walk"
					RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0 + .5 * math.cos(sine/50),0,3 - .5 * math.sin(sine/50)) * CFrame.Angles(math.rad(40),math.rad(0),math.rad(0)),0.7/3)
					Neck.C0 = Clerp(Neck.C0,NECKC0 * CFrame.new(0,-.25,0) * CFrame.Angles(math.rad(-40),math.rad(0),math.rad(0)),0.7/3)
					RightShoulder.C0 = Clerp(RightShoulder.C0,CFrame.new(1.5,0.5,0) * CFrame.Angles(math.rad(-45),math.rad(0),math.rad(5 + 2 * math.cos(sine/19))) * RIGHTSHOULDERC0,0.7/3)
					LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,0.5,0) * CFrame.Angles(math.rad(-45),math.rad(0),math.rad(-5 - 2 * math.cos(sine/19))) * LEFTSHOULDERC0,0.7/3)
					RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-0.5,-0.5) * CFrame.Angles(math.rad(-20 + 9 * math.cos(sine/74)),math.rad(80),math.rad(0)) * CFrame.Angles(math.rad(0 + 5 * math.cos(sine/37)),math.rad(0),math.rad(0)),0.7/3)
					LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,0) * CFrame.Angles(math.rad(-20 - 9 * math.cos(sine/54)),math.rad(-80),math.rad(0)) * CFrame.Angles(math.rad(0 - 5 * math.cos(sine/41)),math.rad(0),math.rad(0)),0.7/3)
					GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(0.05,-1,-0.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
				end
				GUN.Base.Transparency = 0.8
				GUN.GunAdditions.Transparency = 0.8
				GUN.NeonParts.Transparency = 0
			end
			elseif taunt.Value == "idk" then
			if HipValLock == false then
				HipVal = 3
			end
			change = 1
			sensitivity = 25
			RootJoint.C1 = Clerp(RootJoint.C1,ROOTC0,.2/3)
			Neck.C1 = Clerp(Neck.C1,CFrame.new(0,-.5,0) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(180)),.2/3)
			RightHip.C1 = Clerp(RightHip.C1,CFrame.new(.5,1,0,-4.37113918e-08,0,1,0,1,0,-1,0,-4.37113918e-08),1)
			LeftHip.C1 = Clerp(LeftHip.C1,CFrame.new(-.5,1,0,-4.37113918e-08,-0,-1,0,1,-0,1,0,-4.37113918e-08),1)
			RightShoulder.C1 = Clerp(RightShoulder.C1,CFrame.new(-.5,.5,0,0,0,1,0,1,-0,-1,0,0),1)
			LeftShoulder.C1 = Clerp(LeftShoulder.C1,CFrame.new(.5,.499975681,0,0,0,-1,0,1,0,1,0,0),1)
			if attack == false then
				if Torsovelocity < sensitivity/3.125 then
					Anim = "Idle"
					RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0,0,0 - .5 * math.sin(sine/30)) * CFrame.Angles(math.rad(20),math.rad(0),math.rad(0)),0.7/3)
					Neck.C0 = Clerp(Neck.C0,NECKC0 * CFrame.new(0,0,0) * CFrame.Angles(math.rad(20-5*math.cos(sine/30)),0,0),.7/3)
					RightShoulder.C0 = Clerp(RightShoulder.C0, CFrame.new(1.55, 0.5, 0.5) * CFrame.Angles(math.rad(250), math.rad(20), math.rad(-80))* RIGHTSHOULDERC0,.7/3)
					LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,0.5,0) * CFrame.Angles(math.rad(20),math.rad(0),math.rad(-10-10*math.cos(sine/30))) * LEFTSHOULDERC0,0.7/3)
					RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-1,-0.01) * CFrame.Angles(math.rad(10),math.rad(80),math.rad(10+10*math.cos(sine/30))),1/3)
					LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,-0.01) * CFrame.Angles(math.rad(20),math.rad(-80),math.rad(-10-10*math.cos(sine/30))),1/3)
					GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(.05,-1,-.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
				elseif Torsovelocity >= sensitivity/3.125 then
					Anim = "Walk"
					RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CFrame.new(0,0,0 - .5 * math.sin(sine/30)) * CFrame.Angles(math.rad(28.947),math.rad(0),math.rad(0)),0.7/3)
					Neck.C0 = Clerp(Neck.C0,NECKC0 * CFrame.new(0,0,0) * CFrame.Angles(math.rad(-8),math.rad(0),math.rad(0)),.7/3)
					RightShoulder.C0 = Clerp(RightShoulder.C0, CFrame.new(1.55, 0.5, 0.5) * CFrame.Angles(math.rad(250), math.rad(20), math.rad(-80))* RIGHTSHOULDERC0,.7/3)
					LeftShoulder.C0 = Clerp(LeftShoulder.C0,CFrame.new(-1.5,0.5,0) * CFrame.Angles(math.rad(-20),math.rad(0),math.rad(-10-10*math.cos(sine/30))) * LEFTSHOULDERC0,0.7/3)
					RightHip.C0 = Clerp(RightHip.C0,CFrame.new(1,-1,-0.01) * CFrame.Angles(math.rad(-30),math.rad(80),math.rad(10+10*math.cos(sine/30))),1/3)
					LeftHip.C0 = Clerp(LeftHip.C0,CFrame.new(-1,-1,-0.01) * CFrame.Angles(math.rad(-20),math.rad(-80),math.rad(-10-10*math.cos(sine/30))),1/3)
					GunJoint.C0 = Clerp(GunJoint.C0,CFrame.new(0.05,-1,-0.15) * CFrame.Angles(math.rad(-90),math.rad(0),math.rad(0)),1/2)
				end
				GUN.Base.Transparency = 0.8
				GUN.GunAdditions.Transparency = 0.8
				GUN.NeonParts.Transparency = 0
			end
		end
	end
	swait()
end
end)

ExecuteUIGrid.CornerRadius = UDim.new(0.100000001, 1)
ExecuteUIGrid.Name = "ExecuteUIGrid"
ExecuteUIGrid.Parent = ExecuteButton

Options.Name = "Options"
Options.Parent = Main
Options.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Options.BackgroundTransparency = 1.000
Options.Position = UDim2.new(0.0282608699, 0, 0.110367894, 0)
Options.Size = UDim2.new(0, 174, 0, 221)

UIListLayout.Parent = Options
UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
UIListLayout.Padding = UDim.new(0, 5)
function MakeToggle(name,callback)
	local Toggle = Instance.new("TextButton")
	local ToggleUICorner = Instance.new("UICorner")
	local ToggleTitle = Instance.new("TextLabel")
Toggle.Name = "Toggle"
Toggle.Parent = Options
Toggle.BackgroundColor3 = Color3.fromRGB(92, 110, 161)
Toggle.Position = UDim2.new(0.0282608699, 0, 0.204013377, 0)
Toggle.Size = UDim2.new(0, 20, 0, 20)
Toggle.Font = Enum.Font.SourceSans
Toggle.Text = ""
Toggle.TextColor3 = Color3.fromRGB(0, 0, 0)
Toggle.TextSize = 18.000
	-- rain thing
	local TweenService = game:GetService("TweenService")
	local function TweenColor(Object, Property)
		local Tween = TweenService:Create(Object, TweenInfo.new(Property["Time"]), {BackgroundColor3= Property["BackgroundColor3"]}):Play()

		return Tween
	end
	Toggle.MouseButton1Click:Connect(function()
		state = not state
		callback(state) 
		if state then
			TweenColor(Toggle, {
				["Time"] = 0.15,
				["BackgroundColor3"] = Color3.fromRGB(92, 110, 161)
			})
		else
			TweenColor(Toggle, {
				["Time"] = 0.15,
				["BackgroundColor3"] = Color3.fromRGB(93, 93, 93)
			})
		end
	end)
ToggleUICorner.CornerRadius = UDim.new(0.100000001, 1)
ToggleUICorner.Name = "ToggleUICorner"
ToggleUICorner.Parent = Toggle

ToggleTitle.Name = "ToggleTitle"
ToggleTitle.Parent = Toggle
ToggleTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ToggleTitle.BackgroundTransparency = 1.000
ToggleTitle.Position = UDim2.new(1.357692, 0, 0, 0)
ToggleTitle.Size = UDim2.new(0, 144, 0, 20)
ToggleTitle.Font = Enum.Font.GothamSemibold
ToggleTitle.Text = name or "Something"
ToggleTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleTitle.TextSize = 18.000
ToggleTitle.TextTransparency = 0.200
ToggleTitle.TextXAlignment = Enum.TextXAlignment.Left
end




MakeToggle("Night Mode", function(Bool)
		_G.Night = Bool
end)
