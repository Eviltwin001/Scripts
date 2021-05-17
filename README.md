wait(15)
repeat wait() until game:IsLoaded()

local LocalPlayer = game.Players.LocalPlayer
local HRootPart = LocalPlayer.Character.HumanoidRootPart

spawn(function()
while wait(5) do 

local args = { [1] = "MouseButton1"}
game:GetService("ReplicatedStorage").Events.CoolNewRemote:FireServer(unpack(args))

local args = {[1] = "TBC"}
game:GetService("ReplicatedStorage").Events.JoinTeam:FireServer(unpack(args))

end 
end)

spawn(function()
while wait() do 
    for i,v in pairs(workspace.Bananas:GetChildren()) do
        	if v:IsA("MeshPart") and v.Transparency ~= 1 then
        	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.CFrame
        	wait(2)
             end
         end
     end
end)

wait(30)
local x = {}
	for _, v in ipairs(game:GetService("HttpService"):JSONDecode(game:HttpGetAsync("https://games.roblox.com/v1/games/" .. game.PlaceId .. "/servers/Public?sortOrder=Asc&limit=100")).data) do
		if type(v) == "table" and v.maxPlayers > v.playing and v.id ~= game.JobId then
			x[#x + 1] = v.id
		end
	end
	if #x > 0 then
		game:GetService("TeleportService"):TeleportToPlaceInstance(game.PlaceId, x[math.random(1, #x)])
	else
		return notify("Serverhop","Couldn't find a server.")
	end

--
