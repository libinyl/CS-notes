## ab

-n : 总的请求数
-c : 并发数
-k : 是否开启长连接


ab -n 10  -c 10  -H 'Content-Type: application/json' -H 'X-Zhiyan-Uid:laryli' http://127.0.0.1:9052/trpc.teg_devops.infra.Infra/AppList