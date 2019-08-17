## 配置脚本

默认配置文件名是以`.conf`开头的.

```
sudo apt install libx11-dev
sudo apt-get install libxrandr-dev
sudo apt-get install libgtk2.0-dev


./configure --enable-debugger --enable-disasm --enable-debugger-gui --with-x11
make
sudo make install
```
