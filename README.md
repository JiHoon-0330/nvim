# nvim 설정

### 테마 설정
- `~/.config/nvim/lua/plugins/theme.lua` 경로에 추가
```lua
return {
  -- rose-pine 플러그인 설치
  {
    "rose-pine/neovim",
    name = "rose-pine",
    lazy = false, -- 에디터 시작 시 바로 로드
    priority = 1000, -- 다른 플러그인보다 먼저 로드
    config = function()
      require("rose-pine").setup({
        variant = "moon", -- moon 버전 적용
        disable_background = true, -- 터미널 배경과 일치시키고 싶다면 true
      })
      -- 테마 적용 명령어 실행
      vim.cmd("colorscheme rose-pine")
    end,
  },
}
```

### 복사 설정
- space + ff
- `options.lua` 파일에 추가
```lua
vim.opt.clipboard = "unnamedplus"
```

### im-select 설정하기
- [https://github.com/daipeihust/im-select](https://github.com/daipeihust/im-select)
- `~/.config/nvim/lua/plugins/im-select.lua` 경로에 추가
```lua
return {
  {
    "keaising/im-select.nvim",
    config = function()
      require("im_select").setup({
        default_command = "/opt/homebrew/bin/im-select",
        default_im_select = "com.apple.keylayout.ABC",
        set_previous_im = true,
      })
    end,
  },
}
```

### hammerspoon 설정하기
- `brew install --cask hammerspoon`
- `~/.hammerspoon/init.lua` 경로에 추가
```lua
local appWatcher = hs.application.watcher.new(function(appName, eventType, appObject)
    if (eventType == hs.application.watcher.activated) then
        if (appName == "Ghostty") then
            hs.execute("/opt/homebrew/bin/im-select com.apple.keylayout.ABC")
        end
    end
end)

appWatcher:start()
```
