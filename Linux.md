   
* 删除文件

    
    	rm xxx(文件名)
    
* 删除文件夹（`-r`：向下递归；`-f`：强制删除）


    	rm -rf xxx(文件夹路径)

* 从网上下载文件

    
    	wget http;//…… .tar.gz

* 登录服务器
    
    
    	ssh [-p port] username@servername

* 上传本地文件到服务器
    
    
    	scp [-P port] /path/filename username@servername:/path   


* 上传目录到服务器
 
    
    	scp [-P port] -r local_dir username@servername:remote_dir

* 从服务器上下载文件


    	scp [-P port] username@servername:/path/filename /var/www/local_dir

* 从服务器下载整个目录

    
    	scp [-P port] -r username@servername:/var/www/remote_dir  /var/www/local_dir
