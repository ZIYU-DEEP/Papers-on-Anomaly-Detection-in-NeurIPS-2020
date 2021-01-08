# NIPS-2020-Paper-on-Anomaly-Detection
A list of all papers related to anomaly detection in NeurIPS 2020.  

A common finding from those papers – some anomaly detection models can assign low anomaly scores to (thus bias the detection performance on) certain anomalies (*e.g.* anomalies that the models haven't been trained on).   

Common explanations:
- Generative models are biased towards **low-complexity inputs** (which have higher likelihoods);
- Some network structures (*e.g.* CNN) are biased towards **low-level features**, thus cannot discriminate anomalies with just difference on high-level features.
- The **typical sets** and **high-density regions** of some models may not coincide.

## 1. Study of Performance Bias
**Understanding Anomaly Detection with Deep Invertible Networks through Hierarchies of Distributions and Features** [[abs](https://arxiv.org/abs/2006.10848)][[pdf](https://arxiv.org/pdf/2006.10848.pdf)][[code](https://github.com/boschresearch/hierarchical_anomaly_detection)]     
*Robin Tibor Schirrmeister, Yuxuan Zhou, Tonio Ball, Dan Zhang*  
> - **Problem**: Deep generative networks trained via maximum likelihood on one image dataset often assign high likelihood on images from another datasets.   
> - **Explanation**: Such high probability is a result from the combiantion of **model bias** and **domain prior**.   
>   - CNN learns *low-level features*, and such features dominate the *likelihood*.  
>   - Thus, when the discriminative features between inliers and outliers are on *high-level* (e.g. shape), anomaly detection becomes challenging.  
> - **Mitigating Strategy**: 
>   - Method 1: Using the log likelihood ratios of two identical models, one trained on the in-distribution data and the other one on a more general distribution of images; Also, deriving a new outlier loss for the first network on samples from the general distribution.
>   - Method 2: Using a Glow-like model to discriminate by *high-level features* by using only the likelihood contribution of the final scale. (*p.s.* for me it seems that this will not work on those "hard anomalies"; specifically, there could be low-level anomalies and high-level anomalies, and the following paper addresses this issue.).  
> **Relevant papers**: [Do Deep Generative Models Know What They Don't Know?](https://openreview.net/forum?id=H1xwNhCcYm).
<br>

**Further Analysis of Outlier Detection with Deep Generative Models** [[abs](https://arxiv.org/abs/2010.13064)][[pdf](https://arxiv.org/pdf/2010.13064.pdf)]    
*Ziyu Wang, Bin Dai, David Wipf, Jun Zhu*   
> - **Problem**: Deep generative models (DGMs) can frequently assign a **higher likelihood to outliers**.     
> - **Explanation**:    
>   - Observation: A model's *typical set* and *high-density region* may not conincide.  
>   - Thus, the failure of the likelihood-based model does not imply that the model is uncalibrated. 
> The authors also provide additional experiments to disentagle the impact of **low-level features** (*e.g.* texture) and **high-level features** (*e.g.* semantics) in differentiating outliers. 
<br>

**Likelihood Regret: An Out-of-Distribution Detection Score For Variational Auto-encoder** [[abs](https://arxiv.org/abs/2003.02977)][[PDF](https://arxiv.org/pdf/2003.02977.pdf)]     
*Zhisheng Xiao, Qing Yan, Yali Amit*   
> - **Problem**: 
>    - Probabilistic generative models can **assign higher likelihoods** on certain types of OOD samples, make the OOD detection rules based on *likelihood threshold* problematic.  
>    - Some OOD detection methods have been proposed to solve the issue, and this paper found these methods fail on VAEs.  
> - **Mitigating Strategy**: The paper proposes **Likelihood Regret** as an better OOD scoring function for VAEs.  
> - **Relevant papers**: [Input Complexity and Out-of-distribution Detection with Likelihood-based Generative Models](https://openreview.net/forum?id=SyxIWpVYvr) (which claims that generative models are biased towards low-complexity inputs).
<br>

**Why Normalizing Flows Fail to Detect Out-of-Distribution Data** [[abs](https://arxiv.org/abs/2006.08545)][[pdf](https://arxiv.org/pdf/2006.08545.pdf)][[code](https://github.com/PolinaKirichenko/flows_ood)][[thread](https://twitter.com/polkirichenko/status/1272715634544119809)]    
*Polina Kirichenko, Pavel Izmailov, Andrew Gordon Wilson*  
> - **Problem**: Flow-based model (a type of DGMs) can assign high-likelihood to outlier data.    
> - **Explanation**: Flows learn *local pixel correlations* and *generic image-to-latent-space transformations* (*i.e.* inductive biases of flows), which are not specific to the target image dataset.    
> - **Mitigating Strategy**: The papers shows that modifying the flow *coupling layers* can *bias* the flow towards learning the *semantic structure* of the target data.
<br>

**Energy-based Out-of-distribution Detection** [[abs](https://arxiv.org/abs/2010.03759)][[pdf](https://arxiv.org/pdf/2010.03759.pdf)]    
*Weitang Liu, Xiaoyun Wang, John D. Owens, Yixuan Li*  
> - **Problem**: Traditional OOD detection methods relying on the **softmax confidence score** suffer from **overconfident posterior distributions** for OOD data.  
> - **Explanation**: The softmax confidence score often do not align with the underlying probability density.
> - **Mitigating Strategy**: The paper proposes a unified framework for OOD detection that uses an **energy score**.
>   - *Energy scores* are theoretically aligned with the *probability density*, thus are less susceptible to the overconfidence issue.
<br>

**Perfect density models cannot guarantee anomaly detection** [[abs](https://arxiv.org/abs/2012.03808v1)]    
*Charline Le Lan, Laurent Dinh*   
<br>


## 2. Study on Supervision
**CSI: Novelty Detection via Contrastive Learning on Distributionally Shifted Instances** [[abs](https://arxiv.org/abs/2007.08176)][[pdf](https://arxiv.org/pdf/2007.08176.pdf)]     
*Jihoon Tack, Sangwoo Mo, Jongheon Jeong, Jinwoo Shin*   
> A method using self-supervision (considering transformed normal data as abnormal data, then do classification) on anomaly detection.
<br>

**Rethinking the Value of Labels for Improving Class-Imbalanced Learning** [[website](https://www.mit.edu/~yuzhe/imbalanced-semi-self.html)][[abs](https://arxiv.org/abs/2006.07529)][[pdf](https://arxiv.org/pdf/2006.07529)][[code](https://github.com/YyzHarry/imbalanced-semi-self)][[video](http://www.youtube.com/watch?v=XltXZ3OZvyI)][[zhihu-illustration-1](https://zhuanlan.zhihu.com/p/265326764)][[zhihu-illustration-2](https://zhuanlan.zhihu.com/p/259710601)]      
*Yuzhe Yang, Zhi Xu*   
<br>

## 3. Miscellaneous
**Timeseries Anomaly Detection using Temporal Hierarchical One-Class Network**       
*Lifeng Shen, Zhuocong Li, James Kwok*    
<br>

**Certifiably Adversarially Robust Detection of Out-of-Distribution Data**      
*Julian Bitterwolf, Alexander Meinke, Matthias Hein*  
<br>

**One Ring to Rule Them All: Certifiably Robust Geometric Perception with Outliers** [[abs](https://arxiv.org/abs/2006.06769)][[pdf](https://arxiv.org/pdf/2006.06769)]    
*Heng Yang, Luca Carlone*   
<br>

(The following is a workshop one.)  
**Towards Maximizing the Representation Gap between In-Domain & Out-of-Distribution Examples** [[abs](http://arxiv.org/abs/2010.10474v2)]     
*Jay Nandy, Wynne Hsu, Mong Li Lee*   
<br>

(This one is not in NIPS'2020 accepted papers but looks interesting.)   
**Provable Worst Case Guarantees for the Detection of Out-of-Distribution Data** [[abs](https://arxiv.org/abs/2007.08473)][[pdf](https://arxiv.org/pdf/2007.08473)]   
*Julian Bitterwolf, Alexander Meinke, Matthias Hein*   
<br>

