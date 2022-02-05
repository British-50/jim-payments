# jim-payments
QBCore based payment system

Enchanced QB-Input payment system from my other scripts now free on its own

# Installation

To make use of this payment system you need trigger the event

```jim-payments:client:Charge```

for example with qb-target
```
exports['qb-target']:AddBoxZone("Receipt", vector3(1589.14, 6458.26, 26.01), 0.6, 0.6, { name="Receipt", heading = 335.0, debugPoly=debugPoly, minZ = 26.01, maxZ = 26.81, }, 
{ options = { { event = "jim-payments:client:Charge", icon = "fas fa-credit-card", label = "Charge Customer", job = "popsdiner" } }, distance = 2.0	})
```
It currently requires you to be on duty to charge someone

--------------

To make use of the ticket reward system for workers you need to add the ticket item to your shared items lua:
```
["payticket"] 					 = {["name"] = "payticket", 				["label"] = "Receipt", 	     			["weight"] = 150, 		["type"] = "item", 		["image"] = "ticket.png", 				["unique"] = false,   	["useable"] = false,    ["shouldClose"] = false,    ["combinable"] = nil,   ["description"] = "Cash these in at the bank!"},	
```

Add the ticket image to your inventory script

[qb] > qb-inventory > html > images

--------------
To get tickets from phone invoices you NEED to add it to the event when a payment is accepted:

Go to [qb] > qb-phone > client > main.lua
- Around line 645 there should be the PayInvoice NUICallBack
- Directly under this line:

```TriggerServerEvent('qb-phone:server:BillingEmail', data, true)```

- Add this line:

```TriggerServerEvent('jim-payments:Tickets:Give', amount, society)```