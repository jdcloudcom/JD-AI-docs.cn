# 银行定期存款预测

#### 1.数据集介绍
该数据集选自UCI机器学习库，数据来源于某葡萄牙银行机构的一次直接营销活动，该营销活动采用电话访问方式，多次对同一用户进行访问确定是否会购买定期存款。数据集包含41188个样本，从2008年5月至2010年11月的数据，
样本包含20特征值，预测列为y，y的值为0代表不会存款，值为1代表会存款  
特征值如下：  
 1 -age(年龄)  
 2 -job:工作类型(分类:“行政”、“蓝领”、“企业家”、“女佣”、“管理”、“退休”、“自我雇佣”、“服务”、“学生”、“技术员”、“失业”、“未知”)  
 3 -marital:婚姻状况(分类:“离婚”、“已婚”、“单身”、“未知”;注:“离婚”指离婚或丧偶)
 4 -education:(分类:“4年基础”、“6年基础”、“6年基础”、“高中”、“文盲”、“专业”、“课程”、“大学”、“未知”)  
 5 -default:信用违约?(分类:“有”、“无”、“未知”)  
 6 -housing:有住房贷款吗?(分类:“有”、“无”、“未知”)
 7 -loan:有个人贷款吗?(分类:“有”、“无”、“未知”)  
 8 -contact:联系人通信类型(分类:“移动电话”、“电话”)  
 9 -month:最后一次联系所在的月份(分类:“一月”、“二月”、“三月”，……,11月,12月)
 10 -day_of_week:每周最后联系日期(分类:‘mon’、‘tue’、‘wed’、‘thu’、‘fri’)  
 11 -duration:最后的接触持续时间，以秒为单位(数值)  
 12 -campaign:活动期间与同一客户交流过的联系人数目
 13 -pdays:上次活动联系客户后经过的天数(数字;999表示之前没有联络客户)   
 14 -previous:活动前和客户交流过的联系人数量(数字)  
 15 -poutcome:之前营销活动的成果(分类:‘失败’、‘不存在’、‘成功’)  
 16 -emp.var.rate:就业变动率-季度指标(数值)   
 17 -cons.price.idx:消费物价指数-每月指标(数值)   
 18 -cons.conf.idx:消费者信心指数-每月指标(数值)   
 19 -euribor3m: euribor3个月利率-每日指标(数值)  
 20 -nr.employed:员工人数-季度指标(数值)   


#### 2.整体流程

**1）数据集解析**  
**2）模型训练**  
**3）服务发布**  
**4）访问服务**

#### 3.数据准备
**1）样本集以excel格式上传到系统，excel文件第一行是样本的特征值，y列为预测值，其他为特征值**  
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/sample.jpg)

**2）创建数据集，选择「已标注数据集-文本-机器学习」，点击 「提交」即可创建数据集**  
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank.jpg)

**3）数据集创建完成后，可上传数据集，直接上传excel或者将excel压缩成zip包上传，zip包只能包含一个文件， 
     文件上传后会进行数据集及标注信息的解析**    
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank1.jpg)

**4）文件解析完成后，数据量字段为当前数据集的样本量**   
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank2.jpg)

**5）详细了解数据集解析结果可进入标注任务，查看标注数据的详细信息，标注任务会显示特征列、特征列的类型、样本数据信息** 
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank3.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank20.jpg)

#### 4.训练模型
**1）选择菜单栏「我的项目」，项目列表页面「新建项目」，输入项目名称，选择「自动化」类型，提交项目，完成项目的创建**  
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank5.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank6.jpg)

**2）项目创建完成后进行「场景选择」，目前支持4类场景，本案例中选择机器学习，机器学习场景可支持分类、回归两种训练模型，本案例选择分类模型**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank7.jpg)

**3）「数据准备」过程中，可选择步骤3中创建的数据集 「银行存款」，数据选择完后可对「评估指标」、「预测列」、「排除列」进行选择。「评估指标」
     包含平均准确率、精确率、召回率、F1-Score四个选择，该参数对训练迭代会有影响，预测列为要预测的指标，本案例中为y， 排除列选择 
     某一列后，被选择的列不用于后续算法训练，本案例中无排除列**   
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank8.jpg)

**4）数据准备结束后，提交训练，提交成功后，跳转到项目详情页，训练状态为运行中，等待项目运行结束即可**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank9.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank10.jpg)

**5）训练完成，可查看训练结果，本案例分类模型，包含准确率、精确率、召回率和F1-Score共4个指标。更详细信息可通过点击下图中的icon获取，
包含训练/测试样本数量、ROC曲线、特征值的重要度**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank12.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank16.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank17.jpg)

#### 5.模型发布

**1）训练成功可进行服务发布，服务发布后，系统会运行一个API，可使用该API进行预测。发布服务只需要填写服务名称及URL信息，服务URL
为API调用接口。服务提交后需要进行审核，服务状态为「审核中」，后续等待通过即可**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank13.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank14.jpg)

![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank15.jpg)

**2）审核通过服务状态为「运行中」，运行中的服务可进行预测**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank21.jpg)

#### 6.测试服务
**1）服务运行中，可直接点击「服务调用测试」进行调用**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank18.jpg)

**2）body值为用于训练的特征值（去掉排除列），响应中result字段为分类结果**
![](../../../../../../image/AI-and-Machine-Learning/NeuFoundry/case/demo1/Bank20.jpg)




---

如果您对产品有使用或者其他方面任何问题，欢迎联系我们

---