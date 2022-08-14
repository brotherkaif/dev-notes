# GAMEDEV: Love2d Getting Started

## Resources
- [Learn How to Make Games! DevJeeper](https://youtube.com/playlist?list=PL1A1gsSe2tMzxf54D1OooafEnADpjZlP7) 
## Installation/Setup
1. Install via [love2d.org](https://love2d.org)
2. Launch to see "no game" screen

## Folder Structure
Love2D searches the supplied directory for a `main.lua` file. At a minimum, the structure is as follows:
```(bash)
game-directory/
├── conf.lua
└── main.lua
```

To execute the above example: `love path/to/game-directory`

## Config Structure
Sample of `conf.lua`:
```(lua)
function love.conf(t)
	t.title = "title"				-- The title of the window the game is in (string)
	t.version = "11.3"			-- The LOVE version this game was made for (string)
	t.console = true				-- Attach a console (boolean, Windows only)
	t.window.width = 1280		-- The window width (number)
	t.window.height = 720		-- The window height (number)
end
```

## Main Structure
Sample of `main.lua`:
```(lua)
function love.load()
  -- triggers when you start the game
  -- this is where you want to load all your data and assets
end

function love.update(dt)
	-- where you will program the actual game logic
	-- triggers one time per frame
	-- `dt` gives you delta time to deal with frame variance
end

function love.draw()
	-- used to display graphics on the screen
end
```
