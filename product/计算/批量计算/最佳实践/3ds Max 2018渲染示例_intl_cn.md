## 快速开始
本文介绍如何使用批量计算控制台提交一个作业，完成 3ds Max 2018 图片渲染，并导出渲染图片。具体操作步骤如下：
### 一. 制作自定义镜像
1. 制作自定义Windows镜像。
2. 3ds Max 2018 安装流程，参考 [官方主页](https://www.autodesk.com/products/3ds-max/overview)。

> **注意：**
- 请暂时关闭 Windows 防火墙，避免阻止软件下载。
- 参考 [显卡选型指南](https://knowledge.autodesk.com/zh-hans/support/3ds-max/learn-explore/caas/CloudHelp/cloudhelp/2015/CHS/3DSMax/files/GUID-3D6B4C8E-8C0D-4A9C-BFB0-2463803268CE-htm.html) 选择合适的显卡类型，避免显卡初始化失败。无特殊原因，推荐选择“Nitrous Software”。

### 二. 准备渲染文件
渲染素材的主流存储方式有两种：[对象存储](https://intl.cloud.tencent.com/document/product/436) 和 [文件存储](https://intl.cloud.tencent.com/document/product/582)。通过配置挂载参数，Batch 会在渲染作业运行前挂载对象存储或文件存储到本地，渲染器可以像访问本地文件一样访问对象存储或文件存储。

- 渲染素材较小时，推荐将全部素材压缩成 gzip包，上传至对象存储。可参考 [上传对象](https://intl.cloud.tencent.com/document/product/436/6233)。
- 渲染素材较大时，推荐存放在文件存储上。

### 三. 创建任务模板
1. 登录 [批量计算控制台]()，单击左侧导航栏【任务模板】选项，选择目标地域后，单击【新建】按钮。

2. 配置基本信息。示例如下：
![](https://main.qcloudimg.com/raw/cf2f94cec702e0d42abe34b6e0d38bde.jpg)
  * 名称：rendering
  * 描述：3ds Max 2018 Demo
  * 资源配置：S1.LARGE8（4核8G）
  * 资源数量：并发渲染数，比如 1 台
  * 超时时间：默认值
  * 重试次数：默认值
  * 镜像：自定义镜像标识符，比如 img-i64lx84h

3. 配置程序信息。示例如下：
![](https://main.qcloudimg.com/raw/ef7c95752cfb266f855ea0e69436d245.jpg)
  * 执行方式：PACKAGE
  * 程序包地址：以对象存储举例，`cos://barrygz-1251783334.cos.ap-guangzhou.myqcloud.com/render/max.tar.gz`
  * Stdout日志：格式参考 [COS、CFS 路径填写](https://cloud.tencent.com/document/product/599/13996)
  * Stderr日志：同 Stdout 日志
  * 命令行：`3dsmaxcmd Demo.max -outputName:c:\\render\\image.jpg`

4. 配置存储映射。
![](https://main.qcloudimg.com/raw/f5e1836e79852eb5d4c49b917bb870f8.jpg)
  * 输出路径映射-本地路径：`C:\\render\\`
  * 输出路径映射-COS CFS路径：格式参考 [COS、CFS 路径填写](https://cloud.tencent.com/document/product/599/13996)

5. 预览任务 JSON 文件，确认无误后，单击【保存】按钮。

### 四. 提交作业
1. 单击左侧导航栏【作业】选项，选择目标地域后，单击【新建】按钮。

2. 配置作业基本信息。示例如下：
  ![](https://main.qcloudimg.com/raw/7f19ede7710ec960fc4586297213d1fc.jpg)
  * 作业名称：max
  * 优先级：默认值
  * 描述：3ds Max 2018 Demo

3. 选中任务流页面左侧 **rendering** 任务，移动鼠标将任务放置到右侧画布中。

4. 打开任务流右侧 **任务详情**，确认配置无误后，单击【完成】按钮。
![](https://main.qcloudimg.com/raw/00df21802b524cd684f43b68155e3483.jpg)

5. 查询作业运行信息，参考 [查询信息](https://cloud.tencent.com/document/product/599/14567)。

6. 渲染过程演示。
![](https://main.qcloudimg.com/raw/4a0743f3a49045f59c0580deda1529f9.png)

7. 渲染结果查询，参考 [查看对象信息](https://cloud.tencent.com/document/product/436/13326)。
![](https://main.qcloudimg.com/raw/7997d36d8d08e0733fb372dfc6513034.jpg)

## 下一步可以干什么？
本文列举了一个简单的渲染示例，它是一个单实例的作业，仅仅是向用户展示最基本的能力，您可以根据控制台使用指南继续测试 Batch 更高阶的能力。
- **丰富的云服务器配置**：Batch 提供了丰富的云服务器 CVM 配置项，您可以根据业务场景自定义 CVM 配置。
- **远程存储映射**：Batch 在存储访问上进行优化，将对远程存储服务的访问简化为对本地文件系统操作。
- **并行渲染多张图片**：Batch 支持指定并发渲染数，通过 [环境变量](https://intl.cloud.tencent.com/document/product/599/11752) 区分不同的渲染实例，每个渲染实例读取不同的渲染素材，实现并行渲染。
