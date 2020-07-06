# 任务式

欢迎您来到京东智联云NeuFoundry一站式AI开发平台，为了您的快捷使用，请先登录注册京东智联云账号并开通使用权限。


## 一、任务式简介  

## 二、任务式操作描述  

登录系统后,左侧菜单依次点击"项目"-"我的项目"进入项目列表页,如下图:  
![avatar](../../../../image/AI-and-Machine-Learning/NeuFoundry/train.screenshotscreenshot/项目列表页.png)  
创建项目点击右上角"新建项目"按钮,进入项目新建页:如下图  
![avatar](../../../../image/AI-and-Machine-Learning/NeuFoundry/train.screenshotscreenshot/项目新建页.png)  
项目创建页各选项说明:  

    项目名称: 支持中文、英文字母、数字及下划线
    项目类型:  
        1.任务式：使用者将算法程序以一个文件或者一个zip文件压缩包的方式，通过浏览器上传到平台，以此来进行模型训练。
        2.NoteBook：Jupyter Notebook是一个交互式笔记本，支持运行多种编程语言。 本系统中特指使用Jupyter NoteBook
          的方式进行算法代码编写，模型训练任务提交，以及结果查看等操作。
        3.图形化拖拽：系统将常用的算法、流程控制等程序代码封装成组件，使用者通过拖拽和链接组件构建模型训练流程。
        4.自动化：使用者不用写任何代码，通过选择相应的使用场景，以及对应的数据集，系统自动进行训练。
        注意：
            1.图形化拖拽和自动化内置的算法及场景有限，具体支持类型可见产品文档
            2.如有算法文件或可编写算法代码，建议使用任务式和NoteBook
    引擎框架:共12种引擎框架
    编程语言:2种编程语言
    项目简介:自由填写项目相关信息
    关联数据集:
        1.可选数据集:可查看公开数据集以及个人上传数据集
        2.已选数据集:项目关联进行开发训练的相关数据集
        3.添加/移除：勾选"可选数据集"点击添加，将勾选数据集选入到"已选数据集"，
          勾选"已选数据集"点击移除，将勾选数据集取消到"可选数据集"。
    注:创建项目页中部分选项框为联动式，如任务式选项不同，会展现不同选项。选择引擎框架后，才可选择编程语音选项。
本示例为创建任务式项目，任务式项目需要上传一个或多个算法文件的压缩包，最大支持10MB大小文件，任务式新建项目信息如下图： 
![avatar](../../../../image/AI-and-Machine-Learning/NeuFoundry/train.screenshotscreenshot/任务式新建信息.png)  
相关信息填写完成后，点击右上角"创建项目"，项目创建成功后跳转到项目详情页，如下图：  
![avatar](../../../../image/AI-and-Machine-Learning/NeuFoundry/train.screenshotscreenshot/任务式项目详情页.png)  
项目详情页中存在可操作项，如：  

    任务式示例区域：显示项目相关信息，点击引擎框架/编程语言可重新选择相关引擎和编程语言。点击项目简介图标，可编辑项目简介信息
                   任务示例区域右上角图标分别为项目公开（项目权限公开，方便平台交流）、项目删除、项目克隆，注意：项目公开和项目删除为不可逆操作！
    关联数据集区域：显示项目关联数据集相关信息，点击"管理数据集"按钮，可重新选择任务关联数据集。
    历史任务区域：显示任务的历史操作记录，以及可对相关操作记录进行进一步的操作。
        下载输出：下载运行完成后的任务输出结果。
        查看日志：查看运行完成的任务运行日志。
        终止任务：停止正在运行的任务
        编辑：编辑当前任务脚本，可重新提交项目。
项目详情页右上角点击"进入项目"，进入项目脚本编辑页。将Readme.txt文件中指定变量,复制到textcnn_train.py文件中指定位置处，
并右键点击textcnn_train.py将其设置为主文件，如下图：
![avatar](../../../../image/AI-and-Machine-Learning/NeuFoundry/train.screenshotscreenshot/任务式项目编辑1.png)  
![avatar](../../../../image/AI-and-Machine-Learning/NeuFoundry/train.screenshotscreenshot/任务式项目编辑2.png)  
![avatar](../../../../image/AI-and-Machine-Learning/NeuFoundry/train.screenshotscreenshot/任务式项目编辑3.png)  
脚本编辑完成后，点击右上角"提交项目"，弹出任务式运行环境，如下图：  
![avatar](../../../../image/AI-and-Machine-Learning/NeuFoundry/train.screenshotscreenshot/任务式运行环境.png)  
选择相应运行环境，点击"提交任务"，任务开始执行。

---

如果您对产品有使用或者其他方面任何问题，欢迎联系我们

---
