# CSE 6250 - Distilling Knowledge for Epidemic Prognosis  
## Reproducing & Expanding on the DistCare Model  

This project builds on the work from **"Distilling Knowledge from Publicly Available Online EMR Data to Emerging Epidemic for Prognosis"**, a paper that explores how **electronic medical records (EMR) can be used for epidemic prognosis**.  

The original authors introduced **DistCare**, a model designed to transfer knowledge from **publicly available EMR data to emerging epidemics** where patient data is limited. Our goal was to **reproduce the results from the paper, evaluate its robustness, and test our own models based on similar ideas**.

This is the original work that we built upon:  
**Paper:** ["Distilling Knowledge from Publicly Available Online EMR Data to Emerging Epidemic for Prognosis"](https://dl.acm.org/doi/10.1145/3442381.3449935)  
**Original GitHub Repository:** [DistCare](https://github.com/ArthurLeoM/DistCare)  

---

## **Data Sources**
This project uses two publicly available EMR datasets:  

- **PhysioNet Challenge 2019** – A dataset for early sepsis prediction based on ICU patient records.  
  [Download Here](http://physionet.org/content/challenge-2019/1.0.0/)  

- **Tongji Hospital COVID-19 Dataset** – Contains COVID-19 patient records from Tongji Hospital, including vitals, lab results, and outcomes.  
  [Download Here](https://www.nature.com/articles/s42256-020-0180-7)  

---

## **DistCare Model Overview**
The **DistCare** framework is based on **knowledge distillation**, where a **teacher model** trained on a large dataset transfers knowledge to a **student model** trained on a smaller target dataset.  

### **How It Works**
1. **Teacher Model** (GRU-based)  
   - Trained on **PhysioNet data** (large ICU dataset).  
   - Learns general patient risk patterns.  
   - Uses **self-attention layers** for feature selection.  

2. **Student Model**  
   - Learns from the teacher using **knowledge distillation**.  
   - Fine-tuned on **Tongji Hospital COVID-19 data** (smaller dataset).  

3. **Target Model**  
   - Uses the student model’s pre-trained weights.  
   - Predicts **Length of Stay (LOS)** for COVID-19 patients.  

The model optimizes a combination of **Mean Squared Error (MSE) and KL Divergence loss** to balance real labels and teacher predictions.

---

## **Our Work: Reproducing & Extending DistCare**
We took the original **DistCare model**, reproduced its results, and conducted additional experiments, including:  

- **Reproducing the DistCare model's performance on the Tongji dataset**  
- **Developing a custom GRU transfer-learning model** using similar teacher-student distillation  
- **Testing an MLP-based alternative model**  
- **Comparing model performance using Mean Squared Error (MSE) & Mean Absolute Error (MAE)**  

---

## **Results**
| Model | MSE (Lower is Better) | MAE |
|--------|----------------|----------------|
| **Reproduced DistCare** | 305.86 | 16.44 |
| **Original DistCare (Paper Results)** | 198.93 | 9.75 |
| **GRU Transfer Model** | 218.86 | 6.67 |
| **MLP Model** | **152.24** | **6.44** |

**Note:** Our results for the DistCare model were worse than what was reported in the paper. This could be because we **did not have access to the exact preprocessing steps used in the original work**. Additionally, since the **Tongji dataset is relatively small**, simpler models like **MLP** may perform just as well (or even better) than complex architectures.  

---

## **How to Run This Project**
### **1. Reproduce the DistCare Model**
Open **`main_distcare_reproduce.ipynb`** and run all cells.

### **2. Test the GRU Transfer Model**
Open **`gru_transfer_distcare.ipynb`** and run all cells.

### **3. Test the MLP Model**
Open **`mlp_distcare.ipynb`** and run all cells.

---

The report talks about **understanding how knowledge distillation can help in medical AI, especially for emerging epidemics**. Please take a look for a more detailed analysis.
