# Plane
a 2 dimensional plane of cells that you can set and get the state of.

When creating a 2 diensional array to hold states you would usually do something like this..
```Lua

local width =50
local height = 20
local plane = {}

for r = 1, height do -- create a new 2 dimensional plane
  local row = {}
  for c = 1, width do
    row[#row + 1] = false
  end
  plane[#plane + 1] = row
end

array[4][7] = true -- set cell state
local state = array[6][14] -- get cell state
```
There are two issues here..
1. If you have very large dimensions, you are creating a giant table of cells, some of which might never be accessed.
2. You can't use negative coordinates when accessing this array.

My solution...
```Lua
local plane = Plane.new() -- create a new 2 dimensional plane

plane:set(10, 10, true) -- set cell state
local state = plane:get(50, 16) -- get cell state
 ```
Does that just seem a lot more intuitive and easier to read?

When initially created the plane is just an empty table. When you set a cell in the plane that cell is then created on the fly, so the table grows in size only when you set any cells state.

The plane class also maintains an internal offset so you can supply negative coordinates without breaking anything.
