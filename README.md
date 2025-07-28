
# QNAP8528 内核模块（容器化编译版）  


源项目 [0xGiddi/qnap8528](https://github.com/0xgiddi/qnap8528)

源容器化编译项目 [gzxiexl/qnap8528](https://github.com/gzxiexl/qnap8528)

---
按照源项目的说明，给脚本添加了`skip_hw_check=true`参数，同时去掉了源项目脚本里的特殊符号。

在TS-464C2上测试通过。

```
greetingsyi@FnOS:~/qnap8528$ sudo ./build.sh
正在构建 Docker 镜像 (qnap8528-compiler)...
[+] Building 19.9s (8/8) FINISHED                                                                         docker:default
 => [internal] load build definition from Dockerfile                                                                0.0s
 => => transferring dockerfile: 448B                                                                                0.0s
 => [internal] load metadata for docker.io/library/debian:bookworm                                                  0.0s
 => [internal] load .dockerignore                                                                                   0.0s
 => => transferring context: 2B                                                                                     0.0s
 => [1/4] FROM docker.io/library/debian:bookworm                                                                    0.0s
 => [2/4] RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list.d/debian.sources                0.4s
 => [3/4] RUN apt-get update && apt-get install -y --no-install-recommends     gcc     make     build-essential    16.0s
 => [4/4] WORKDIR /driver                                                                                           0.0s
 => exporting to image                                                                                              3.3s
 => => exporting layers                                                                                             3.3s
 => => writing image sha256:c0cfc935b18e5ebb52b91a2d48a113766c21729628809137d7d843a4670b8771                        0.0s
 => => naming to docker.io/library/qnap8528-compiler                                                                0.0s
镜像构建成功
启动 Docker 容器...
cad4e922ee859e46723def6042f2c230a3a950005e3a4f1a46e59f518220f9f2
开始编译内核模块...
make: Entering directory '/usr/src/linux-headers'
warning: the compiler differs from the one used to build the kernel
  The kernel was built by: gcc (Debian 12.2.0-14) 12.2.0
  You are using:           gcc (Debian 12.2.0-14+deb12u1) 12.2.0
  CC [M]  /driver/qnap8528.o
  MODPOST /driver/Module.symvers
  CC [M]  /driver/qnap8528.mod.o
  CC [M]  /driver/.module-common.o
  LD [M]  /driver/qnap8528.ko
make: Leaving directory '/usr/src/linux-headers'
编译成功
安装驱动到系统...
驱动 qnap8528 已加载
Created symlink /etc/systemd/system/multi-user.target.wants/qnap8528-load.service → /etc/systemd/system/qnap8528-load.service.
已配置开机自动加载
清理临时容器...
检测传感器数据...
qnap8528 传感器信息：
qnap8528-isa-0000
Adapter: ISA adapter
fan1:         892 RPM
temp1:        +47.0°C
temp6:        +40.0°C
temp11:        +2.0°C
temp16:       -19.0°C

```