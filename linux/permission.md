---
layout: page
category: linux
name: permission
title: 文件权限
---

* owner/group/others/all (u/g/o/a)
* r/w/x/- (4/2/1/0) 
* directory/regularfile/link/block/character (d/-/l/b/c) 
* chgrp/chown/chmod 
* +/-/= 

* owner:所有者,group:所属组,others:其他用户，all:所有人 
* 对于文件:{r:可读,w:可写,x:可执行,-:无权限} 
* 对于目录:{r:可列出目录中的内容,w:可在目录中创建、删除和修改文件,x:可使用cd命令切换到此目录,-:没有任何此目录的访问权限} 
* chgrp:修改用户所属组，chown：修改文件所有者，chmod:修改文件权限 

* -rwxr-xr-x 
* 1-1位表示文件类型，-表示文件，d表示目录 
* 2-4位表示文件所有者的权限，u权限 
* 5-7位表示文件所有者所属组成员的权限，g权限 
* 8-10位表示所有者所属组之外的用户的权限，o权限 
* 2-10位的权限总和有时称为a权限 

* chmod:数字表示法,文本表示法 
* chmod文本表示法中可用:{=：重新制定权限,-：对目前的设置减少权限,+：对目前的设置增加权限} 

* chgrp root demo 
* chgrp -R root demo 
* chown root demo 
* chown -R root demo 
* chown root:root demo 
* chmod 750 demo 
* chmod -R 310 demo 
* chmod u=rwx,go=r demo 
* chmod u+x,g-w demo

