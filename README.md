# Gym Membership Churn Analysis

*[English](#english) | [Türkçe](#türkçe)*

---

## English

### Overview

A Python-only data analysis project on gym/fitness club membership churn. It combines statistical hypothesis testing with a logistic regression classification model to answer: **which member segments carry the highest churn risk, and what factors drive that risk?**

Full findings, methodology, and business recommendations are in [`REPORT.pdf`](./REPORT.pdf) (Turkish version: `REPORT_TR.pdf`). This README covers the technical/reproducibility side only.

### Dataset

- **Source:** "Model Fitness" fitness-club dataset — 4,000 members, 14 original features (synthetic data, used for portfolio purposes)
- `data/gym_churn_us.csv` — raw data
- `data/gym_churn_us_clean.csv` — after EDA (engineered features added: `frequency_drop`, `age_group`)
- `data/gym_churn_us_dummy.csv` — after feature engineering (dummy-encoded, model-ready)

### Tech stack

- **Python 3**, Jupyter Notebook
- `pandas`, `numpy` — data handling
- `matplotlib`, `seaborn` — visualization
- `scipy.stats` (`mannwhitneyu`, `chi2_contingency`) — hypothesis testing
- `statsmodels` (`Logit`, `variance_inflation_factor`) — inferential modeling & multicollinearity check
- `scikit-learn` (`train_test_split`, `confusion_matrix`, `classification_report`, `roc_auc_score`) — train/test split & model evaluation

### Repository structure

```
notebooks/
  01_quality_control.ipynb        data quality checks (nulls, duplicates, dtypes)
  02_exploratory_analysis.ipynb   EDA, feature engineering (frequency_drop, age_group), churn-rate breakdowns
  03_hypothesis_testing.ipynb     Mann-Whitney U + chi-square / Cramér's V tests
  04_feature_engineering.ipynb    correlation/VIF checks, dummy encoding, final model-ready dataset
  05_model.ipynb                  statsmodels.Logit model, coefficient interpretation, evaluation
data/
  gym_churn_us.csv
  gym_churn_us_clean.csv
  gym_churn_us_dummy.csv
README.md
REPORT.pdf
REPORT_TR.pdf
```

### Methodology summary

1. **Quality control** — verify no missing values / duplicates.
2. **EDA** — churn rate profiling across all variables; engineer `frequency_drop` and `age_group`.
3. **Hypothesis testing** — Mann-Whitney U (frequency_drop vs. churn), chi-square/Cramér's V (categorical variables vs. churn) to validate which variables are worth modeling.
4. **Feature engineering** — drop redundant/insignificant columns, one-hot encode categoricals, confirm no multicollinearity via VIF.
5. **Modeling** — `statsmodels.Logit` on an 80/20 stratified split; evaluate on the held-out test set (confusion matrix, precision/recall/F1, ROC-AUC).

### Headline results

- Overall churn rate: **26.5%**
- Model: ROC-AUC **0.972**, accuracy **93%**, churn-class precision **0.90** / recall **0.83**
- Strongest churn drivers (all p < 0.05): drop in class-attendance frequency, lack of group-class participation, short contract length, low tenure ("lifetime"), younger age group

### How to reproduce

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn jupyter
jupyter notebook notebooks/01_quality_control.ipynb
```

Run the notebooks in order (01 → 05); each one reads the CSV produced by the previous step and writes the CSV consumed by the next.

---

## Türkçe

### Genel Bakış

Python tabanlı bir spor salonu/fitness üyeliği churn (üye kaybı) analizi projesi. İstatistiksel hipotez testlerini bir lojistik regresyon sınıflandırma modeliyle birleştirerek şu soruyu yanıtlar: **hangi üye segmentleri en yüksek churn riskini taşıyor ve bu riski neler sürüklüyor?**

Detaylı bulgular, metodoloji ve iş önerileri [`REPORT.pdf`](./REPORT.pdf) dosyasında (Türkçe sürüm: `REPORT_TR.pdf`). Bu README sadece teknik/tekrarlanabilirlik tarafını kapsar.

### Veri Seti

- **Kaynak:** "Model Fitness" fitness salonu veri seti — 4.000 üye, 14 orijinal özellik (sentetik veri, portföy amaçlı kullanılmıştır)
- `data/gym_churn_us.csv` — ham veri
- `data/gym_churn_us_clean.csv` — EDA sonrası (üretilen özellikler eklenmiş: `frequency_drop`, `age_group`)
- `data/gym_churn_us_dummy.csv` — feature engineering sonrası (dummy encode edilmiş, modele hazır)

### Kullanılan Teknolojiler

- **Python 3**, Jupyter Notebook
- `pandas`, `numpy` — veri işleme
- `matplotlib`, `seaborn` — görselleştirme
- `scipy.stats` (`mannwhitneyu`, `chi2_contingency`) — hipotez testleri
- `statsmodels` (`Logit`, `variance_inflation_factor`) — çıkarımsal modelleme ve çoklu doğrusal bağlantı kontrolü
- `scikit-learn` (`train_test_split`, `confusion_matrix`, `classification_report`, `roc_auc_score`) — train/test ayrımı ve model değerlendirmesi

### Repo Yapısı

```
notebooks/
  01_quality_control.ipynb        veri kalite kontrolü (eksik değer, tekrar eden kayıt, veri tipleri)
  02_exploratory_analysis.ipynb   keşifsel veri analizi, feature engineering (frequency_drop, age_group), churn oranı kırılımları
  03_hypothesis_testing.ipynb     Mann-Whitney U + ki-kare / Cramér's V testleri
  04_feature_engineering.ipynb    korelasyon/VIF kontrolü, dummy encoding, modele hazır nihai veri seti
  05_model.ipynb                  statsmodels.Logit modeli, katsayı yorumu, değerlendirme
data/
  gym_churn_us.csv
  gym_churn_us_clean.csv
  gym_churn_us_dummy.csv
README.md
REPORT.pdf
REPORT_TR.pdf
```

### Metodoloji Özeti

1. **Kalite kontrolü** — eksik değer/tekrar eden kayıt olmadığının doğrulanması.
2. **EDA** — tüm değişkenler için churn oranı profillemesi; `frequency_drop` ve `age_group` özelliklerinin üretilmesi.
3. **Hipotez testleri** — Mann-Whitney U (frequency_drop vs. churn), ki-kare/Cramér's V (kategorik değişkenler vs. churn) ile hangi değişkenlerin modellemeye değer olduğunun doğrulanması.
4. **Feature engineering** — gereksiz/anlamsız sütunların çıkarılması, kategorik değişkenlerin one-hot encode edilmesi, VIF ile çoklu doğrusal bağlantı olmadığının teyidi.
5. **Modelleme** — %80/20 stratified split üzerinde `statsmodels.Logit`; test setinde değerlendirme (confusion matrix, precision/recall/F1, ROC-AUC).

### Öne Çıkan Sonuçlar

- Genel churn oranı: **%26,5**
- Model: ROC-AUC **0,972**, doğruluk **%93**, churn sınıfı precision **0,90** / recall **0,83**
- En güçlü churn sürükleyicileri (tümü p < 0.05): ders katılım sıklığındaki düşüş, grup derslerine katılmama, kısa sözleşme süresi, düşük üyelik süresi ("lifetime"), genç yaş grubu

### Nasıl Çalıştırılır

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn jupyter
jupyter notebook notebooks/01_quality_control.ipynb
```

Notebook'ları sırayla (01 → 05) çalıştırın; her biri bir önceki adımın ürettiği CSV'yi okur ve bir sonraki adımın kullanacağı CSV'yi yazar.
