Security Assessment of a Face Recognition System 



\## Authors



\* 

\*\*Alessio Donato Giura\*\* - Group 03, University of Salerno 





\* 

\*\*Lucia Nancy Lavista\*\* 





\* 

\*\*Alessandro Maruotto\*\* 





\* 

\*\*Michele Penna\*\* 







\---



\## Project Description



This project evaluates the robustness of a face recognition system based on deep neural networks against adversarial evasion attacks with bounded intensity. The study explores vulnerabilities in White-Box and Black-Box scenarios to measure attack transferability. It also proposes defense mechanisms to mitigate threats, analyzing the architectural trade-off between strict security and system usability.



\---



\## Main Objectives



\* 

\*\*Baseline Evaluation:\*\* Measure the initial operational accuracy of a model on a clean dataset.





\* 

\*\*Attack Generation:\*\* Create untargeted and targeted adversarial examples bounded spatially by the $L\_{\\infty}$ norm with a maximum perturbation budget of $\\epsilon=0.10$.





\* 

\*\*Transferability Analysis:\*\* Verify the effectiveness and degradation of generated attacks when blindly applied to a target classifier with a different architecture to test adversarial overfitting.





\* 

\*\*Defense Implementation:\*\* Develop and evaluate mitigation mechanisms, including preprocessing via JPEG compression and Zero Trust architectures with anomaly detection in the latent space.







\---



\## Architecture and Dataset



\* 

\*\*Dataset:\*\* Balanced subset extracted from VGGFace2, consisting of 100 identities (50 male and 50 female) for a total of 1000 images, extracted via a streaming pipeline to optimize disk usage.







| Model | Architecture | Role in Threat Model | Baseline Accuracy |

| --- | --- | --- | --- |

| \*\*NN1\*\* | Inception-ResNet-v1 | Surrogate Model (White-Box) 



&#x20;| 84.50% 



&#x20;|

| \*\*NN2\*\* | ResNet-50 | Target Model (Black-Box) 



&#x20;| 88.70% 



&#x20;|



\---



\## Evaluated Attacks



\* 

\*\*Implementation Framework:\*\* The entire suite of attacks was implemented leveraging the Adversarial Robustness Toolbox (ART).





\* 

\*\*Fast Gradient Sign Method (FGSM):\*\* Basic single-step attack.





\* 

\*\*Basic Iterative Method (BIM):\*\* Iterative extension for granular gradient computation.





\* 

\*\*Projected Gradient Descent (PGD):\*\* The universal first-order adversary, equipped with stochastic initialization.





\* 

\*\*DeepFool:\*\* Geometric optimization aimed at finding the minimum displacement necessary to cross decision boundaries.





\* 

\*\*Carlini \& Wagner ($L\_{\\infty}$):\*\* Advanced optimization algorithm on logits to minimize distortion while guaranteeing evasion, which was successfully fixed via monkey patching for the targeted variant.







\---



\## Defense Strategies



\* 

\*\*Input Transformation (JPEG Compression):\*\* Tested as a spatial low-pass filter, this defense proved largely ineffective against optimized iterative attacks like PGD and BIM. This demonstrates that modern adversarial perturbations do not reside exclusively in the high-frequency spectrum.





\* 

\*\*Adversarial Detector in Latent Space (Zero Trust Architecture):\*\* A Random Forest classifier was trained to discriminate 512-dimensional embeddings extracted from the neural network.





\* 

\*\*Security-Usability Trade-off:\*\* The optimal operational configuration, trained on PGD, BIM, and CW, reduced the residual attack success rate to almost 0%. However, this highlighted an inevitable usability cost, generating a False Positive Rate (FPR) of 26.5% on legitimate users.







\---



\## Technology Stack



\* 

\*\*Language:\*\* Python 3.





\* 

\*\*Main Libraries:\*\* PyTorch, torchvision, Adversarial Robustness Toolbox (ART), numpy, pandas, Pillow (PIL).





\* 

\*\*Execution Environment:\*\* Google Colab with GPU hardware acceleration (NVIDIA A100/T4) and state management via checkpointing on Google Drive.

