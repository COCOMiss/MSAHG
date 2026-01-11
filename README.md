# MSAHG: Multifaceted Scenario-Aware Hypergraph Learning

This repository contains the official PyTorch implementation of the paper **Multifaceted Scenario-Aware Hypergraph Learning for Next POI Recommendation**, which has been submitted to/accepted by **AAAI 2026**.

MSAHG is a novel framework designed to address the oversight of mobility variations across distinct contextual scenarios (e.g., tourists vs. locals, weekdays vs. weekends) in Next POI recommendation. It adopts a **scenario-splitting paradigm** to capture scenario-specific features through disentangled sub-hypergraphs and introduces an **Adaptive Parameter Splitting (APS)** mechanism to resolve optimization conflicts between scenarios.

* **The Multifaceted Scenarios in Next POI Recommendation**
* **Overall Model Framework**

## Core Contributions

* **Multifaceted Scenario Definition**: We define composite scenarios across three orthogonal dimensions: user type (local/tourist), temporal context (weekday/weekend), and spatial area (urban/suburban).
* **Disentangled Sub-hypergraph Construction**: We construct scenario-specific sub-hypergraphs (Collaborative, Temporal, Geographic, and Transition views) to capture fine-grained mobility semantics.
* **Adaptive Parameter Splitting (APS)**: A dynamic mechanism that monitors gradient similarity across scenarios and adaptively splits conflicting parameters, balancing scenario-specific adaptation with global generalization.

## Installation

1. Clone the repository:
```shell
git clone https://github.com/YourUsername/MSAHG.git
cd MSAHG

```


2. **Environment Requirements**:
* Python 3.12+
* PyTorch 2.4.1+
* CUDA 12.1+
* Recommended Hardware: NVIDIA A40 (24GB+ VRAM) or equivalent.


3. Install dependencies:
```shell
pip install -r requirements.txt

```



## Datasets

We evaluate MSAHG on three large-scale real-world datasets: **Gowalla**, **NYC**, and **TKY**.

* **Preprocessing**: Traces are segmented into sessions and classified into multifaceted scenarios based on residence status, timestamps, and geofencing as described in the paper.

| Dataset | #Users | #POIs | #Check-ins | #Scenarios |
| --- | --- | --- | --- | --- |
| NYC | 4,008 | 6,052 | 163,892 | 8 |
| TKY | 5,595 | 8,367 | 258,416 | 8 |
| Gowalla | 8,375 | 9,845 | 316,247 | 8 |

## Usage

### Training

To train MSAHG with the default settings (including the Adaptive Parameter Splitting process):

```shell
python main.py --dataset nyc --batch_size 200 --lr 0.001 --split_epoch 20

```

* `--dataset`: Choose from `nyc`, `tky`, or `gowalla`.
* `--split_epoch`: The epoch when the APS mechanism starts detecting conflicts (suggested: 20 for NYC/Gowalla, 30 for TKY).

### Evaluation

The model evaluates performance using **Acc@k** (k=1, 5, 10) and **MRR**. Results will be saved in the `results/` directory.

## Experimental Results

MSAHG consistently outperforms state-of-the-art baselines (including STHGCN, DCHL, and GETNext) across all datasets.

| Model | Dataset | Acc@1 | Acc@5 | Acc@10 | MRR |
| --- | --- | --- | --- | --- | --- |
| **MSAHG** | **NYC** | **0.1983** | **0.3854** | **0.4632** | **0.2831** |
| STHGCN | NYC | 0.1652 | 0.3405 | 0.4177 | 0.2491 |
| DCHL | NYC | 0.1601 | 0.3341 | 0.4093 | 0.2435 |
| GETNext | NYC | 0.1492 | 0.3118 | 0.3804 | 0.2241 |

*(Detailed results for TKY and Gowalla can be found in our paper.)*

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

The hypergraph implementation is partly inspired by [STHGCN](https://github.com/ant-research/Spatio-Temporal-Hypergraph-Model). We thank the authors for their contributions to the community.
