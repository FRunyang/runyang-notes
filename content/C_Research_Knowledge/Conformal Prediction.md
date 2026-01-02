---
aliases:
  - CP
tags:
  - CP
date: 2025-11-03T11:09:00
---
> *共性预测 Conformal Prediction 学习*

## 基本流程

*共性预测目标：*
对于任意一个模型，构造出一个预测集合，而不是单一的输出。这个集合满足，真实标签在集合中的概率大于等于 $1-\alpha$。注意，这里模型输出都是logits，即每个类别的预测概率。
*具体流程*：
1. 为了构造集合，需要$n$个校准集。首先对校准集每一个样本计算一个 Conformal Score（也称不一致性分数，越大表示预测越不可靠）：
	```python
	# 1: get conformal scores. n = calib_Y.shape[0] 
		cal_smx = model(calib_X).softmax(dim=1).numpy()
		cal_scores = 1-cal_smx[np.arange(n),cal_labels]
	# Example
		cal_smx = np.array([
		  [0.9, 0.05, 0.05],   # sample 0
		  [0.2, 0.7, 0.1],     # sample 1
		  [0.3, 0.2, 0.5]      # sample 2
		])
		cal_labels = np.array([0, 1, 2])
	```
2. 有 socre 之后，计算一个 $\hat{q}$,即大约$1-\alpha$分位数，（如排序后第 $1-\alpha$个数）
	```python
	q_level = np.ceil((n+1)*(1-alpha))/n
	qhat = np.quantile(cal_scores, q_level, method='higher')
	# example
	s = np.array([1, 2, 3, 4, 5])
	print(np.quantile(s, 0.8, method="higher")) # 5
	# n=5,q=0.8, 计算分位点的位置：
	#p=q×(n−1)=0.8×4=3.2
	#这意味着分位点在第 3.2 个样本（从 0 开始计数）处。  
	#按照 `"higher"` 的规则：
	#找到 大于等于 3.2 的最小索引 → 索引 4（对应值 5）
	#所以输出 5
	```
3. 为每个测试样本构造集合，$C(X_{test}) = {y : \hat{f}(X_{test})_y ≥ 1 − \hat{q}}$,即测试样本类别概率大于等于$1 − \hat{q}$
就放进集合里。这样就完成了构造。

