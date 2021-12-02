# Share folder over network using NFS (Network File Sharing)

Sharing a folder over network without password on Ubuntu machines
Help provided from [cloud.netapp blog](https://cloud.netapp.com/blog/azure-anf-blg-linux-nfs-server-how-to-set-up-server-and-client) and [dummies.com](https://www.dummies.com/computers/operating-systems/linux/how-to-share-files-with-nfs-on-linux-systems/)

## On the server
Install the NFS server utilities
```
sudo apt-get update
sudo apt install nfs-kernel-server
```
Give access to everyone to the folder to be shared if not done already
```
sudo chmod 777 /pathtomyshareddir #everyone can modify files
```
Then, modify the file `\etc\exports` with the following:
```
/pathtomyshareddir 192.168.1.24(ro,sync) _host2_(_options_) ...
```
see more options on  [dummies.com](https://www.dummies.com/computers/operating-systems/linux/how-to-share-files-with-nfs-on-linux-systems/)

Finally, start the server for the updated  
```
sudo exportfs -a                         #making the file share available
sudo systemctl restart nfs-kernel-server #restarting the NFS kernel
``` 

## On the client

Install the NFS utilities
```
sudo apt update
sudo apt install nfs-common
```

Create the folder to mount the shared folder
```
sudo mkdir /path/foldername
```

Mount the shared folder at the desired location
```
sudo mount -t nfs {IP of NFS server}:{folder path on server} /path/foldername
```

To mount the folder after reboot, update the `\etc\fstab` file
```
{IP of NFS server}:{folder path on server} /path/foldername nfs defaults 0 0
```




