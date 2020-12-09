## 执行`docker-compose up -d redis mysql nginx workspace`失败总结
- `127` git bash中进到laradock目录，vim source.sh,`:set ff=unix :wq`
- `2` 去`https://www.ipaddress.com/`获取`raw.githubusercontent.com`的真实IP配置到hosts中
- `1` 翻墙
- `100` 重启`docker` 
- laradock_nginx启动失败，端口占用。我的是valet占用端口，valet stop