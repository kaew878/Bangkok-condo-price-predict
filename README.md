Note :  

1. This project is focus on study about Machine Learning , EDA (Exploratory Data Analysis) and Feature Engineering  

2. This Data set is since 2019. So This is model for evaluate bangkok house/condominium price in 2019
  
3. The project developer utilized AI to assist in generating nearly all of the code. The developer’s primary role was to design the overall approach, define the workflow and underlying principles for each stage of the project, and review the generated code to ensure that it aligned with the intended objectives, methodologies, and project requirements.

4. Most of all describtion is Thai , so if you do not understand Thai this is 2026 and we have AI :)


data set : https://www.kaggle.com/datasets/thedevastator/predicting-bangkok-condominium-prices-using-web

Google Collab Project : https://colab.research.google.com/drive/1u9M2veqtW7yhNQOTP2bVrCQGqSM9lz2q

XGBoost เหมาะกับการประเมินราคาอสังหาในกรุงเทพ เพราะ:

1. ราคาคอนโด/บ้านมี “ความสัมพันธ์ซับซ้อน” เช่น BTS ใกล้แค่ไหน, เขตอะไร, อายุอาคาร, ส่วนกลาง, วิว, ขนาดห้อง — ปัจจัยพวกนี้ไม่ได้เพิ่มราคาตรงๆ แบบเส้นตรง ซึ่ง XGBoost จับ pattern ซับซ้อนได้ดี

2. จัดการข้อมูลจริงได้เก่ง ข้อมูลอสังหามักมี missing values, outliers, และ feature หลายประเภท XGBoost รับมือได้ค่อนข้างดีโดยไม่ต้อง preprocess หนักเท่า model บางประเภท

3. เหมาะกับ tabular data ข้อมูลอสังหาส่วนใหญ่เป็นตาราง (ราคา, พื้นที่, ชั้น, เขต ฯลฯ) ซึ่งเป็นจุดแข็งของ XGBoost มาก

4. เรียนรู้ interaction ระหว่าง feature ได้อัตโนมัติ เช่น “คอนโดใกล้ BTS + อยู่ CBD + ห้องใหญ่” อาจดันราคาขึ้นแรงกว่าดูแต่ feature เดี่ยวๆ

5. ให้ accuracy สูงในงาน regression งานทำนายราคาเป็น regression problem ซึ่ง XGBoost มักให้ผลแม่นยำมากกับข้อมูล structured/tabular

สรุป:
XGBoost เหมาะ เพราะ “ราคาบ้านในกรุงเทพมีหลายปัจจัยที่สัมพันธ์กันแบบซับซ้อน” และ model นี้เก่งมากกับข้อมูลตารางที่ nonlinear และ noisy แบบอสังหาไทย

# 📌 สรุปภาพรวมโปรเจค: การพยากรณ์ราคาบ้าน/คอนโดในกรุงเทพฯ ด้วย XGBoost

โปรเจคนี้มีวัตถุประสงค์เพื่อสร้างโมเดล Machine Learning ที่มีความแม่นยำสูงในการประเมินราคาคอนโดมิเนียม (บาท/ตร.ม.) โดยครอบคลุมขั้นตอนสำคัญดังนี้:

### 1. การเตรียมข้อมูลและจัดการค่าผิดปกติ (Data Cleaning & EDA)
*   **Target Transformation:** พบว่าราคาคอนโดมีความเบ้ขวา (Skewed) จึงใช้ **Yeo-Johnson Transformation** เพื่อปรับให้ข้อมูลมีการกระจายตัวแบบปกติ ช่วยให้โมเดลเรียนรู้ได้ดีขึ้นทั้งในกลุ่มราคาถูกและราคาแพง
*   **Geographic Analysis:** วิเคราะห์ความสัมพันธ์เชิงพื้นที่ พบการกระจุกตัวของราคาสูงในย่าน CBD (Siam, Asoke, Silom)

### 2. Feature Engineering ซึ่งหัวใจของความแม่นยำ
*   **Distance to CBD:** คำนวณระยะทางจากพิกัด (Lat/Long) ไปยังจุดยุทธศาสตร์ 3 แห่ง เพื่อแทนค่าความพรีเมียมของทำเล
*   **Weighted Amenity Score:** แทนที่จะนับจำนวนสิ่งอำนวยความสะดวกตรงๆ เราใช้ค่า **Correlation** มาเป็นน้ำหนักถ่วง เพื่อให้ความสำคัญกับฟีเจอร์ที่ส่งผลต่อราคาจริงๆ (เช่น สระว่ายน้ำ และ ยิม)
*   **Target Encoding:** แปลงชื่อเขต (District) เป็นค่าตัวเลขตามราคาเฉลี่ยของเขตนั้นๆ เพื่อให้โมเดลเข้าใจศักยภาพของแต่ละทำเล
*   **Feature Selection:** คัดกรองฟีเจอร์ที่มีความแปรปรวนต่ำ (Low Variance) และความสัมพันธ์ต่ำ (Low Correlation) ออก เพื่อลด Noise

### 3. ประสิทธิภาพของโมเดล (XGBoost Results)
เราเลือกใช้ **XGBoost Regressor** ซึ่งเป็นโมเดลกลุ่ม Tree-based Ensemble ที่ทรงพลัง:
*   **R-Squared (R²) ≈ 0.76** (บน Transformed Scale): บ่งบอกว่าโมเดลสามารถอธิบายความผันผวนของข้อมูลได้ดีมากทางสถิติ
*   **R-Squared (R²) ≈ 0.72** (บนราคาจริง): ความแม่นยำเมื่อนำไปใช้งานจริง
*   **MAE ≈ 19,833 บาท/ตร.ม.:** ค่าความคลาดเคลื่อนเฉลี่ยอยู่ในเกณฑ์ที่ยอมรับได้สำหรับตลาดอสังหาริมทรัพย์ที่มีความหลากหลายสูง
--- 
*หมายเหตุ: โมเดลมีความแม่นยำสูงมากในกลุ่มราคาไม่เกิน 200,000 บาท/ตร.ม. สำหรับกลุ่ม Super Luxury จะมีความผันผวนสูงกว่าเนื่องจากปัจจัยเฉพาะตัวของโครงการนั่นเองครับ*
