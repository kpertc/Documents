#programming-language 

[https://www.lua.org/](https://www.lua.org/)

> Lua(pronounced **LOO-ah**), 就是单纯的葡萄牙语中的月亮("Moon")

> 适合游戏开发 C语言 胶水语言 热更 即使编译 JIT 体积小
> 5.4.3的压缩包压缩的话只有350K, 不压缩只有1.3M


```lua
-- comment
```

```lua
--默认全局变量 
a = 1 

--局部变量 添加local 
local a = 1 

-- 没被声明的搜都是 
nil
```

```lua
-- assigning multiple variable
a,b = 1,2
```

String支持转译字符
中括号 原始字符

a..b 连接
转换

```lua
tostring()
tonumber()
```

```lua
-- length of string
a = ‘asdasd’

print(#a) -- 6

-- ASCII to string
s = string.char(0x30, 0x31, 0x32, 0x33) -- 0123

string.byte(s.2)
```

```lua
function functionname (…)
	— body
end

-- default return nil

function functionname (a,b,c)
	print(a,b,c)
	return a,b,c -- define return
end
```

```lua
t:a() 
t.a(t)
```

### Table
```lua
a = {1, "a", {}, function() end} -- any type

-- Get value, lua start from 1
a[1] 

-- write value
a[1] = 123 

-- length
print(#a)

-- insert
table.insert(a, "d")
table.insert(a,2,"d") -- insert 'd' at 2nd position

-- remove
table.remove(a, 2) -- remove 2nd value
removedValue = table.remove(a, 2) -- remove value will be returned
```

```lua
a = {
	a = 1,
	b = "1234",
	c = function () end,
	d = 123123,
	[",;"] = 123
}

print(a["a"]) --1
print(a.a) --1
print(a[",;"]) --123

a["a"] = 2
```

### 全局变量
```lua
a = 1

_G[a] --1
_G["table"]["insert"] 
```

Condition
```lua
a = true
b = false

0 → true
nil → false

1>2
1<2
1>=2

a ~= b -- not equal

a and b
a or b 
not a 
```

```lua
if 1>10 then
	print("1")
elseif 1<10 then
	print("2")
else
	print("3")
end

-- ternary
b > 10 and "yes" or "no"
```

### Loop
```lua
-- 1-10 loop
for i=1, 10 do
	print(i)
end

-- 1 3 5 7 9 loop
for i=1, 10, 2 do
	print(i)
end

-- "break" loop
for i=1, 10 do
	if i = 5 then break end
end
```

```lua
-- while loop

local n = 10
while n > 1 do
	n = n - 1 -- no -- += in Lua
end

while n > 1 do
	if n == 5 then break end -- break in while loop
	n = n - 1
end
```

### math
```lua
math.sin(time)
```