# 使用自动化构建模型

Ku+
MLOps提供了自动化建模方式，无需关注模型选型、参数调整等开发细节，仅需两步即可完成一个AI开发项目。以创建图像分类为例。

步骤1：准备数据

步骤2：创建项目，训练模型

步骤3：将模型部署上线

步骤4：服务调用

**步骤1：准备数据**

Ku+
MLOps在【数据】-【公开数据集】中提供了可直接用于训练的平台预置数据集，本文操作示例使用此数据集进行模型训练。如果您想使用自己的数据集，具体操作参考4.2、4.3。

**步骤2：创建项目，训练模型**

1. 在Ku+ MLOps平台，单击左侧导航栏【项目】-【我的项目】。

2. 单击“新建项目”，填写项目名称、项目类型和项目简介等信息。项目类型选择自动化。

**![C:\\Users\\WANGQI\~1\\AppData\\Local\\Temp\\1631784893(1).png](media/f0ba79b4c7307f39c00650e8620c3661.png)**

1. 单击“创建项目”，跳转至【场景选择】页面，选择“图像分类”应用场景、“通用图像分类”子应用场景。

![C:\\Users\\WANGQI\~1\\AppData\\Local\\Temp\\1631785402(1).png](media/850273e0851a3c65166589e201d0edc1.png)

1. 单击“下一步”，跳转至【数据准备】页面，选择平台的公开数据集“图像分类”

![C:\\Users\\WANGQI\~1\\AppData\\Local\\Temp\\1631785446(1).png](media/bfdbe8433d3c4c1d5545d4b83591c1cf.png)

1. 单击“下一步”，跳转至【任务提交】页面，确认信息后，单击“提交训练”，完成图像分类项目创建。

![C:\\Users\\WANGQI\~1\\AppData\\Local\\Temp\\1631785473(1).png](media/e275b6df396c8f3176242b27d59ba4b1.png)

1. 训练时间相对较长，请耐心等待。训练完成后，可以在【项目详情】页面查看“项目评估”，如“准确率”、“F1-score”、“精确率”、“召回率”。

![C:\\Users\\WANGQI\~1\\AppData\\Local\\Temp\\1631785632(1).png](media/bc5e9f7a39e17347f93817950394474e.png)

**步骤3：将模型部署上线**

1. 当项目详情的历史任务区域，状态为“已完成”时，单击“发布”。

![C:\\Users\\WANGQI\~1\\AppData\\Local\\Temp\\1631785775(1).png](media/c8abb2ebf57ad57cf85ee1ea1eaa370e.png)

1. 在【发布】信息填写页面，填写服务名称和接口地址信息，单击“服务发布”，将模型发布上线。

![C:\\Users\\WANGQI\~1\\AppData\\Local\\Temp\\1631785842(1).png](media/0958f99ac08494d4c0a8b8aff9849f33.png)

**步骤4：服务调用**

1. 发布通过审核后，即可在【概览】-【在线服务】中进行服务调用操作。

![C:\\Users\\WANGQI\~1\\AppData\\Local\\Temp\\1631785889(1).png](media/86024c2375f9a3aee547e5e61e81588d.png)

1. 单击“服务调用测试”，填写参数；若为图片类参数，可单击“Base64转换工具”进行格式转换，将转换后的内容填入框内。

![C:\\Users\\WANGQI\~1\\AppData\\Local\\Temp\\1631785929(1).png](media/bb87365cab64e9c2da82f7960965b912.png)

![C:\\Users\\WANGQI\~1\\AppData\\Local\\Temp\\1631785964(1).png](media/c1a5815b1c43aedf3dd20d7c168b3a7b.png)

1. 单击“测试”，可在【调试信息】区域看到测试结果。

![C:\\Users\\WANGQI\~1\\AppData\\Local\\Temp\\1631786000(1).png](media/02f7106b8b14b27b53095e1beda6213f.png)



---

如果您对产品有使用或者其他方面任何问题，欢迎联系我们

---
