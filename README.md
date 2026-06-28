## 1. Project

## A Novel Sample Clustering Method for Diabetes Data Classification

## 2. Giới thiệu (Overview / Description)

Dự án này tập trung xây dựng một pipeline Machine Learning nhằm phân loại bệnh tiểu đường dựa trên bộ dữ liệu Pima Indians Diabetes Dataset.

Mục tiêu chính của project là nghiên cứu ảnh hưởng của các phương pháp tiền xử lý dữ liệu, phát hiện mẫu nhiễu (outlier), phân cụm dữ liệu và các mô hình học máy trong bài toán dự đoán nguy cơ mắc bệnh tiểu đường.

Quy trình được xây dựng bao gồm:

- Phân tích khám phá dữ liệu (Exploratory Data Analysis - EDA) để đánh giá đặc điểm phân phối, tương quan giữa các biến và sự khác biệt giữa nhóm có/không có tiểu đường.
- Xử lý dữ liệu không hợp lệ bằng cách thay thế các giá trị 0 bất thường trong các thuộc tính sinh học bằng phương pháp imputation phù hợp.
- Chuẩn hóa dữ liệu nhằm đưa các biến về cùng một không gian giá trị.
- Áp dụng phương pháp clustering dựa trên KMeans để xác định các mẫu dữ liệu bất thường và tách dữ liệu nhiễu.
- Đánh giá mức độ ảnh hưởng của các đặc trưng thông qua Cohen's d nhằm đo lường sự khác biệt giữa hai nhóm Outcome.
- Huấn luyện và đánh giá các mô hình Machine Learning bao gồm:
  - SGDClassifier với GridSearchCV tối ưu tham số.
  - K-Nearest Neighbors kết hợp Robust Mahalanobis Distance.
  - Logistic Regression với các phương pháp regularization như L1 (Lasso), L2 (Ridge), ElasticNet và Adaptive Lasso.

Project hướng tới xây dựng một hệ thống hỗ trợ phân loại bệnh tiểu đường có khả năng xử lý dữ liệu nhiễu, cải thiện độ ổn định của mô hình và tăng khả năng giải thích thông qua phân tích trọng số đặc trưng.

## 3. Result

Kết quả thực nghiệm sau quá trình tiền xử lý dữ liệu, lọc mẫu dựa trên Cohen's d và huấn luyện mô hình được trình bày dưới đây.

### Pipeline Workflow

<p align="center">
  <img src="Output/Pipeline.png" width="50%">
</p>

### Cohen's d Filtering Result

<p align="center">
  <img src="Output/Filtering.png" width="50%">
</p>

### Model Evaluation Result

<p align="center">
  <img src="Output/ROC.png" width="50%">
</p>


## 4. Dataset

Dự án sử dụng **Pima Indians Diabetes Dataset**, một bộ dữ liệu chuẩn thường được sử dụng trong các nghiên cứu phân loại bệnh tiểu đường.

Bộ dữ liệu gồm **768 mẫu**, bao gồm **8 đặc trưng y tế** và một biến mục tiêu nhị phân (`Outcome`):

- `1`: Có tiểu đường
- `0`: Không tiểu đường

### Các thuộc tính

| Feature | Mô tả |
|---|---|
| Pregnancies | Số lần mang thai |
| Glucose | Nồng độ glucose trong huyết tương |
| BloodPressure | Huyết áp tâm trương |
| SkinThickness | Độ dày nếp gấp da cơ tam đầu |
| Insulin | Nồng độ insulin trong huyết thanh |
| BMI | Chỉ số khối cơ thể |
| DiabetesPedigreeFunction | Yếu tố nguy cơ di truyền liên quan đến tiểu đường |
| Age | Tuổi của bệnh nhân |

### Ghi chú

- Tất cả các đặc trưng đều là dữ liệu dạng số.
- Một số thuộc tính y tế chứa giá trị 0 không hợp lý về mặt sinh học (ví dụ: BMI, glucose, huyết áp), được xem như dữ liệu thiếu và xử lý trong bước tiền xử lý.
- Dataset được sử dụng cho quá trình phân tích dữ liệu, đánh giá đặc trưng, lọc mẫu nhiễu và xây dựng mô hình phân loại bệnh tiểu đường.

## 5. Công nghệ sử dụng (Tech Stack)

### Programming Language
- Python

### Data Processing & Analysis
- Pandas
- NumPy

### Data Visualization
- Matplotlib
- Seaborn

### Machine Learning
- Scikit-learn
  - Logistic Regression
  - SGDClassifier
  - KNN
  - Random Forest
  - KMeans Clustering
  - GridSearchCV

### Data Preprocessing
- Scikit-learn
  - StandardScaler
  - MinMaxScaler
  - RobustScaler
  - SimpleImputer

### Imbalanced Data Handling
- Imbalanced-learn
  - SMOTE

### Statistical Analysis
- Cohen's d Effect Size
- Mahalanobis Distance

### Environment
- Google Colab
- Jupyter Notebook



## 6. Installation

git bash:
- git clone (https://github.com/nguyenhoanghuy34/diabetes-data-filtering-cohend.git)
- cd your-project
- pip install -r requirements.txt


## 7. Workflow

![Pipeline](Output/Pipeline.png)

Quy trình của mô hình gồm các bước chính:

1. **Data Preprocessing**
   - Kiểm tra dữ liệu thiếu và giá trị không hợp lệ.
   - Thay thế các giá trị 0 không có ý nghĩa sinh học bằng giá trị median.
   - Chuẩn hóa dữ liệu trước khi huấn luyện.

2. **Intentional Clustering (Noise Filtering)**
   - Phân nhóm dữ liệu theo nhãn Outcome.
   - Với mỗi biến, K-Means được sử dụng để xác định xu hướng trung tâm của dữ liệu.
   - Các mẫu có độ lệch lớn so với trung tâm được đánh dấu là dữ liệu nhiễu (outlier).
   - Tập dữ liệu được chia thành:
     - **Common samples**: dữ liệu sạch, ít nhiễu.
     - **Rare samples**: dữ liệu bất thường, chứa thông tin đặc biệt.

3. **Cohen’s D Feature Evaluation**
   - Đánh giá mức độ khác biệt giữa hai lớp bằng Cohen’s D.
   - Các biến có Cohen’s D ≥ 0.5 được xem là có khả năng phân biệt tốt giữa hai nhóm.

4. **Model Selection**
   - Với **common samples**:
     - Sử dụng mô hình tuyến tính nhẹ như SGDClassifier để khai thác đặc điểm rõ ràng của dữ liệu.
   - Với **rare samples**:
     - Sử dụng mô hình phi tuyến như KNN kết hợp Robust Mahalanobis Distance để xử lý dữ liệu nhiễu.

5. **Evaluation**
   - Đánh giá mô hình bằng:
     - Accuracy
     - F1-score
     - Confusion Matrix
     - ROC-AUC Curve

## 8. Citation

[1] Okwor, I. A., Hitch, G., Hakkim, S., Akbar, S., Sookhoo, D., and Kainesie, J.  
"Digital technologies impact on healthcare delivery: a systematic review of artificial intelligence (AI) and machine-learning (ML) adoption, challenges, and opportunities."  
AI, vol. 5, no. 4, pp. 1918–1941, 2024.

[2] Bhuyan, S. S. et al.  
"Generative artificial intelligence use in healthcare: opportunities for clinical excellence and administrative efficiency."  
Journal of Medical Systems, vol. 49, no. 1, p. 10, 2025.

[3] Mizna, S., Arora, S., Saluja, P., Das, G., and Alanesi, W. A.  
"An analytic research and review of the literature on practice of artificial intelligence in healthcare."  
European Journal of Medical Research, vol. 30, no. 1, p. 382, 2025.

[4] Migdalis, I. N.  
"Chronic Complications of Diabetes: Prevalence, Prevention, and Management."  
MDPI, vol. 13, p. 7001, 2024.

[5] Guan, H. et al.  
"Advances in secondary prevention mechanisms of macrovascular complications in type 2 diabetes mellitus patients: a comprehensive review."  
European Journal of Medical Research, vol. 29, no. 1, p. 152, 2024.

[6] International Diabetes Federation.  
"IDF Diabetes Atlas, 11th Edition."  
International Diabetes Federation, Brussels, Belgium, 2025.

[7] Wang, S. C., Nickel, G., Venkatesh, K. P., Raza, M. M., and Kvedar, J. C.  
"AI-based diabetes care: risk prediction models and implementation concerns."  
NPJ Digital Medicine, vol. 7, no. 1, p. 36, 2024.

[8] Oei, S., Bakkes, T., Mischi, M., Bouwman, R., van Sloun, R., and Turco, S.  
"Artificial intelligence in clinical decision support and the prediction of adverse events."  
Frontiers in Digital Health, vol. 7, p. 1403047, 2025.

[9] Hu, H., Dong, W., Yu, J., Guan, S., and Zhu, X.  
"Utilizing Attention-Enhanced Deep Neural Networks for Large-Scale Preliminary Diabetes Screening in Population Health Data."  
Electronics, vol. 13, no. 21, p. 4177, 2024.

[10] Rolando, M., Raggio, V., Naya, H., Spangenberg, H., and Cagnina, L.  
"A labeled medical records corpus for the timely detection of rare diseases using machine learning approaches."  
Scientific Reports, vol. 15, no. 1, p. 6932, 2025.

[11] Feng, X., Cai, Y., and Xin, R.  
"Optimizing diabetes classification with a machine learning-based framework."  
BMC Bioinformatics, vol. 24, no. 1, p. 428, 2023.

[12] Zhang, Z.  
"Comparison of Machine Learning Models for Predicting Type 2 Diabetes Risk Using the Pima Indians Diabetes Dataset."  
Journal of Innovations in Medical Research, vol. 4, no. 1, pp. 65–71, 2025.

[13] Qi, X., Lu, Y., Shi, Y., Qi, H., and Ren, L.  
"A deep neural network prediction method for diabetes based on Kendall’s correlation coefficient and attention mechanism."  
PLOS ONE, vol. 19, no. 7, p. e0306090, 2024.

[14] Zhao, J., Gao, H., Yang, C., An, T., Kuang, Z., and Shi, L.  
"Attention-oriented CNN method for type 2 diabetes prediction."  
Applied Sciences, vol. 14, no. 10, p. 3989, 2024.

[15] García-Ordás, M. T. et al.  
"Diabetes detection using deep learning techniques with oversampling and feature augmentation."  
Computer Methods and Programs in Biomedicine, vol. 202, p. 105968, 2021.

[16] Shams, M. Y., Tarek, Z., and Elshewey, A. M.  
"A novel RFE-GRU model for diabetes classification using PIMA Indian dataset."  
Scientific Reports, vol. 15, no. 1, p. 982, 2025.

[17] Reza, M. S., Amin, R., Yasmin, R., Kulsum, W., and Ruhi, S.  
"Improving diabetes disease patients classification using stacking ensemble method with PIMA and local healthcare data."  
Heliyon, vol. 10, no. 2, 2024.

[18] Idris, N. F. et al.  
"Stacking with Recursive Feature Elimination-Isolation Forest for classification of diabetes mellitus."  
PLOS ONE, vol. 19, no. 5, p. e0302595, 2024.

[19] Aich, A., Murshed, M. M., Hewage, S., and Mayeaux, A.  
"CopulaSMOTE: A Copula-Based Oversampling Approach for Imbalanced Classification in Diabetes Prediction."  
arXiv preprint arXiv:2506.17326, 2025.

[20] Liu, C., Yang, H., Yang, J., and Wang, H.  
"Correlation analysis of diabetes based on Copula."  
Frontiers in Endocrinology, vol. 15, p. 1291895, 2024.

[21] Cohen, J.  
"Statistical Power Analysis for the Behavioral Sciences."  
Routledge, 2013.
