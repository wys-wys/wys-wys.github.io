分辨率不能全屏问题
解决办法1：
终端下： sudo pacman -S open-vm-tools
sudo pacman -S gtkmm
sudo pacman -S xf86-video-vmware
sudo pacman -S xf86-input-vmmouse
systemctl enable vmtoolsd

解决方法4：
新增加一个文件重命名为20-screen.conf到etc/X11/xorg.conf.d的下面
1、创建文件： sudo touch 20-screen.conf
2、编辑文件：sudo nano 20-screen.conf
添加以下字段，即：
Section "Screen"
Identifier "Screen0"
Device "Videocard0"
DefaultDepth 24
SubSection "Display"
Viewport 0 0
Depth 24
Modes "1360x768" "1280x768" "1024x768" "800x600" "768x576" "640x480"
EndSubSection
EndSection
3、移动新建文件到目录下：
\# sudo mv 20-screen.conf /etc/X11/xorg.conf.d/
注：在桌面建的文件，就从桌面进。如果需要-r指定文件路径，就加-r
\# sudo mv -r 20-screen.conf /etc/X11/xorg.conf.d/
重启 reboot,重启后就能看到效果了，非常稳定。