---
title: Fixing "husky" can not run git hooks (node installed by "nvm")
updated: 2026-02-27T11:33:52+07:00
tags:
  - javascript
  - tools
  - husky
  - git
  - dotfiles
---
Part of [[dotfiles|Dotfiles]]
Add file `~/.config/husky/init.sh` 

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```