# BIG_DATA
- df.na.drop(how="any", thresh = 1).show() dùng để xóa các dòng bị null nhưng có 1 dòng có dữ liệu. tường tự như 2 thì xóa các dòng nhưng để lại các dòng có 2 cột dữ liệu còn trong dòng
- df.na.drop(how="any", subset = ["ten cot"]).show()   xóa các dòng mà trong ten_cot có null. các cột còn lại có null k sao
- df.na.fill("MISSING VALUE").show()   thay các phần tử null bằng MISSING VALUE
- df.na.fill("MISSING VALUE" ['ten_cot', 'ten_cot']).show()   thay các phần tử null ở các cột đã chọn bằng MISSING VALUE
- muốn tính 1 phép tả cột thì dùng agg({'ten_cot': pheptinh}) muốn phân từng loại thì dùng groupBy().pheptinh().
-------------------------------------------
- "Mean square error" (MSE) là một thuật ngữ trong thống kê và machine learning. Nó là một phép đo độ chính xác của một mô hình dự đoán hoặc ước lượng so với dữ liệu thực tế. MSE được tính bằng cách lấy trung bình của bình phương của sự chênh lệch giữa giá trị dự đoán và giá trị thực tế của từng điểm dữ liệu trong tập dữ liệu.
- 
--------------------------------------------
1. Độ chính xác (Accuracy): Độ chính xác là tỷ lệ giữa số lượng dự đoán đúng và tổng số mẫu trong tập dữ liệu.
Công thức: Accuracy = (TP + TN) / (TP + TN + FP + FN)
Trong đó:
- TP (True Positive): Số lượng dự đoán đúng là positive (dự đoán tích cực) và nhãn thực tế cũng là positive.
- TN (True Negative): Số lượng dự đoán đúng là negative (dự đoán tiêu cực) và nhãn thực tế cũng là negative.
- FP (False Positive): Số lượng dự đoán sai là positive (dự đoán tích cực) nhưng nhãn thực tế là negative.
- FN (False Negative): Số lượng dự đoán sai là negative (dự đoán tiêu cực) nhưng nhãn thực tế là positive.
2. Độ chính xác có trọng số (Weighted Precision):
- Độ chính xác có trọng số là trung bình có trọng số của độ chính xác cho từng lớp.
- Nó đo lường khả năng của mô hình trong việc dự đoán đúng các mẫu thuộc vào mỗi lớp.
- Trong trường hợp phân loại đa lớp, độ chính xác có trọng số sẽ đánh giá hiệu suất của mô hình trên tất cả các lớp, bằng cách trung bình hoặc tính toán trọng số dựa trên số lượng mẫu trong mỗi lớp.
3. Độ nhớ (Recall hoặc Sensitivity):
- Độ nhớ là tỷ lệ giữa số lượng dự đoán đúng positive và tổng số mẫu thực tế positive.
- Công thức: Recall = TP / (TP + FN)
- Nó đo lường khả năng của mô hình trong việc tìm ra tất cả các mẫu thuộc vào một lớp cụ thể.
4. Điểm F1 (F1 Score):
- Điểm F1 là một số tổ hợp của độ chính xác và độ nhớ.
- Nó là sự trung bình điều hòa của độ chính xác và độ nhớ.
- Điểm F1 càng cao, mô hình càng tốt. Điểm F1 sử dụng khi bạn muốn cân nhắc cả precision và recall.
5. Diện tích dưới đường cong ROC (Area Under the ROC Curve - AUC-ROC):
- AUC-ROC là diện tích dưới đường cong ROC, một biểu đồ thể hiện tỷ lệ True Positive Rate (TPR) so với False Positive Rate (FPR) cho các ngưỡng dự đoán khác nhau.
- Nó đo lường khả năng của mô hình phân loại đúng giữa các lớp dương và âm.
-------------------------------------------------
# Clean Data
I. Có
  1. Hình thức:
    a. Sai định dạng: df.withColumn('column', df['column'].cast(...)
     - Thừa
       + Cột
          * Chọn cột: df.select()
          * Vứt cột: df.drop()
        + Dòng
          * Lọc dữ liệu: df.filter()
          * Bỏ lặp: df.dropDuplicates(['cot'])
    b. Nội dung
      - Sai:
        + Sửa: df.withColumn('age', when(df['age'] == 140, 40).otherwise(df['age']))
        + Vứt: df[df['age']!=140]
      - Ngoại lai
        + Phát hiện:
          * vẽ
          * quantile: approxQuantile()
          * standard deviation: stddev_samp()
        + Xử lý
          * Vứt: không được bằng / không nằm trong khoảng ngoại lai -> lọc dữ liệu -> .filter(...)
          * Tách bảng:
            +, df1: filter trong khoảng bt
            +, df2: filter ngoài khoảng bt
II. Không có -> NA
  1. Kiểm tra NA: df.filter(df['col'].isNull())
  2. Xử lý NA:
     a. 1) Vứt: df.na.drop()
     b. 2) Điền: df.na.fill(value)
     c. 3) Tách: -> lọc
![320717445-0928a391-8046-475b-8fb1-7a3e74e88cae](https://github.com/tung071017/BIG_DATA/assets/138083316/d2b9e509-bfde-4911-b136-afd532fba1c5)

https://github.com/awinml/amex-default-classification/blob/main/amex-eda.ipynb
