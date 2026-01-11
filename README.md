# MSAHG: Multifaceted Scenario-Aware Hypergraph Learning

This repository provides the official implementation of the paper **Multifaceted Scenario-Aware Hypergraph Learning for Next POI Recommendation**, accepted by **AAAI 2026**.

MSAHG is a novel framework designed to address the oversight of mobility variations across distinct contextual scenarios (e.g., tourists vs. locals, weekdays vs. weekends) in Next POI recommendation. It adopts a **scenario-splitting paradigm** to capture scenario-specific features through disentangled sub-hypergraphs and introduces an **Adaptive Parameter Splitting (APS)** mechanism to resolve optimization conflicts between scenarios.

* **Model Framework**

![MSAHG Overall Framework](model.pdf)


## Core Contributions

* **Multifaceted Scenario Definition**: We define composite scenarios across three orthogonal dimensions: user type (local/tourist), temporal context (weekday/weekend), and spatial area (urban/suburban).
* **Disentangled Sub-hypergraph Construction**: We construct scenario-specific sub-hypergraphs (Collaborative, Temporal, Geographic, and Transition views) to capture fine-grained mobility semantics.
* **Adaptive Parameter Splitting**: A dynamic mechanism that monitors gradient similarity across scenarios and adaptively splits conflicting parameters, balancing scenario-specific adaptation with global generalization.

---

## Installation

1. **Clone the repository**:

```shell
git clone https://github.com/COCOMiss/MSAHG.git
cd MSAHG

```

2. **Environment Requirements**:
The repository has several important dependencies:

* Python 3.12+
* PyTorch 2.4.1+
* CUDA 12.1+

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
* `--split_epoch`: The epoch when the Adaptive Parameter Splitting mechanism starts detecting conflicts (suggested: 20 for NYC/Gowalla, 30 for TKY).

### Evaluation

The model evaluates performance using **Acc@k** (k=1, 5, 10, 20) and **MRR**. Results will be saved in the `results/` directory.

---

## Experimental Results

MSAHG achieves state-of-the-art performance in 53.3% of evaluation metrics (48/90 cases) and ranks second in 33.3% (30/90), securing top-two positions in 86.7% of all scenario-metric combinations.

### Multi-Scenario Performance Comparison

The following table compares MSAHG against state-of-the-art baselines across different multifaceted scenarios:

| Model | Scenario | Gowalla (Acc@1 / MRR) | NYC (Acc@1 / MRR) | TKY (Acc@1 / MRR) |
| --- | --- | --- | --- | --- |
| **HSTLSTM** | Local | 0.1314 / 0.2014 | 0.2020 / 0.2809 | 0.2159 / 0.2978 |
|  | Tourist | 0.1079 / 0.1714 | 0.1298 / 0.1886 | 0.1679 / 0.2387 |
| **DeepMove** | Local | 0.1343 / 0.2122 | 0.1603 / 0.2382 | 0.1756 / 0.2698 |
|  | Tourist | 0.1074 / 0.1751 | 0.1178 / 0.1722 | 0.1455 / 0.2254 |
| **GETNext** | Local | 0.1556 / 0.2432 | 0.1782 / 0.2398 | 0.1416 / 0.2479 |
|  | Tourist | 0.0785 / 0.1329 | 0.0714 / 0.1519 | 0.0213 / 0.0771 |
| **STHGCN** | Local | 0.1433 / 0.2115 | 0.1730 / 0.2533 | 0.2283 / 0.3271 |
|  | Tourist | 0.0543 / 0.1168 | 0.1841 / 0.2663 | 0.1392 / 0.2073 |
| **DCHL** | Local | 0.1364 / 0.2203 | 0.1463 / 0.2408 | 0.1190 / 0.2072 |
|  | Tourist | 0.0752 / 0.1569 | 0.1029 / 0.1559 | 0.0658 / 0.1391 |
| **MSAHG** | **Local** | **0.1629 / 0.2386** | **0.2026 / 0.3483** | **0.2076 / 0.3175** |
| (Ours) | **Tourist** | **0.1059 / 0.1885** | **0.1921 / 0.3201** | **0.1402 / 0.2334** |
|  | **Downtown** | **0.1871 / 0.2723** | **0.2947 / 0.4666** | **0.2132 / 0.3358** |
|  | **Suburban** | **0.1540 / 0.2310** | **0.1816 / 0.3013** | **0.1993 / 0.2927** |



