# 语音数据性能检测工具
===
## 实现功能
---
1. 支持各种评估指标
	1). SDR: 		Source-to-Distortion Ratio, 信号失真比
	2). SIR: 		Source to Interferences Ratio, 源信号干扰比
	3). SAR:		Signal to Artifacts Ratio, 人造误差成分
	4). STOI:		Short-Time Objective Intelligibility, 短时客观可懂度
	5). PESQ:		Perceptual evaluation of speech quality, 感知语音质量评估
	6). SI-SNR: 	Scale-invariant source-to-noise ratio, 尺度不变信噪比

2. 支持单个样本输入，也支持minibatch格式样本的输入
	eg：单样本	   [C, T]    
		minibatch [B, C, T]
	注:		B batch
			C channel
			T length of audio

3. 支持自动纠正输入信号与参考信号的计算排序，所利用的排序规则是最大化SI-SNR。有时候估计信号和参考通道间的排序是反的，本脚本可自动纠正。

## 输入格式
---
single sample:
	Args:
		estimate: 	numpy.ndarray, [C, T], reordered by best PIT permutation
		reference:  numpy.ndarray, [C, T]
		mixture:    numpy.ndarray, [T] or [C, T]
	Returns:
		average_SDRi 
		average_SIRi
		average_SIRi
		average_STOIi
		average_PESQi
		average_SISNRi
	注：i -> improvement

minibatch:
	Args:
		estimate: 	numpy.ndarray, [B, C, T], reordered by best PIT permutation
		reference:  numpy.ndarray, [B, C, T]
		mixture:    numpy.ndarray, [B, T] or [B, C, T]
	Returns:
		average_SDRi
		average_SIRi
		average_SIRi
		average_STOIi
		average_PESQi
		average_SISNRi
	注：i -> improvement


