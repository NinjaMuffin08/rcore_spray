# rcore_spray
Step 1: Drag folder into resource folder. Then start the resource in server.cfg, "start rcore_spray"

Step 2: Run the sql script, spray

Step 3: Add the following into qb-core/shared/items.lua ...

    -- rcore spray
	["spray"] 					 	 = {["name"] = "spray", 			  	  		["label"] = "Bomboletta Spray", 		["weight"] = 300, 		["type"] = "item", 		["image"] = "spray.png", 				["unique"] = false, 	["useable"] = false, 	["shouldClose"] = false,   ["combinable"] = nil,   ["description"] = "Spray Can"},
	["spray_remover"] 			     = {["name"] = "spray_remover", 			  	["label"] = "Kit rimozione Spray", 		["weight"] = 300, 		["type"] = "item", 		["image"] = "spray_remover.png", 		["unique"] = false, 	["useable"] = true, 	["shouldClose"] = true,    ["combinable"] = nil,   ["description"] = "Spray Remover"},

Step 4: Add the items to a shop of your choice...

    [1] = {
        name = "spray",
        price = 900,
        amount = 50,
        info = {},
        type = "item",
        slot = 1,
    },
    [2] = {
        name = "spray_remover",
        price = 2000,
        amount = 15,
        info = {},
        type = "item",
        slot = 2
    },

# Notify Police with ps-dispatch (Optional)
1) In client/client.lua, add the following Event ... (Line 56)

    RegisterNetEvent('rcore_spray:notifypolice')
    AddEventHandler('rcore_spray:notifypolice', function()
        exports["ps-dispatch"]:CustomAlert({
            coords = GetEntityCoords(PlayerPedId()),
            message = "Graffiti in progress",
            dispatchCode = "10-45",
            description = "",
            radius = 0,
            sprite = 541,
            color = 2,
            scale = 0.8,
            length = 3,
        })
    end)

2) In server/server.lua, add the following line of code on line 46...

    TriggerClientEvent('rcore_spray:notifypolice', source)


