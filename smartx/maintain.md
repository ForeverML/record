## 清理 prometheus 所占用的磁盘空间
在 leader 节点执行:
```shell
service prometheus stop
sh /usr/share/prometheus/pre_start.sh
rm -rf /mnt/prometheus
sh /usr/share/prometheus/post_stop.sh
service prometheus start
```