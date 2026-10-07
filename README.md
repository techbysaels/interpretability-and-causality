# 🔎 Interpretability and Causality

## Introduction to the Repository

This repository explores a practical question that comes up repeatedly in applied machine learning: **a model can make a useful prediction without giving us enough information to understand, trust, or act on it responsibly?**.

The repository separates two ideas that are often mixed together. **Interpretability** helps explain how a model arrived at an output or which features contributed to it. **Causality** asks a different question: whether changing a factor would actually change the outcome. A feature can be highly predictive and easy to explain without being causal, and a model can be accurate while still relying on unstable shortcuts, proxies, or relationships that should not guide an intervention.

The use cases move across insurance, medical AI, public-sector decisions, autonomous systems, and computer vision. Together they show why model quality has to be evaluated at more than one level: predictive performance, explanation quality, causal meaning, human use, and operational risk.

## Repository Map

| Document | Use case | Core question | Main takeaway |
|---|---|---|---|
| [automobile-insurance-and-telematics](https://github.com/techbysaels/interpretability-and-causality/blob/aa77f9925d5da542f6ac84b1ee163122ce2705be/automobile-insurance-and-telematics.md) | Automobile insurance pricing with telematics | How can new behavioral sensor data improve prediction without changing the causal meaning of established rating factors? | Keep causal interpretation separate from incremental predictive value. The proposed approach anchors the existing pricing model and adds telematics as a separate risk layer, with controls for provenance, leakage, exposure, fairness, privacy, and vendor change. |
| [interpretability-in-medical-devices](https://github.com/techbysaels/interpretability-and-causality/blob/aa77f9925d5da542f6ac84b1ee163122ce2705be/interpretability-in-medical-devices.md) | Evaluation of AI-enabled medical devices | What evidence is needed before a medical AI system can be trusted beyond the dataset or hospital where it was developed? | External validation, clinically meaningful metrics, subgroup analysis, uncertainty, drift monitoring, transparency, and clearly defined stakeholder responsibilities are part of model quality—not optional documentation. |
| [risks-of-lack-interpretability-and-causality](https://github.com/techbysaels/interpretability-and-causality/blob/24e1cf89f39cab2e1e4ae09a34d9a9b0852b505e/risks-of-lack-interpretability-and-causality.md) | High-impact failures and everyday neural-network applications | What happens when humans receive a model output without enough information to understand uncertainty, drivers, or failure modes? | Human-in-the-loop is only useful when the human has enough information to challenge the model. Interpretability needs to exist at the model and system level, especially when decisions affect rights, safety, budgets, or access to services. |
| [image-classification-interpretability](https://github.com/techbysaels/interpretability-and-causality/blob/aa77f9925d5da542f6ac84b1ee163122ce2705be/image-classification-interpretability/Image_Classification_Interpretability.ipynb) | Code example: Integrated Gradients for image classification | Which pixels contribute most to an Inception V1 prediction? | Integrated Gradients makes local feature attribution visible. In the coyote example, the model assigns 90.1% probability to coyote, and the attribution is concentrated mainly on the animal rather than the snow background. The method improves interpretability but does not establish causality. |

## Why Interpretability Matters in AI

A prediction is easier to trust when engineers and domain experts can inspect the evidence behind it. The materials in this repository show several reasons this matters.

In medical AI, a model may perform well at one institution and degrade elsewhere because populations, equipment, workflows, or data distributions differ. An explanation layer can help identify whether a model is using clinically plausible information or site-specific signals, but the broader validation process still needs external testing, subgroup analysis, uncertainty reporting, and drift monitoring.

The public-benefit and autonomous-driving examples make the human side equally important. A reviewer who receives only a risk score may simply confirm it rather than provide meaningful oversight. In a safety-critical system, engineers also need to reconstruct how classifications and uncertainty changed over time and why a safer response was—or was not—triggered.

## Why Causality Matters in AI

Interpretability and causality answer different questions. Knowing that a feature contributed to a prediction does not tell us that changing that feature will change the real-world outcome.

The automobile-insurance case makes this distinction concrete. Traditional rating variables such as age, vehicle characteristics, territory, prior claims, and exposure can be joined with telematics such as braking, acceleration, speed patterns, turning, trip frequency, and nighttime driving. Adding every available variable directly into one model may improve prediction while changing the meaning of existing coefficients. A behavioral variable can sit downstream of an existing factor, act as a proxy, or duplicate information already captured elsewhere.

The proposed design therefore separates the **baseline causal component** from an **incremental telematics prediction layer**. That preserves the original causal interpretation while still allowing new data to contribute predictive information. It also forces an engineering team to document what each feature means, prevent temporal leakage, account for exposure, validate by subgroup, monitor missingness, and independently test third-party inputs before they affect pricing.

This is a useful repository principle beyond insurance: **do not infer an intervention from a predictive relationship unless the causal question has actually been defined and supported**.

## Code Example: Integrated Gradients

The notebook [image-classification-interpretability.ipynb](https://github.com/techbysaels/interpretability-and-causality/blob/aa77f9925d5da542f6ac84b1ee163122ce2705be/image-classification-interpretability/Image_Classification_Interpretability.ipynb) turns the interpretability discussion into an executable workflow using a pretrained Inception V1 image classifier and Integrated Gradients.

The notebook walks through the method from first principles: establishing a black-image baseline, interpolating between the baseline and the observed image, computing target-class gradients, approximating the integral, and rendering the resulting attribution mask.

The saved coyote prediction is **90.1%**, with timber wolf and grey fox as the next alternatives. The attribution is concentrated mainly around the coyote's body contour and back, with additional signal around the face and ears, while the snow background receives relatively little emphasis. That is a useful local diagnostic, but it is not evidence that the model will generalize to every coyote image or that the highlighted pixels are causal features of the animal in the real world.

## Repository Takeaways

Across the repository, the same engineering pattern appears in different forms:

- Accuracy and confidence are necessary but incomplete measures of model quality.
- Local explanations help identify shortcuts, proxies, and unexpected model behavior.
- Interpretability must be designed for the people who will actually use or challenge the model output.
- Causal interpretation should be protected when new predictive features are introduced.
- High-impact systems require external validation, uncertainty reporting, drift monitoring, and clear escalation paths.
- Explanation methods support auditing and debugging, but they do not convert correlation into causation.

The repository is intended as a practical record of how I approach model review: not only asking whether a model performs well, but also **what it learned, why its output is plausible, what that explanation does not prove, and what evidence would be needed before using the result in a real decision**.
