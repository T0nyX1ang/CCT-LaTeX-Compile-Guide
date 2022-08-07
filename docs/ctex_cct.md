# 本地CTEX + CCT

**该方法是最简单的本地编译方法.**

!!! info "提前准备的东西"

- SSI提供的[CTEX套装](http://scis.scichina.com/download/CTeX_2.8.0.125_Full.rar), 也可以在CTEX官网下载最新版

- 下载[最新版SSI模板](http://scis.scichina.com/download/ssi-template.zip)至本地

!!! info "编译步骤"

- 打开CTEX自带的`WinEdt`, 选择`Accessories`菜单, 找到`CCT`选项, 点击`CCT-LaTeX`直接编译

- 为了确保交叉引用正确, 需要重复上述步骤, 再次编译文档

!!! tip "该方法的优点"

- 本地编译方式中**最容易**的方法

!!! warning "该方法的不足"

- `CTEX`和`TeX Live`不兼容, 而且`CTEX`中宏包较旧

- ~~一般来说~~, `CTEX`只能用于`Windows`系统

!!! appendix "额外的说明"

- 如果一定要将`CTEX`和`TeX Live`放在一起使用, 推荐将CTEX装入虚拟机中, 以避免兼容性带来的影响, 虚拟机可以选用`VMWare/Virtualbox`
