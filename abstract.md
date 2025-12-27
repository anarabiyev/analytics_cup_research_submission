# Introduction

**Expected Threat (xT)** is a widely used metric to evaluate players’ actions based on how much they increase the likelihood of scoring. This submission aims to bring a new dimension to the xT metric by introducing a **context-aware decision quality measurement system** that penalizes xT values resulting from **non-optimal decisions**. By using **SkillCorner’s passing options** concept, I propose the **Decision – xT (D-xT)** metric, which adjusts traditional xT values by incorporating **decision quality** and penalizing actions that reflect **suboptimal decision-making**.

# Method

The methodology is to calculate **attacking upside**, **turnover cost**, and a **risk parameter** for each passing option and evaluate them accordingly. This provides a fair and structured way to rank passing options.

For each on-ball possession with multiple passing options available, a **context-aware utility value** is computed to assess and rank the options. For each option $ i $, the **attacking expected value**, denoted as $ \text{AttackEV}_i $, is estimated as the product of the pass completion probability and the resulting xT gain if the pass is completed.

$$
\text{AttackEV}_i = p_i^{\text{comp}} \cdot \Delta xT_i
$$

where:
- $ p_i^{\text{comp}} $ is the probability that pass option $$ i $$ is successfully completed  
- $ \Delta xT_i $ is the change in Expected Threat resulting from the completed pass
