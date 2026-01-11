Here is the full **README.md** in English, following the layout of STHGCN and incorporating your updated dataset statistics.

---

# MSAHG: Multifaceted Scenario-Aware Hypergraph Learning

This repository provides the official implementation of the paper **Multifaceted Scenario-Aware Hypergraph Learning for Next POI Recommendation**, accepted by **AAAI 2026**.

MSAHG is a novel framework designed to address the oversight of mobility variations across distinct contextual scenarios (e.g., tourists vs. locals, weekdays vs. weekends) in Next POI recommendation. It adopts a **scenario-splitting paradigm** to capture scenario-specific features through disentangled sub-hypergraphs and introduces an **Adaptive Parameter Splitting (APS)** mechanism to resolve optimization conflicts between scenarios.

* **Disentangled Sub-hypergraphs**
* **Model Framework**

![MSAHG Overall Framework](model.pdf)

## Core Contributions

* **Multifaceted Scenario Definition**: We define composite scenarios across three orthogonal dimensions: user type (local/tourist), temporal context (weekday/weekend), and spatial area (urban/suburban).
* **Disentangled Sub-hypergraph Construction**: We construct scenario-specific sub-hypergraphs (Collaborative, Temporal, Geographic, and Transition views) to capture fine-grained mobility semantics.
* **Adaptive Parameter Splitting (APS)**: A dynamic mechanism that monitors gradient similarity across scenarios and adaptively splits conflicting parameters, balancing scenario-specific adaptation with global generalization.

---

## Installation

1. **Clone the repository**:
```shell
git clone https://github.com/YourUsername/MSAHG.git
cd MSAHG

```


2. **Environment Requirements**:
The repository has several important dependencies:
* Python 3.12+
* PyTorch 2.4.1+
* CUDA 12.1+
* Recommended Hardware: NVIDIA A40 (24GB+ VRAM) or equivalent.


3. **Install dependencies**:
```shell
pip install -r requirements.txt

```



---

## Datasets

We evaluate MSAHG on three large-scale real-world datasets: **Gowalla**, **NYC**, and **TKY**. The multifaceted scenarios are classified based on residence status, timestamps, and geofencing.

### Dataset and Multi-scenario Statistics

| Metric | Gowalla | NYC | TKY |
| --- | --- | --- | --- |
| **Basic Statistics** |  |  |  |
| Users | 3,996 | 1,743 | 1,383 |
| POIs | 9,823 | 7,289 | 17,023 |
| Check-ins | 238,488 | 57,327 | 507,260 |
| Trajectories | 24,499 | 6,102 | 41,374 |
| **Multi-scenario Categories** |  |  |  |
| Local Users | 3,219 | 1,146 | 1,259 |
| Tourists | 777 | 597 | 124 |
| Downtown POIs | 7,229 | 5,291 | 11,742 |
| Suburban POIs | 2,603 | 1,998 | 5,281 |
| Workday Trajectories | 15,706 | 4,174 | 28,792 |
| Weekend Trajectories | 8,793 | 1,928 | 12,582 |

---

## Usage

### Training

To train MSAHG with default settings (including the Adaptive Parameter Splitting process):

```shell
python main.py --dataset nyc --batch_size 200 --lr 0.001 --split_epoch 20

```

* `--dataset`: Choose from `nyc`, `tky`, or `gowalla`.
* `--split_epoch`: The epoch when the APS mechanism starts detecting conflicts (suggested: 20 for NYC/Gowalla, 30 for TKY).

### Evaluation

The model evaluates performance using **Acc@k** (k=1, 5, 10) and **MRR**. Results will be saved in the `results/` directory.

---

## Experimental Results

MSAHG consistently outperforms state-of-the-art baselines across all datasets.

| Model | Dataset | Acc@1 | Acc@5 | Acc@10 | MRR |
| --- | --- | --- | --- | --- | --- |
| **MSAHG (Ours)** | **NYC** | **0.1983** | **0.3854** | **0.4632** | **0.2831** |
| STHGCN | NYC | 0.1652 | 0.3405 | 0.4177 | 0.2491 |
| DCHL | NYC | 0.1601 | 0.3341 | 0.4093 | 0.2435 |
| GETNext | NYC | 0.1492 | 0.3118 | 0.3804 | 0.2241 |

*(Detailed analysis and ablation studies are available in the paper.)*

---

## Citation

If you find our work or code useful for your research, please cite our paper:

```bibtex
@inproceedings{lin2026msahg,
  title={Multifaceted Scenario-Aware Hypergraph Learning for Next POI Recommendation},
  author={Lin, Yuxi and Li, Yongkang and Xing, Jie and Fan, Zipei},
  booktitle={Proceedings of the AAAI Conference on Artificial Intelligence (AAAI)},
  year={2026}
}

```

## Acknowledgements

The implementation of hypergraph convolution is partly inspired by [STHGCN](https://github.com/ant-research/Spatio-Temporal-Hypergraph-Model). We thank the authors for their contributions to the community.

---

**Next step**: I can help you write a `requirements.txt` based on the versions listed above, or help you draft the `argparse` configuration for your `main.py` if needed.
