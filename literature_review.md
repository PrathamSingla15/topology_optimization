# Most Relevant Recent Papers for the BTP

The project aims to optimize a biodegradable implant across its full service life rather than only at implantation. Its proposed framework links evolving implant geometry, structural stiffness, corrosion, load transfer to bone, and bone remodeling, while using a matrix-free GPU solver to keep the repeated multiphysics analyses computationally practical.

Within this shortlist, the literature is strong on individual parts of that chain, but no selected paper demonstrates the exact combination proposed in the deck. This suggests an unresolved integration problem: coupling a reaction-diffusion corrosion model with mechanics and remodeling feedback, then solving the resulting time-dependent optimization efficiently on a GPU.

## Ranked shortlist

### 1. Li et al. (2026) - closest overall methodological match

Li, C., Zhang, M., Ji, J., Xu, X., & Luo, Z. (2026). Topology optimization of biodegradable structures with phase-field corrosion modeling. *Computer Methods in Applied Mechanics and Engineering, 461*, 119159. [https://doi.org/10.1016/j.cma.2026.119159](https://doi.org/10.1016/j.cma.2026.119159)

- **Why it matters:** This is the closest end-to-end precedent because corrosion-driven geometry evolution is placed directly inside a topology-optimization loop.
- **What it contributes:** Phase-field corrosion, post-corrosion compliance constraints, and time-dependent adjoint sensitivities provide a strong reference architecture for degradation-aware optimization.
- **Caveat:** The version of record was published online in 2026 and is assigned to the November 2026 issue. Its phase-field formulation should not be presented as equivalent to the reaction-diffusion corrosion model proposed in the deck.
- **Deck-pillar mapping:** Corrosion + mechanics + degradation-aware topology optimization.

**PPT-ready blurb (41 words):** This paper integrates phase-field corrosion directly into topology optimization and derives time-dependent adjoint sensitivities to control post-corrosion compliance. It is the closest methodological match to our framework, but its phase-field degradation model is not the same as our planned reaction-diffusion formulation.

### 2. Sun et al. (2024) - strongest bridge to bone remodeling

Sun, H., Ding, X., Xu, S., Duan, P., Xiong, M., & Zhang, H. (2024). 具有时变刚度的骨折内固定植入物结构设计及骨重塑效果评估 [Structural design and evaluation of bone remodeling effect of fracture internal fixation implants with time-varying stiffness]. *Journal of Biomedical Engineering, 41*(3), 595–603. [https://doi.org/10.7507/1001-5515.202311037](https://doi.org/10.7507/1001-5515.202311037)

- **Why it matters:** It connects degradation-aware, time-varying implant stiffness to a downstream bone-remodeling outcome in a tibial fixation-plate example.
- **What it contributes:** A variable-density, dual-material topology design based on different degradation rates and elastic moduli, followed by remodeling-based comparison of the optimized plate.
- **Caveat:** The article is in Chinese, with an English abstract. Bone remodeling is used to evaluate the optimized design after optimization; it is not coupled back into the optimization loop.
- **Deck-pillar mapping:** Mechanics + time-varying stiffness + post-optimization bone-remodeling evaluation.

**PPT-ready blurb (40 words):** This study topology-optimizes a dual-material fixation plate for time-varying stiffness under degradation, then evaluates the optimized design using a bone-remodeling simulation. It directly motivates our mechanics-to-remodeling link, although remodeling is a post-optimization assessment rather than a fully coupled design variable.

### 3. Kovačević et al. (2023) - strongest corrosion-physics reference

Kovačević, S., Ali, W., Martínez-Pañeda, E., & LLorca, J. (2023). Phase-field modeling of pitting and mechanically-assisted corrosion of Mg alloys for biomedical applications. *Acta Biomaterialia, 164*, 641–658. [https://doi.org/10.1016/j.actbio.2023.04.011](https://doi.org/10.1016/j.actbio.2023.04.011)

- **Why it matters:** It addresses magnesium corrosion in body-fluid-like environments and includes localized pitting and the interaction between mechanical loading and corrosion.
- **What it contributes:** A physically based diffuse-interface model that combines magnesium dissolution and ion transport, with validation against in-vitro magnesium-wire measurements and implant-relevant numerical examples.
- **Caveat:** This is a phase-field corrosion model, not a reaction-diffusion implementation or a complete topology-optimization/remodeling framework.
- **Deck-pillar mapping:** Corrosion physics + mechano-chemical coupling + biomedical degradation validation.

**PPT-ready blurb (39 words):** This phase-field model covers uniform, pitting, and mechanically assisted corrosion of magnesium alloys in body-fluid-like environments, and was calibrated and validated against in-vitro Mg-wire data. It provides a valuable validation strategy, but does not establish the planned reaction-diffusion equations.

### 4. Zhao et al. (2024) - strongest computational-scaling reference

Zhao, J., Qi, T., & Wang, C. (2024). Efficient GPU accelerated topology optimization of composite structures with spatially varying fiber orientations. *Computer Methods in Applied Mechanics and Engineering, 421*, 116809. [https://doi.org/10.1016/j.cma.2024.116809](https://doi.org/10.1016/j.cma.2024.116809)

- **Why it matters:** It demonstrates how large topology-optimization problems with spatially varying material behavior can be made tractable on GPUs.
- **What it contributes:** An MGPCG solver, template-based stiffness representation, and GPU matrix-vector strategies that reduce stiffness storage and repeated linear-solve cost.
- **Caveat:** The validation concerns spatially varying composite structures. It supports the solver design, not biomedical validity, corrosion behavior, or bone remodeling.
- **Deck-pillar mapping:** Matrix-efficient finite-element operations + MGPCG + GPU-accelerated topology optimization.

**PPT-ready blurb (42 words):** This work combines GPU acceleration with an MGPCG solver and matrix-efficient stiffness operations for large-scale topology optimization of spatially varying composites. It supports our computational strategy, but it validates solver scalability in composite structures, not biodegradation, bone remodeling, or biomedical implant performance.

## Overall synthesis and remaining gap

Together, these papers support the four building blocks of the proposed study and, within this shortlist, suggest an unresolved integration problem: Li et al. couple corrosion and optimization without remodeling; Sun et al. evaluate remodeling only after optimization; Kovačević et al. provide phase-field corrosion physics; and Zhao et al. establish GPU solver scalability outside the biomedical setting. None provides the deck's exact reaction-diffusion PDE formulation. The phase-field papers support the coupling architecture and validation strategy, while equation selection and calibration remain project tasks. The BTP should therefore frame its contribution as integrating and testing these blocks, not as claiming that any one paper validates the complete framework.

**Source verification:** Bibliographic metadata and DOI status were checked against publisher/Crossref records for Li, Kovačević, and Zhao, and against PubMed/PMC for Sun (PMID 38932547). The publisher confirms that Li is available online; Crossref records its November 2026 issue assignment, and no Crossref online-publication date is asserted here. Method claims were limited to the corresponding abstracts and publisher highlights.

## Exact text for the PPT slide

**Li et al. (2026; published online and assigned to the November 2026 issue), *Computer Methods in Applied Mechanics and Engineering*.** This paper integrates phase-field corrosion directly into topology optimization and derives time-dependent adjoint sensitivities to control post-corrosion compliance. It is the closest methodological match to our framework, but its phase-field degradation model is not the same as our planned reaction-diffusion formulation.

**Sun et al. (2024), *Journal of Biomedical Engineering*.** This study topology-optimizes a dual-material fixation plate for time-varying stiffness under degradation, then evaluates the optimized design using a bone-remodeling simulation. It directly motivates our mechanics-to-remodeling link, although remodeling is a post-optimization assessment rather than a fully coupled design variable.

**Kovačević et al. (2023), *Acta Biomaterialia*.** This phase-field model covers uniform, pitting, and mechanically assisted corrosion of magnesium alloys in body-fluid-like environments, and was calibrated and validated against in-vitro Mg-wire data. It provides a valuable validation strategy, but does not establish the planned reaction-diffusion equations.

**Zhao et al. (2024), *Computer Methods in Applied Mechanics and Engineering*.** This work combines GPU acceleration with an MGPCG solver and matrix-efficient stiffness operations for large-scale topology optimization of spatially varying composites. It supports our computational strategy, but it validates solver scalability in composite structures, not biodegradation, bone remodeling, or biomedical implant performance.
