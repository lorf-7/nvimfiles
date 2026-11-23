# nvimfiles

个人 Neovim 配置，基于 [LazyVim](https://github.com/LazyVim/LazyVim) starter，用 lazy.nvim 管理插件。

- 仓库：<https://github.com/lorf-7/nvimfiles>
- 配置目录：`~/.config/nvim`（clone 到这里即可）
- 插件与缓存：`~/.local/share/nvim`、`~/.local/state/nvim`，不入库
- 环境：Neovim 0.12.x（LazyVim 需要 0.10+）

## 安装

```bash
# 如已有旧配置，先挪走
[ -e ~/.config/nvim ] && mv ~/.config/nvim ~/.config/nvim.bak

git clone git@github.com:lorf-7/nvimfiles.git ~/.config/nvim
nvim    # 首次启动会自动安装 lazy.nvim 和全部插件
```

系统剪贴板依赖 `xclip`（X11）或 `wl-copy`（Wayland）；缺失时 yank 会提示没有 provider。

## 目录结构

```
init.lua                 # 入口，只 require config.lazy
lua/config/lazy.lua      # 引导 lazy.nvim 并装配 LazyVim
lua/config/options.lua   # vim 选项（已启用 clipboard=unnamedplus）
lua/config/keymaps.lua   # 自定义快捷键
lua/config/autocmds.lua  # 自定义自动命令
lua/plugins/             # 自定义插件 spec，按文件名自动加载
lazy-lock.json           # 插件版本锁定，必须提交
lazyvim.json             # LazyVim extras 与安装元数据
.neoconf.json            # neodev/lua_ls 的 neoconf 配置
stylua.toml              # Lua 格式化风格
```

## 日常维护

- **加插件**：在 `lua/plugins/` 下新建 `.lua` 文件返回 spec，例如

  ```lua
  return {
    "tpope/vim-surround",
  }
  ```

  lazy.nvim 会自动加载该目录，不需要在 `init.lua` 里手动 import。

- **升级插件**：`:Lazy update` 之后提交锁文件

  ```bash
  cd ~/.config/nvim
  git add lazy-lock.json
  git commit -m "chore: 更新 lazy-lock"
  git push
  ```

- **查看状态**：`:Lazy` 打开管理界面，`:checkhealth` 检查环境。
- **改配置**：直接编辑 `~/.config/nvim` 下的文件，这个目录本身就是 Git 工作区。

## 说明

- 仓库保留了 LazyVim starter 的提交历史和 Apache-2.0 LICENSE，方便追溯来源；
  日常改动直接提交在 `main` 上。
- LazyVim 本体是插件（在 `lazy-lock.json` 里锁版本），升级走 `:Lazy update`，不需要合并 starter 模板。
- 不要提交 `~/.local/share/nvim`、`~/.local/state/nvim` 下的内容。
