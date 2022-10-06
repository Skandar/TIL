# Вывод название текущей git ветки в prompt терминала (zsh)

Вывести имя ветки в prompt терминала можно добавив скрипт в `~/.zshrc`.

```sh
function parse_git_branch() {
    git branch 2> /dev/null | sed -n -e 's/^\* \(.*\)/[\1] /p'
}
#
COLOR_DEF=$'%f'
COLOR_USR=$'%F{243}'
COLOR_DIR=$'%F{197}'
COLOR_GIT=$'%F{39}'
setopt PROMPT_SUBST
export PROMPT='${COLOR_USR}%n ${COLOR_DIR}%2~ ${COLOR_GIT}$(parse_git_branch)${COLOR_DEF}$ '
```

## Ссылки

- [Add Git Branch Name to Terminal Prompt (MacOS Catalina zsh)](https://gist.github.com/reinvanoyen/05bcfe95ca9cb5041a4eafd29309ff29?permalink_comment_id=4117181#gistcomment-4117181)
