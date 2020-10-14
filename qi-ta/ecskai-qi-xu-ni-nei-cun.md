
### aliyun ecs 

    sysctl -w vm.swappiness=60
  
### 其他主机

    dd if=/dev/zero of=/mnt/swap bs=1M count=1024
    mkswap /mnt/swap
    swapon /mnt/swap
    sysctl -w vm.swappiness=60
    
   
### 树莓派 
    sudo nano /etc/dphys-swapfile
    CONF_SWAPSIZE=100
    sudo /etc/init.d/dphys-swapfile restart