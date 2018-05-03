---
layout: app
---

# Ubuntu Kylin 16.04 BUG及解决方案收集
### appstreamcli错误

在Ubuntu一装好时就存在的bug

解决方法如下：

```sh
sudo pkill -KILL appstreamcli
wget -P /tmp https://launchpad.net/ubuntu/+archive/primary/+files/appstream_0.9.4-1ubuntu1_amd64.deb https://launchpad.net/ubuntu/+archive/primary/+files/libappstream3_0.9.4-1ubuntu1_amd64.deb
sudo dpkg -i /tmp/appstream_0.9.4-1ubuntu1_amd64.deb /tmp/libappstream3_0.9.4-1ubuntu1_amd64.deb
```

### pip升级错误

从pip8升级到pip10后会报错

ImportError: cannot import name 'main'

解决方法如下：

```sh
sudo gedit /usr/bin/pip
```

打开文件后将文件下半部分修改为

```python
from pip import __main__

if __name__ == '__main__':
    sys.exit(__main__._main())
```

保存退出即可
