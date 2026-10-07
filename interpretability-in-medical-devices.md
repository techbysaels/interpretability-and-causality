# Interpretability in medical devices

Due to several factors, medical AI devices may not be evaluated properly. This presents a complex and ethically challenging issue for developers, healthcare workers, and patients.

After reviewing the article ['Are Medical AI Devices Evaluated Appropriately?'](https://hai.stanford.edu/news/are-medical-ai-devices-evaluated-appropriately) about the evaluation of medical devices, highlights the complexities in developing applications using medical AI and features suggested future directions for developers of medical AI devices, I would respond to the following questions: What are some of the challenges in evaluating medical AI devices, and how can they be overcome?, How can evaluation frameworks be standardized across different devices and applications to ensure consistency and fairness in the evaluation process?, How can these stakeholders work together to establish guidelines and standards for evaluation, and what steps can be taken to ensure that these guidelines are followed? and Which additional resources would I recommend to read to address this topic?

## What are some of the challenges in evaluating medical AI devices, and how can they be overcome?

One of the most important challenges is the generalization of the models. The article provides an example of an AI model identifying collapsed lungs in chest X-rays. It was trained and tested with data from Stanford Health Center and performed well, but the accuracy decreased when testing with data from other institutions. On one of them, the performance was higher for White patients than for Black patients. This demonstrates that the data should be evaluated in more hospitals and that the reasons for differences in accuracy should be checked to have a complete picture of the performance.

Another challenge is the extended use of retrospective data, meaning that the models predict well for historical data but not for new data. This happens because historical data have already known outputs, but new data need to consider the interactions between the doctors and AI systems in real clinical environments. The performance of every AI tool, especially medical ones, depends partly on how the tool is used and how the physicians act on their recommendations.

A third challenge is data and model drift, because patient populations, clinical practices, equipment, data distributions, and standards can change after deployment. According to the article, the FDA identified that these changes are causes of performance degradation, bias, and reduced reliability. The population has changed over time; for example, we should not expect the same lung composition for healthy persons after the COVID-19 pandemic.

Finally, a transparency problem is also present because the models have been found to have reporting gaps. These gaps could include safety and effectiveness documents without subject sample size, without specifications of the machine-learning technique used, or without uncertainty outputs. These could lead to the thought that the model predicts with the same exact accuracy every output without the possibility of looking further into the model. Medical decisions need strong clinical evidence to support them, and by dealing with these challenges, the outcomes would be better for the health of the population.

## How can evaluation frameworks be standardized across different devices and applications to ensure consistency and fairness in the evaluation process?

I would standardize the evaluation process and minimum evidence requirements instead of applying the same metric to every AI medical device. I think I would first request a clearly defined intended use, intended patient population, clinical environment, and level of risk. Then training, validation, and independent test datasets should be documented transparently and should be validated through external sites, particularly for high-risk applications, ensuring the model is generalizing correctly.

I also consider that meaningful metrics should be used and noted in the outcomes, such as sensitivity, specificity, calibration, false-negative rates, or other measures according to the device. It should be complemented with analysis across demographic and clinical subgroups. Other important information such as limitations, uncertainty, known failure conditions, and human-AI interaction should also be documented for the general knowledge of the users.

For the users, it should be stated that the model is an input for real-world evaluation, not the absolute truth. They must also be aware of performance drift or biases detected to avoid any issues when diagnosing a disease. Finally, a predefined model should be stated when a change in the model requires revalidation or regulatory review from the users.

## How can these stakeholders work together to establish guidelines and standards for evaluation, and what steps can be taken to ensure that these guidelines are followed?

For this use case, stakeholders are developers, healthcare professionals, patients, and regulators. All should ensure that the AI is being used well instead of making the developers responsible for all the issues.

Developers should understand the architecture, datasets, limitations, and failure modes because they should be able to explain what the model is doing to come up with a prediction. They should be especially careful documenting the data provenance, validation procedures, known limitations, and performance across relevant groups. This information is key to addressing the transparency problem mentioned earlier.

Healthcare professionals should accompany the development by determining which evaluation metrics actually correspond to meaningful clinical outcomes. They are also essential for testing how the AI interacts with real workflows because an accurate system can still become unsafe if the recommendations are presented at the wrong time, are difficult to interpret, or encourage excessive reliance on automation.

Patients need to participate in discussions about acceptable risk, privacy, informed use, usability, fairness, and the consequences of incorrect predictions because they would be the main affected ones by any decision taken. They are a relevant audience and source for information about machine-learning medical devices.

Finally, regulators should provide minimum requirements that make evaluations comparable and auditable. Fortunately, nowadays, organizations like WHO include regulators, policymakers, academia, industry, developers, manufacturers, and healthcare practitioners. It emphasizes the risk-benefit assessment together with evaluation, validation, and monitoring of the performance.

## Which additional resources would I recommend to read to address this topic?

### [WHO — Generating Evidence for Artificial Intelligence Based Medical Devices: A Framework for Training, Validation and Evaluation (2021)](https://www.who.int/publications/i/item/9789240038462)

In the publication, WHO describes a framework designed for developers and researchers working on AI-base software on medical devices. It complements the article because the WHO framework addresses the issues seen in the article and helps us think more systematically about the evidence that should be generated during training, validation, and evaluation.

### [IMDRF — Good Machine Learning Practice for Medical Device Development: Guiding Principles (2025)](https://www.imdrf.org/documents/good-machine-learning-practice-medical-device-development-guiding-principles)

I recommend this resource also because it is more recent and is focused on creating international principles. The framework contains ten principles and considers safety and effectiveness throughout the medical device’s product life cycle instead of only effectiveness at a static point in time. It will help us to share a similar vision and allow requirements to reflect the risk and intended use of individual devices.
