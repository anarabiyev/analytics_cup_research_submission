# Decision–xT (D-xT): Context-Aware Penalization of xThreat Based on Decision Quality

## Introduction
Expected Threat (xT) is a widely used metric to evaluate players’ actions based on how much they increase the likelihood of scoring. This submission introduces a new dimension to the xT metric by incorporating **context-aware decision quality**. Using SkillCorner’s passing options concept, we propose **Decision–xT (D-xT)**, a metric that penalizes xT values resulting from non-optimal decisions.

## Method
For each on-ball possession with multiple passing options, a context-aware utility value is computed to assess and rank the available options.

For each option *i*, the **attacking expected value** is defined as:

$$
A_i = p^{comp}_i \cdot \Delta xT_i
$$

where:
- $\( p^{comp}_i \)$ is the probability of pass completion
- \( \Delta xT_i \) is the xT gain conditional on completion

To account for downside risk, a **turnover expected value** is computed:

\[
T_i = p^{fail}_i \cdot r_i
\]

where:
- \( p^{fail}_i = 1 - p^{comp}_i \)
- \( r_i \in [0, 1] \) is a bounded risk multiplier based on pass difficulty, relative distance, and defensive pressure

Decision context is incorporated via a **risk parameter** \( \rho_i \), modeled using a bounded sigmoid function:

\[
\rho_i = \sigma(g(zone_i, role, pressure_i, urgency)), \quad
\sigma(x) = \frac{1}{1 + e^{-x}}
\]

The **utility** of each option is then calculated as:

\[
U_i = A_i - \rho_i T_i
\]

A **normalized regret** is computed by comparing the chosen pass to the best available option:

\[
regret = \frac{\max_j U_j - U_{chosen}}{(\max_j U_j - \min_j U_j) + \epsilon}
\]

where \( \epsilon > 0 \) is a small stability constant.

This regret is mapped to a **bounded penalty factor** using an anchored logistic function:

\[
\pi(regret) = \frac{1}{1 + \exp(k(regret - b))}
\]

with parameters \( k > 0 \) and \( b \), and an anchoring constraint such that \( \pi(0) = 1 \).

The penalized xT is then computed as:

\[
\text{D-xT} = xT_{realized} \cdot \pi(regret)
\]

## Results
Across 10 matches (308 player–match observations), Decision–xT reduced total xT from **66.28 to 50.49**, a **23.8% decrease**, indicating that a substantial share of xT arose from suboptimal passing decisions. Match-level reductions ranged from **19.0% to 30.1%**.

At the player level, several high-xT contributors experienced reductions exceeding **45%**, reflecting frequent selection of lower-utility options. In contrast, decision-efficient players retained nearly all of their xT (reductions below **5%**), demonstrating that D-xT differentiates contribution based on **decision quality rather than volume**.

## Conclusion
This work introduces **Decision–xT**, a method for penalizing xT based on context-aware decision quality. Future work includes parameter tuning using larger datasets and extending the framework to incorporate ball-carry options.

