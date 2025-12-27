## Introduction

Expected Threat (xT) is a widely used metric to evaluate the players’ actions based on how much they increase the likelihood of scoring. This submission aims to bring a new dimension to the xT metric by introducing a context-aware decision quality measurement system that penalizes xT values results from non-optimal decisions. By using SkillCorner’s passing options concept, I propose Decision – xT (D-xT) metric that adjusts traditional xT values by incorporating decision quality and penalizing actions that reflect suboptimal decision-making.

## Method

The methodology is to calculate attacking upside, turnover cost, and the risk parameter for each passing option and evaluate them accordingly. This will provide a fair way to rank passing options.

For each on-ball possession with multiple passing options available, a context-aware utility value is computed to assess and rank the options. For each option , first, the attacking expected value, , is estimated, defined as the product of pass completion probability and the resulting xT gain if pass is completed.

To account for downside risk, a turnover excepted value, , is computed, as the probability of pass failure multiplied by a bounded risk multiplier derived from pass difficulty, relative pass distance within the option set, and defensive pressure at the target location.

Decision context is incorporated through a risk parameter modelled via a bounded sigmoid function of pitch zone, player role, defensive pressure, and match urgency (time and score).

The utility of each pass is calculated as:

With values available for the chosen and other passing options, a penalty system can be generated. For each possession, the utility of the executed pass is compared to all available passing options. A normalized regret is computed as the difference between the best and chosen utilities, scaled by the within-possession utility spread with a small stability floor. This regret is mapped to a bounded penalty factor using an anchored logistic function, ensuring no penalty when the optimal option is selected. The realized xThreat is multiplied by this factor to obtain penalized xT.

## Results

Across 10 matches (308 player–match observations), Decision–xT (D-xT) reduced total xT from 66.28 to 50.49, corresponding to a 23.8% decrease, indicating that a substantial share of xT arose from suboptimal passing decisions. Match-level reductions were consistent, ranging from 19.0% to 30.1%. At the player level, several high-xT contributors experienced large absolute and relative reductions (exceeding 45%), reflecting frequent selection of lower-utility options. In contrast, decision-efficient players preserved nearly all of their xT, with reductions below 5%, demonstrating that D-xT differentiates contribution based on decision quality rather than volume alone.

Fig 1. A penalized pass.

Fig 2. A non-penalized pass.

## Conclusion

To summarize, this submission illustrates a method to rate passes and penalize their xT based on decision quality with context-aware information and introduces Decision – xT metric. The future work for this method is to fine-tune the parameters with more matches datasets and include ball carry options into calculations.
