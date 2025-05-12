

# SocioDiff Synthetic Load Dataset

This repository provides the synthetic residential load dataset generated using the **SocioDiff** framework, as described in our paper:

> **"SocioDiff: A Socio-aware Diffusion Model for Residential Load Data Generation"**
> \[Under review at IEEE Transactions on Smart Grid]

## 📘 Overview

The **SocioDiff Dataset** aims to support research in energy consumption forecasting, synthetic data generation, and socio-demographic behavior modeling. It simulates realistic residential electricity load profiles based on a combination of real socio-demographic information and learned consumption patterns.

We also plan to release the full source code upon the acceptance of the associated paper. The code repository is hosted at: [https://github.com/Intelligame/SocialDiff\_code](https://github.com/Intelligame/SocialDiff_code).

## 🧩 Dataset Description

Each sample in the dataset consists of:

* **Input**: socio-demographic features (e.g., income level, household size, education, age group, etc.)
* **Output**: a daily electricity load time series of 336 time steps (30-minute intervals for one week)

The dataset is generated using a conditional diffusion model trained on a proprietary dataset of 4,000 households collected over 3 years. For privacy reasons, the original data is not released. This synthetic version mimics its statistical characteristics without leaking private information.


## 📂 Data Source

The original real-world load data used to train the SocioDiff model is the **Commission for Energy Regulation (CER) Smart Metering Project dataset**, which contains electricity consumption data for Irish residential consumers. The CER dataset is publicly available from the Irish Social Science Data Archive (ISSDA) and can be accessed at the following link:

🔗 [https://www.ucd.ie/issda/data/commissionforenergyregulationcer/](https://www.ucd.ie/issda/data/commissionforenergyregulationcer/)

Please note that access may require agreement to ISSDA’s data usage terms.



### ⚙️ Social Characteristics Used in Conditioning

The following socio-demographic attributes are used in SocioDiff for conditional generation. Underrepresented groups—those with lower presence in the dataset—are marked in **bold**, as they are particularly important for fairness-aware data modeling.


| No. | Social Characteristic | Class Labels                                                               |
| --- | --------------------- | -------------------------------------------------------------------------- |
| 1   | Social class          | 1: AB<br>2: C1-C2<br>**3: DE**                                             |
| 2   | Age of income earner  | **1: Young (≤ 35)**<br>2: Medium (35\~65)<br>3: Old (> 65)                 |
| 3   | Live alone            | **1: Yes**<br>2: No                                                        |
| 4   | Employment status     | **1: Unemployed**<br>2: Employed                                           |
| 5   | Income                | **1: Poor (≤ 30,000)**<br>2: Medium (30,000\~75,000)<br>3: Rich (> 75,000) |

---

These socio-demographic features are extracted from the **[RESIDENTIAL PRE TRIAL SURVEY](https://github.com/Intelligame/SocialDiff/blob/main/RESIDENTIAL%20PRE%20TRIAL%20SURVEY.doc)**, which was conducted as part of the Irish CER Smart Metering Project. The survey collected detailed information on household composition, income, employment, and other social attributes before the metering trial. This structured metadata provides a reliable foundation for conditioning the generative model and ensuring that the resulting synthetic load profiles reflect real-world demographic diversity.

## 🧪 Generation Method

The data is produced using a **conditional diffusion model** trained to map structured socio-demographic features to residential load patterns. The model captures both temporal patterns and socio-contextual variations, enabling the generation of realistic and diverse consumption profiles.

Detailed methodology is available in Section III of our paper.


## 📁 Files

* `generated_data/pred_data.csv`: tabular data where each row contains socio-demographic attributes and the corresponding generated 336-length load sequence.

## 📊 Format Example

```csv
social,age,alone,employment,income,load_t0,load_t1,...,load_t335
DE,Old,Alone,Unemployed,Poor,0.10439315,0.12021788,...,0.28655297
```

Each row represents a synthetic weekly electricity consumption profile for one household, conditioned on its socio-demographic attributes.

* The fields `load_t0` to `load_t335` represent **336 consecutive load measurements**, each spaced at **30-minute intervals**, covering a full **7-day period** (48 points per day × 7 days).



## 🛠️ How to Use the Dataset

This dataset is designed to support downstream tasks such as residential load forecasting, fairness-aware modeling, and social behavior analysis. Below is a guide on how to use it effectively:

### 1. Load Forecasting Task

To use the dataset for short-term or day-ahead load forecasting:

* Treat `load_t0` to `load_t287` (first 6 days) as input
* Predict `load_t288` to `load_t335` (7th day)
* Optionally include socio-demographic fields as auxiliary inputs

### 2. Suggested Preprocessing

* Convert categorical attributes to one-hot or embedding indices if using neural networks
* Denormalize load values if needed (currently values are normalized to \[0, 1])
* Apply sliding windows if you wish to create multiple overlapping samples per household

### 3. Example Use Case (PyTorch-style input)

```python
import pandas as pd
data = pd.read_csv("generated_data/pred_data.csv")

X_social = data[['social', 'age', 'alone', 'employment', 'income']]
X_load = data[[f'load_t{i}' for i in range(288)]]
y_load = data[[f'load_t{i}' for i in range(288, 336)]]
```

This format allows you to train models that predict future electricity usage conditioned on both historical consumption and socio-demographic context.

---



## 📜 License

This dataset is released under the **CC BY-NC 4.0** License. You are free to use, adapt, and share it for **non-commercial research purposes**, provided that you cite the original paper.

## 📝 Citation

If you use this dataset in your research, please cite:

```bibtex
@article{SocioDiff2025,
  title={SocioDiff: A Socio-aware Diffusion Model for Residential Load Data Generation},
  author={Chen, Weilong and others},
  journal={IEEE Transactions on Smart Grid},
  year={2025},
  note={Under review}
}
```

## 📬 Contact

For questions or collaborations, please contact:

**Weilong Chen**

University of Electronic Science and Technology of China

Email: [chenweilong921@gmail.com](mailto:chenweilong921@gmail.com)

