## kill

ps aux |grep curl |awk '{print $2}'|xargs kill -9