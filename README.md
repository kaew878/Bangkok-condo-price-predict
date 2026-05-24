Note :  

1. This project is for personal study about Machine Learning , EDA (Exploratory Data Analysis) and Feature Engineering

2. This Data set is since 2019. So This is model for evaluate bangkok house/condominium price in 2019

data set : https://www.kaggle.com/datasets/thedevastator/predicting-bangkok-condominium-prices-using-web

Google Collab Project : https://colab.research.google.com/drive/1u9M2veqtW7yhNQOTP2bVrCQGqSM9lz2q

# 📌 สรุปภาพรวมโปรเจค: การพยากรณ์ราคาคอนโดในกรุงเทพฯ ด้วย XGBoost

โปรเจคนี้มีวัตถุประสงค์เพื่อสร้างโมเดล Machine Learning ที่มีความแม่นยำสูงในการประเมินราคาคอนโดมิเนียม (บาท/ตร.ม.) โดยครอบคลุมขั้นตอนสำคัญดังนี้:

### 1. การเตรียมข้อมูลและจัดการค่าผิดปกติ (Data Cleaning & EDA)
*   **Target Transformation:** พบว่าราคาคอนโดมีความเบ้ขวา (Skewed) จึงใช้ **Yeo-Johnson Transformation** เพื่อปรับให้ข้อมูลมีการกระจายตัวแบบปกติ ช่วยให้โมเดลเรียนรู้ได้ดีขึ้นทั้งในกลุ่มราคาถูกและราคาแพง
*   **Geographic Analysis:** วิเคราะห์ความสัมพันธ์เชิงพื้นที่ พบการกระจุกตัวของราคาสูงในย่าน CBD (Siam, Asoke, Silom)

### 2. วิศวกรรมฟีเจอร์ (Feature Engineering) - หัวใจของความแม่นยำ
*   **Distance to CBD:** คำนวณระยะทางจากพิกัด (Lat/Long) ไปยังจุดยุทธศาสตร์ 3 แห่ง เพื่อแทนค่าความพรีเมียมของทำเล
*   **Weighted Amenity Score:** แทนที่จะนับจำนวนสิ่งอำนวยความสะดวกตรงๆ เราใช้ค่า **Correlation** มาเป็นน้ำหนักถ่วง เพื่อให้ความสำคัญกับฟีเจอร์ที่ส่งผลต่อราคาจริงๆ (เช่น สระว่ายน้ำ และ ยิม)
*   **Target Encoding:** แปลงชื่อเขต (District) เป็นค่าตัวเลขตามราคาเฉลี่ยของเขตนั้นๆ เพื่อให้โมเดลเข้าใจศักยภาพของแต่ละทำเล
*   **Feature Selection:** คัดกรองฟีเจอร์ที่มีความแปรปรวนต่ำ (Low Variance) และความสัมพันธ์ต่ำ (Low Correlation) ออก เพื่อลด Noise

### 3. ประสิทธิภาพของโมเดล (XGBoost Results)
เราเลือกใช้ **XGBoost Regressor** ซึ่งเป็นโมเดลกลุ่ม Tree-based Ensemble ที่ทรงพลัง:
*   **R-Squared (R²) ≈ 0.76** (บน Transformed Scale): บ่งบอกว่าโมเดลสามารถอธิบายความผันผวนของข้อมูลได้ดีมากทางสถิติ
*   **R-Squared (R²) ≈ 0.72** (บนราคาจริง): ความแม่นยำเมื่อนำไปใช้งานจริง
*   **MAE ≈ 19,833 บาท/ตร.ม.:** ค่าความคลาดเคลื่อนเฉลี่ยอยู่ในเกณฑ์ที่ยอมรับได้สำหรับตลาดอสังหาริมทรัพย์ที่มีความหลากหลายสูง

### 4. เครื่องมือใช้งานจริง (Interactive Tool)
*   สร้าง **Interactive Widget** ที่ช่วยให้ผู้ใช้สามารถระบุเขตและรายละเอียดของคอนโด เพื่อรับราคาประเมินได้ทันทีภายใน Notebook

--- 
*หมายเหตุ: โมเดลมีความแม่นยำสูงมากในกลุ่มราคาไม่เกิน 200,000 บาท/ตร.ม. สำหรับกลุ่ม Super Luxury จะมีความผันผวนสูงกว่าเนื่องจากปัจจัยเฉพาะตัวของโครงการนั่นเองครับ*
