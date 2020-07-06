# 乳腺癌预测

#### 1.数据集介绍
数据集选自UCI机器学习库，数据的特征值从乳腺肿块的细针穿刺(FNA)数字化图像中计算出来的，描述了细胞核的特征，数据集包含569个样本，样本包含30特征
这30个特征值实际上是由10个特征值计算而来  


#### 2.整体流程

**1）数据集解析**  
**2）模型训练**  
**3）服务发布**  
**4）访问服务**

#### 3.数据准备
**1）样本集以excel格式上传到系统，excel文件第一行是样本的特征值，Diagnosis列为预测值，0代表恶性，1代表良性，其他为特征值**  
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/sample.jpg)

**2）创建数据集，选择「已标注数据集-文本-机器学习」，点击 「提交」即可创建数据集**  
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_1.jpg)

**3）数据集创建完成后，可上传数据集，直接上传excel或者将excel压缩成zip包上传，zip包只能包含一个文件， 
     文件上传后会进行数据集及标注信息的解析**    
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_2.jpg)

**4）文件解析完成后，数据量字段为当前数据集的样本量**   
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_3.jpg)

**5）详细了解数据集解析结果可进入标注任务，查看标注数据的详细信息，标注任务会显示特征列、特征列的类型、样本数据信息** 
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_4.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_5.jpg)

#### 4.训练模型
**1）选择菜单栏「我的项目」，项目列表页面「新建项目」，输入项目名称，选择「自动化」类型，提交项目，完成项目的创建**  
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank5.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_6.jpg)

**2）项目创建完成后进行「场景选择」，目前支持4类场景，本案例中选择机器学习，机器学习场景可支持分类、回归两种训练模型，本案例选择分类模型**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_7.jpg)


**3）「数据准备」过程中，可选择步骤3中创建的数据集 「银行存款」，数据选择完后可对「评估指标」、「预测列」、「排除列」进行选择。「评估指标」
     包含平均准确率、精确率、召回率、F1-Score四个选择，该参数对训练迭代会有影响，预测列为要预测的指标，本案例中为Diagnosis， 排除列选择 
     某一列后，被选择的列不用于后续算法训练，本案例中无排除列，本案例排除列为**    
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_8.jpg)

**4）数据准备结束后，提交训练，提交成功后，跳转到项目详情页，训练状态为运行中，等待项目运行结束即可**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_9.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_10.jpg)

**5）训练完成，可查看训练结果，本案例分类模型，包含准确率、精确率、召回率和F1-Score共4个指标。更详细信息可通过点击下图中的icon获取，
包含训练/测试样本数量、ROC曲线、特征值的重要度**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_11.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_12.jpg)


#### 5.模型发布
**1）训练成功可进行服务发布，服务发布后，系统会运行一个API，可使用该API进行预测。发布服务只需要填写服务名称及URL信息，服务URL
为API调用接口。服务提交后需要进行审核，服务状态为「审核中」，后续等待通过即可**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_13.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_14.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_15.jpg)

**2）审核通过服务状态为「运行中」，运行中的服务可进行预测**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_16.jpg)

#### 6.测试服务
**1）服务运行中，可直接点击「服务调用测试」进行调用**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_17.jpg)

**2）body值为用于训练的特征值（去掉排除列），响应中result字段为分类结果**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Breast_Cancer_18.jpg)
