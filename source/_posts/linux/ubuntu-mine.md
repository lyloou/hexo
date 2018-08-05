## 设置管理员密码
首次使用管理员登录需要先设置密码
```sh
sudo passwd
```


## [自动挂载E盘](https://askubuntu.com/questions/46588/how-to-automount-ntfs-partitions)
- `vi /etc/fstab` & add below line
```sh
#Windows-Partition
UUID=0004D1FE0007434B /home/lou/e ntfs rw,auto,users,exec,nls=utf8,umask=003,gid=46,uid=1000    0   0
```
- Finding which disk you will set
```sh
sudo fdisk -l
```
- Finding the UUID
```sh
sudo blkid
```
- Check it
```
sudo mount -a
```

## 软件
设置image:
```
http://mirros.aliyun.com/ubuntu
```

```
sudo apt-get update
sudo apt-get install terminator

sudo add-apt-repository ppa:synapse-core/ppa
sudo apt-get update
sudo apt-get install synapse

sudo apt install vlc
```