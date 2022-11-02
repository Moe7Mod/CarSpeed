local library = loadstring(game:HttpGet("https://pastebin.com/raw/wxmdExdD", true))()
local main = library:CreateWindow("Main")
local speed = 1
local on = false
box = main:Box("Speed multiplier",{type="number"},function(new,old,enter)
   if enter then
       speed = tonumber(new)
   end
end)
box.Text = 1
main:Toggle("On/Off",{},function()
   on = not on
end)
main:Section("Moe7MMod#0701")
local met = getrawmetatable(game)
setreadonly(met,false)
local old = met.__newindex
met.__newindex = function(t,k,v)
   if tostring(t) == "#AV" then
       if not on then return old(t,k,v) end
       if k == "angularvelocity" or k == "maxTorque" then
          return old(t,k,Vector3.new(v.X*speed,v.Y*speed,v.Z*speed))
       end
   end
   return old(t,k,v)
end
