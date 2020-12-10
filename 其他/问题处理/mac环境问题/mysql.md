- `ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)`

    - `sudo chown -R _mysql:mysql /usr/local/var/mysql`

    - `sudo mysql.server start`
        - 执行失败`ERROR! The server quit without updating PID file`
          - 这一步失败可能是修改的配置有问题原因