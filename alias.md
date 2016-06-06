##语法：alias [别名]=[指令名称]
##参数：若不加任何参数，则列出所有的别名设置
```bash
[root(0)@yz-lab-563 15:05:29 /home/linanou]# alias
alias check='sh /home/service/client/monitor/health_chk.sh'
alias cp='cp -i'
alias fsh='sh /home/linanou/fsh'
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias mv='mv -i'
alias rm='rm -i'
alias text.sh='sh /home/linanou/text.sh'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
```
####注：alias的效力仅限于此次登录，若想之久话可以设置到~/.bashrc
##例子
```bash
vim ~/.bashrc

alias fsh='sh /home/linanou/fsh'
alias php='/home/service/php/bin/php'
```
