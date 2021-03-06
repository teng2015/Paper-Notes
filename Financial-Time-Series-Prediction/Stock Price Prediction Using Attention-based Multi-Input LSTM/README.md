## Stock Price Prediction Using Attention-based Multi-Input LSTM

作者：Hao Li

年份：2018

出版：ACML

目的：预测第二天开盘价

结论:结合多种股票对指数走势进行预测

本文的主要贡献总结如下：

	1. 我们发现相关股票的潜在用途，并利用相关股票的股价来预测目标股票的未来价格。
	
	2. 我们提出了一种新的MI-LSTM模型，该模型使主流能够决定其他因素的使用，并对不同的记忆单元输入和不同时间步长的隐藏状态采用双阶段注意机制，以提高预测精度.
	
	3. 我们将所提出的模型与各种最先进的模型进行比较，以评估MI-LSTM对中国股市股票数据的有效性。与LSTM相比，MI-LSTM的均方误差(MSE)提高了9.96%.

方法流程：

	1. 股价预测
	
	2. 神经网络
	
	3. 注意力机制在其他应用的研究
	
在各种机器学习任务中，神经网络分配注意权值取得了很大的成功。在机器翻译中，目标是把一个给定的句子翻译成另一种语言的新句子。原句中不同的词在生成目标句中不同的词时，其重要性是不同的，这是理所当然的。Bahdanau等人(2014)使用基于注意的RNNs对对应于不同单词的不同隐藏输出分配注意权重取得了巨大的成功，因此使用注意权重已经成为一种流行病。在电子健康记录领域，Ma等(2017)在不同的时间步长上引入了三种时间注意。推荐系统方面，Wang et al.(2017)在多个神经网络中分配注意力，Chen et al. (2017a)利用知识型注意力来利用领域知识。此外，注意机制在QA系统Chen等(2017b)和图像标题生成Xu等(2015b)方面也取得了进展。最后，Qin等(2017)在最近的股票价格预测工作中，结合了编解码器和注意机制，提出了一种基于双阶段注意的RNN，即DA-RNN。我们也将采用DA-RNN作为比较方法之一。

4.预先知识

4.1 定义

我们将目标股票的历史序列定义为Y=(y1,y2，…，yT)T∈RT，其中T表示时间窗sieze,yT表示T时刻的股票价格，X=(x1,x2，…，xT)T∈RT×D，其中D表示相关股票的数量，正如：

<img src="https://github.com/jm199504/Paper-Notes/blob/master/Financial-Time-Series-Prediction/Stock%20Price%20Prediction%20Using%20Attention-based%20Multi-Input%20LSTM/images/1.png">

多输入LSTM模型（Multi-input LSTM model）：

<img src="https://github.com/jm199504/Paper-Notes/blob/master/Financial-Time-Series-Prediction/Stock%20Price%20Prediction%20Using%20Attention-based%20Multi-Input%20LSTM/images/2.png">

4.2 LSTM模型

<img src="https://github.com/jm199504/Paper-Notes/blob/master/Financial-Time-Series-Prediction/Stock%20Price%20Prediction%20Using%20Attention-based%20Multi-Input%20LSTM/images/3.png">

4.3因子

<img src="https://github.com/jm199504/Paper-Notes/blob/master/Financial-Time-Series-Prediction/Stock%20Price%20Prediction%20Using%20Attention-based%20Multi-Input%20LSTM/images/4.png">

其中X包含三种股票系列:
4.3.1正相关级数
4.3.2负相关级数
4.3.3指数系列
本文利用皮尔逊相关系数(PCC)来度量不同股票价格序列之间的相关性。给定两个变量A,B∈RT, PCC由：

<img src="https://github.com/jm199504/Paper-Notes/blob/master/Financial-Time-Series-Prediction/Stock%20Price%20Prediction%20Using%20Attention-based%20Multi-Input%20LSTM/images/5.png">

其中Cov(·)和Var(·)分别为协方差和方差.
		
4.4 MI-LSTM说明

<img src="https://github.com/jm199504/Paper-Notes/blob/master/Financial-Time-Series-Prediction/Stock%20Price%20Prediction%20Using%20Attention-based%20Multi-Input%20LSTM/images/6.png">

在我们的实验中，我们选择ReLU作为激活因子。
我们使用RMSProp Hinton等人(2012)作为我们的训练优化器，学习率为0.001。
在数据大小方面，小批量大小为512。
该模型是通过最小化所有列车样本的均方误差来学习的

5.数据集
我们选择CSI-300指数下的主要股票作为数据集。在300只股票中，我们剔除了历史记录在4年以内的40只股票。我们也将CSI-300指数作为个股，因此我们的数据集包含了261只股票2013年4月25日至2017年5月15日的开盘价格。验证集从最近的300-101天派生而来，测试集从最近的100天派生而来，其余的用于培训。在固定时间窗大小T = 10和stride 1下，我们总共从261只股票(含指数)中生成249,516个样本，包括171,216个训练样本、52,200个验证样本和26,100个测试样本

6.评估指标
Min. MSE & Avg. MSE

7.参数选择
相关股票数量的影响

<img src="https://github.com/jm199504/Paper-Notes/blob/master/Financial-Time-Series-Prediction/Stock%20Price%20Prediction%20Using%20Attention-based%20Multi-Input%20LSTM/images/7.png">

注意模块效应

<img src="https://github.com/jm199504/Paper-Notes/blob/master/Financial-Time-Series-Prediction/Stock%20Price%20Prediction%20Using%20Attention-based%20Multi-Input%20LSTM/images/8.png">
