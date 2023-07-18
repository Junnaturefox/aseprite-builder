# aseprite-window-x64-builder
这是两个 GitHub Actions 的自动化 workflow, 自动或半自动为 Windows 构建 x64 位的 Aseprite.
通过使用 GitHub 操作, 无需手动编译, 并且不包含恶意软件.

请在使用前查看 [Aseprite 的 EULA](https://github.com/aseprite/aseprite/blob/main/EULA.txt).

为了遵守 Aseprite 的 EULA, 此 workflow 不会将编译后的二进制文件上传到公共可访问空间. 编译后的二进制文件将存储于`Releases`的`draft`仅供仓库所有者可见. 

编译后的二进制文件因为缺失`libcrypto-1_1-x64.dll`无法正常运行, 目前以个人能力不知道如何在编译时解决. workflow将会从<https://github.com/feenkcom/libopenssl/releases>获取缺少的dll并且一并打包, 如果不需要可根据情况自习更换, 删除或者修改workflow.

# 使用方法

Fork 本仓库, 打开Fork仓库的`Setting-Actions-General`页面, 确保`Workflow permissions`选择了`Read and write permissions`. 

## 手动构建

访问<https://github.com/aseprite/aseprite/releases>, 获得欲构建的`Release`对应`tags`. 接着打开Fork仓库的`Actions`页面, 左侧选择`手动构建`workflow, 点击`Run workflow`然后将刚刚获得的`tags`填写在`Release对应的tags`提示下方, 点击`Run workflow`后等待`workflow`执行完毕. 打开Fork仓库的`Code-Releases`, 在刚刚生成的`draft`下方的附件处下载.

## 自动检查更新与构建

如果Fork仓库当前版本与Aseprite的最新Releases不同, 则自动获取最新tags然后执行编译并且在Fork仓库的`Code-Releases`生成`draft`.

`自动检查更新与构建`workflow会在UTC(协调世界时)`0:00`, 及北京时间(UTC+8)`8:00`时自动执行, 如需启用请编辑`.github/workflows/auto-build.yml`, 将第三行到第五行的注释取消:
~~~
on:
  schedule:
  - cron: '0 0 * * *'
~~~