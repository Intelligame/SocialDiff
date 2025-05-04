

# SocioDiff Synthetic Load Dataset

This repository provides the synthetic residential load dataset generated using the **SocioDiff** framework, as described in our paper:

> **"SocioDiff: A Socio-aware Diffusion Model for Residential Load Data Generation"**
> \[Under review at IEEE Transactions on Smart Grid]

## 📘 Overview

The **SocioDiff Dataset** aims to support research in energy consumption forecasting, synthetic data generation, and socio-demographic behavior modeling. It simulates realistic residential electricity load profiles based on a combination of real socio-demographic information and learned consumption patterns.

## 🧩 Dataset Description

Each sample in the dataset consists of:

* **Input**: socio-demographic features (e.g., income level, household size, education, age group, etc.)
* **Output**: a daily electricity load time series of 96 time steps (15-minute intervals for one day)

The dataset is generated using a conditional diffusion model trained on a proprietary dataset of 4,000 households collected over 3 years. For privacy reasons, the original data is not released. This synthetic version mimics its statistical characteristics without leaking private information.


## 📂 Data Source

The original real-world load data used to train the SocioDiff model is the **Commission for Energy Regulation (CER) Smart Metering Project dataset**, which contains electricity consumption data for Irish residential consumers. The CER dataset is publicly available from the Irish Social Science Data Archive (ISSDA) and can be accessed at the following link:

🔗 [https://www.ucd.ie/issda/data/commissionforenergyregulationcer/](https://www.ucd.ie/issda/data/commissionforenergyregulationcer/)

Please note that access may require agreement to ISSDA’s data usage terms.


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

