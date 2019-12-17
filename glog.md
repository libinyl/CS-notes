## glog

1. 在编译 gflag 时,一定要在 ccmake 时选中 shared.
2. 在编译 glog 之后,要新增 libglog.conf,并 ldconfig.

https://github.com/google/glog/issues/174

https://github.com/gflags/gflags/blob/master/INSTALL.md


libglog.so.0

cd /etc/ld.so.conf.d/
echo  " /usr/local/lib" >  libglog.conf
ldconfig -v