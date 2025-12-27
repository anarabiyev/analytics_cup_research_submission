# Introduction

**Expected Threat (xT)** is a widely used metric to evaluate players’ actions based on how much they increase the likelihood of scoring. This submission aims to bring a new dimension to the xT metric by introducing a **context-aware decision quality measurement system** that penalizes xT values resulting from **non-optimal decisions**. By using **SkillCorner’s passing options** concept, I propose the **Decision – xT (D-xT)** metric, which adjusts traditional xT values by incorporating **decision quality** and penalizing actions that reflect **suboptimal decision-making**.

# Method

The methodology is to calculate **attacking upside**, **turnover cost**, and a **risk parameter** for each passing option and evaluate them accordingly. This provides a fair and structured way to rank passing options.

For each on-ball possession with multiple passing options available, a **context-aware utility value** is computed to assess and rank the options. For each option $i$, the **attacking expected value**, denoted as $\text{AttackEV}_i$, is estimated as the product of the pass completion probability and the resulting xT gain if the pass is completed.

$$
\text{AttackEV}_i = p_i^{\text{comp}} \cdot \Delta xT_i
$$

where:
- $p_i^{\text{comp}}$ is the probability that pass option $i$ is successfully completed  
- $\Delta xT_i$ is the change in Expected Threat resulting from the completed pass

To account for downside risk, a turnover expected value, $TurnoverEV_i$, is computed as the probability of pass failure multiplied by a bounded risk multiplier derived from pass difficulty, relative pass distance within the option set, and defensive pressure at the target location.

$$
TurnoverEV_i = (1 - p_i^{comp}) \cdot m_i
$$

$$
m_i = \text{clip}\left(
1 + w_{diff}\,\text{PassDifficulty}_i
+ w_{dist}\,\text{Dist}_i
+ w_{press}\,P_i,
\; m_{min},\; m_{max}
\right)
$$

Decision context is incorporated through a risk parameter $\lambda_i$ modelled via a bounded sigmoid function of pitch zone, player role, defensive pressure, and match urgency (time and score).

$$
z_i = \beta_0 + \beta_{role} Role_i + \beta_{zone} Zone_i + \beta_{pressure} Press_i - \beta_{urgency} Urg_i
$$

The utility of each pass is calculated as:

$$
pass_{u_i} = AttackEV_i - \alpha \cdot \lambda_i \cdot TurnoverEV_i
$$

With $pass_u$ values available for the chosen and other passing options, a penalty system can be generated. For each possession, the utility of the executed pass is compared to all available passing options. A normalized regret is computed as the difference between the best and chosen utilities, scaled by the within-possession utility spread with a small stability floor. This regret is mapped to a bounded penalty factor using an anchored logistic function, ensuring no penalty when the optimal option is selected. The realized $xThreat$ is multiplied by this factor to obtain penalized $xT$.

# Results

Across 10 matches (308 player–match observations), Decision–xT (D-xT) reduced total $xT$ from 66.28 to 50.49, corresponding to a 23.8% decrease, indicating that a substantial share of $xT$ arose from suboptimal passing decisions. Match-level reductions were consistent, ranging from 19.0% to 30.1%. At the player level, high-$xT$ contributors experienced large absolute and relative reductions (exceeding 45%), reflecting frequent selection of lower-utility options. In contrast, decision-efficient players preserved nearly all of their $xT$, with reductions below 5%, demonstrating that D-xT differentiates contribution based on decision quality rather than volume alone.

# Conclusion

To summarize, this submission illustrates a method to rate passes and penalize their $xT$ based on decision quality with context-aware information and introduces the Decision–xT metric. Future work for this method is to fine-tune the parameters with larger match datasets and include ball-carry options in the calculations.
