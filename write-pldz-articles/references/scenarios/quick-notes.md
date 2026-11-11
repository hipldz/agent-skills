# 简短笔记 / 局部配置

**什么时候读：** 只有一条设置、几行操作、一个随手记下的取舍，或一篇尚未展开的短文。

原始文章中确实有只用一句话完成目的的情形，也有用两类选项加一句选择便结束的情形。简短是有效的内容形态，不是需要补全的残缺教程。

## 内置原文案例

### 一行配置就是正文

**节选出处：**《VSCode相关配置》；原文文字已收录在下方，无需寻找完整文章。

原文连续节选（直接收录在本文件中；原图未打包）：

````markdown
## 视图折叠

〔此处原文有配图；图片未收录〕

`editor.stickyScroll.enabled`，默认是 true，改为 false 即可

## 快捷键

- Go Back

〔此处原文有配图；图片未收录〕

- Find all reference

〔此处原文有配图；图片未收录〕
````

**这段体现的写作动作：** 在截图之后直接说设置项，后面又列两个快捷键截图；没有安装步骤、效果评测或总结。这就是合理的篇幅。



### 区分两类方法，落到自己的选择

**节选出处：**《2_1_1_ROS2_Arduino》；原文文字已收录在下方，无需寻找完整文章。

原文连续节选（直接收录在本文件中；原图未打包）：

````markdown
ROS2 和 Arduino 的通讯方式有很多，个人觉得只要分为两大类

1. 第一类是采用 ros2arduino 或者 MicroROS 这类的包，在 arduino 板卡上尝试直接进行 ros2 的节点的发布和订阅, 然后主机上则采用对应的 DDS 工具 例如 MicroROS 的各种通讯中间件，Mirco_XRCE_DDS 图像中间件，或者是 ros2_serial 获取发布订阅的串口数据的中间件

2. 直接从微控制器本身出发，Arduino 直接烧录自身的功能代码 而不依赖仍和 ROS2 相关的库，然后用 Python 或者 C/C++编写接受串口消息的节点，做发布和订阅

〔此处原文有配图；图片未收录〕

那么这里就采用第二种方式，最简单快速的完成 ROS2 和 Arduino 的通讯
````

**这段体现的写作动作：** 作者将方案粗略分为两类，选第二种，随后就结束。分类本身是当时作者的理解，不等于客观上只有两类。



### 随手记录一个已有工具的实际操作

**节选出处：**《体验code-server》；原文文字已收录在下方，无需寻找完整文章。

原文连续节选（直接收录在本文件中；原图未打包）：

````markdown
## 1. 安装code-server

### 1.1 使用安装包

#### 1. 前置条件

- 已安装 Node.js (v12 及以上) 和 npm。  
- Linux 下需安装 C/C++ 编译环境（如 Debian/Ubuntu: `sudo apt install -y build-essential python3`），以编译原生模块。

#### 2. 安装命令


1. 设置版本, 可以在 [https://github.com/coder/code-server/releases](https://github.com/coder/code-server/releases) 查看最新的 release 版本号.

```bash
export VERSION=4.102.2
```

〔此处原文有配图；图片未收录〕


2. 下载解压

```bash
mkdir -p ~/.local/lib ~/.local/bin

curl -fL https://github.com/coder/code-server/releases/download/v$VERSION/code-server-$VERSION-linux-amd64.tar.gz \
  | tar -C ~/.local/lib -xz
```


3. 配置路径和快捷访问

```bash
mv ~/.local/lib/code-server-$VERSION-linux-amd64 ~/.local/lib/code-server-$VERSION

ln -s ~/.local/lib/code-server-$VERSION/bin/code-server ~/.local/bin/code-server

PATH="~/.local/bin:$PATH"
```

4. 测试

```bash
code-server

# Now visit http://127.0.0.1:8080. Your password is in ~/.config/code-server/config.yaml
```
````

**这段体现的写作动作：** 虽然比一行配置长，但依然围绕“怎样装”直接组织命令，不需要先讲 IDE 的发展史。



## 抽象成动作，而不是模板

优先保留明确操作、所需条件和实际参数。用户只要求备忘录，就允许只有一句说明或几条命令。若最小操作本身有风险，再补必要的范围与注意事项，不为文章“完整”扩字数。

## 误用提醒

勿把来自文章元数据的「publish」或图片存在感当作文章必须长的理由；别把未提供的截图、测试结果硬塞进便签。
