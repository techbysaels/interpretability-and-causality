# Automobile insurance and telematics

Traditional automobile insurance pricing often uses information given at the moment of approval. The data used involves driver age, vehicle characteristics, territory, prior claims, and exposure. Nowadays, we can add new information using telematics obtained by smartphone or vehicle sensors to check on driving behaviour; for example, Cambridge Mobile Telematics (CMT) describes its insurance platform as using sensor data and AI to monitor driving behaviour and support risk-based insurance programs. So et al. (2020) and Chan et al. (2023) also show that telematics can capture variables such as distance travelled, braking, acceleration, turning, travel frequency, speed patterns, and nighttime driving that are not currently represented in traditional automobile insurance but could definitely improve risk differentiation.

However, the main issue in adding this data would be the change of meaning of existing model coefficients. A variable could be useful, but the combination of data could delete this usefulness to improve the accuracy, presenting the endogenous problem of the variables. Then, we need to determine which variables are causal and would help the model to improve without taking meaning away from them. Considering this information, the following responses to the questions are presented:

## How would I update an existing pricing model to use this data while preserving causal interpretations for existing features in the model?

First, I would start by defining what is causal in the current traditional model, making an evaluation for every feature and documenting the conclusions. It is important to notice that interpretability is not the same as causality; interpretability helps us understand the model, but for causality we must respond to the question: Is this variable impacting the outcome correctly, or is it an incorrect cause-effect assumption made by the model?

Then, I would add the telematics features to the model; however, I would not do it all at once because we need to address which variables are causal and which are not adding value to the model. For example, age may influence driving experience and behaviour, which may affect the crash risk. If the age coefficient was intended to represent a total causal effect, adding variables like braking, speeding, or distraction variables could change the age coefficient into a different effect. The new coefficient might be valid for the overall model, but it would not answer the same causal question, losing interpretability and causality of the model. For that reason, the telematics variables should be classified first as predictive signals or proxies before allowing their insertion into the causal part of the model. In this way, the variables descendant of an existing causal feature would not automatically be used as controls when estimating the original total effect.

After these preparations, I would use the strategy of the shallow approach, where I maintain the original causal component and add telematics as a separate incremental risk layer. Using the original data, I would estimate (or re-estimate) and validate the baseline model apart from the telematics and then add a telematics correction that could be estimated by a neural network model. This structure will benefit the model by not re-estimating baseline coefficients just because we have new data available and changing the meaning, and also will allow the telematics to be evaluated as incremental predictive information. Additionally, to reduce duplication of predictive information, I would consider residualizing highly correlated telematics summaries against the baseline features before using them in the incremental layer. Doing some research, I have found that this approach has been described by Chan et al. (2023), making this model not only theoretical but also usable in practice.

Finally, I would keep causal explanations separate from telematics prediction for the stakeholders. The causal interpretation would come from the original rating factors, and the telematics would be explained as incremental predictive contributions and not necessarily causal variables because they would need further analysis.

## How would I recommend integrating this data into the existing model? What other elements would I need to consider?

Because NIST notes that third-party data and systems can complicate AI risk measurement because the provider's metrics, methods, and risk controls may differ from those of the organization deploying the system (NIST, 2023), I would integrate the data in stages rather than sending raw telematics directly into the production pricing algorithm. This is especially important because we are using third-party data.

To integrate this data into production, I would recommend the following:

- Establish a data contract and provenance record to know exactly the meaning of each field and how it is generated, among other important data like timestamps or version changes.

- Create policy-aligned behavioural features because we need to have controlled features instead of raw trip data.

- Prevent temporal leakage because only driving behaviour observed before the outcome period being priced or predicted should be used.

- Treat exposure explicitly as event counts should be interpreted relative to exposure where appropriate.

- Use the baseline model as an anchor because it has the causal effects analysed; the telematics will not provide causality

- Validate out of sample and by subgroup to insure performance

- Monitor missingness and selection should be informative rather than random. An analysis must be done on usable trip coverage, missing sensor periods, and driver attribution quality before allowing the score to affect the price

- Choose the observation period empirically because after some time window, the data became repeated instead of adding value to the model. For example, patterns repeat after three months of driving historical data.

- Implement fairness and regulatory testing because we are dealing with an application that could affect people and their access to these services.

- Create continuous monitoring and vendor-change controls because the third-party provider can change their code, scoring algorithm, sensor methods, or field definitions, affecting the overall models.

- Privacy, consent, security, and explainability are key to this process because we are dealing with sensitive information that can reveal much more than driving risk and could put the users in danger. Then I would apply data minimization using only the data needed for the pricing purpose and not more. Protecting the users and the company from privacy or legal issues.

- I would not agree with a vendor score that cannot be independently tested; we should know where the data comes from, even if it’s a predicted one the third party is trying to provide for our benefit. Not knowing the source of the data would lead to blind usage of the final model and, almost certainly, to legal issues or economic losses.

## References

- Cambridge Mobile Telematics. (n.d.). Cambridge Mobile Telematics: Safer mobility with sensor data and AI. Retrieved August 11, 2026, from https://www.cmtelematics.com/

- Chan, I. W., Tseung, S. C., Badescu, A. L., & Lin, X. S. (2023). Data mining of telematics data: Unveiling the hidden patterns in driving behaviour. arXiv. https://arxiv.org/abs/2304.10591

- National Institute of Standards and Technology. (2023). Artificial Intelligence Risk Management Framework (AI RMF 1.0) (NIST AI 100-1). https://doi.org/10.6028/NIST.AI.100-1

- So, B., Boucher, J.-P., & Valdez, E. A. (2020). Cost-sensitive multi-class AdaBoost for understanding driving behavior with telematics. arXiv. https://arxiv.org/abs/2007.03100
