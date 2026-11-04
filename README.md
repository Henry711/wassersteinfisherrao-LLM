Can reformulating the training objective as an unbalanced transport problem mitigate catastrophic forgetting in LLM's?

preliminary experiment: should take <3hrs on T4 GPU in Google Colab

main experiment: ca. 30hrs on T4 GPU in Google Colab

This method aims to reduce catastrophic forgetting in a replay free, task-free manner without warning between domain (mode) changes.

The model is treated as an unnormalised mixture of adapter components, M = Σ m_c ρ_c, fitted to the growing measure of all data seen so far. Each step has three parts:

E-step: sequences are assigned to components by exact Bayes, γ_c ∝ m_c ρ_c(x).
Fisher–Rao reaction: masses only grow with evidence.
Wasserstein transport: a component moves with step factor min(1, A·b_c/m_c), and the shared adapter with min(1, A·b/N).

New components are created where the data is not covered. Old knowledge becomes stiff in proportion to the evidence behind it, while new data is learned at full rate. The control BAL is the same algorithm with normalised masses.

Prior work this builds on:
Unbalanced optimal transport and WFR: Chizat, Peyré, Schmitzer & Vialard (2018); Liero, Mielke & Savaré (2018); Kondratyev, Monsaingeon & Vorotnikov (2016).
Related continual-learning ideas: mixtures learned online (online EM, Dirichlet-process mixtures), CN-DPM (Lee et al., 2020), mixtures of LoRA experts (e.g. Zadouri et al., 2023).
Baselines: EWC / online EWC (Kirkpatrick et al., 2017; Schwarz et al., 2018) and experience replay.
Models and adapters: Pythia (Biderman et al., 2023) and LoRA (Hu et al., 2021).

Data:
arXiv abstracts (gfissore/arxiv-abstracts-2021),
AG News,
German Wikipedia (wikimedia/wikipedia, CC BY-SA),
LAMBADA (EleutherAI/lambada_openai),
WikiText-103,


