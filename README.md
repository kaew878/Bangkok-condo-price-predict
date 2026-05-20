# Bangkok-condo-price-predict
Machine learning project to predict condo prices in Bangkok
# 🏢 Bangkok Condominium Price Prediction

ชุดข้อมูลและโปรเจคแมชชีนเลิร์นนิงเพื่อทำนายราคาคอนโดมิเนียมในกรุงเทพมหานคร

## 📊 Project Overview

โปรเจคนี้ใช้เทคนิคแมชชีนเลิร์นนิงเพื่อสร้างแบบจำลองการทำนายราคาต่อตารางเมตร (Price per Square Meter) ของคอนโดในกรุงเทพ โดยพิจารณาจากตำแหน่ง สิ่งอำนวยความสะดวก ระยะห่างจากสถานที่สำคัญ และลักษณะเฉพาะของทรัพย์สิน

## 📋 Features Description

### 🗺️ ข้อมูลทำเนียบทั่วไป (General Information)
| Feature | ประเภท | คำอธิบาย |
|---------|--------|---------|
| **district** | String | เขตของกรุงเทพที่คอนโดตั้งอยู่ |
| **latitude** | Float | พิกัด latitude ของคอนโด |
| **longitude** | Float | พิกัด longitude ของคอนโด |
| **year_built** | Integer | ปีที่สร้างคอนโด |
| **bld_age** | Integer | อายุของคอนโด (ปี) |

### 🏗️ ลักษณะทางกายภาพของโครงการ (Project Structure)
| Feature | ประเภท | คำอธิบาย |
|---------|--------|---------|
| **proj_area** | Float | พื้นที่ของโครงการคอนโด (ตารางเมตร) |
| **nbr_buildings** | Integer | จำนวนตึกในคอนโด |
| **nbr_floors** | Integer | จำนวนชั้นของตึก |
| **units** | Integer | จำนวนหน่วยอพาร์ตเมนต์ในคอนโด |

### 🏥 ระยะห่างจากสถานที่สำคัญ (Proximity to Important Places)

#### โรงพยาบาล (Hospital)
- **hospital** - ระยะห่างไปโรงพยาบาลที่ใกล้ที่สุด (กม.)

#### ร้านค้า (Shops)
- **dist_shop_1** to **dist_shop_5** - ระยะห่างไปร้านค้า 5 แห่งที่ใกล้ที่สุด (กม.)

#### โรงเรียน (Schools)
- **dist_school_1** to **dist_school_5** - ระยะห่างไปโรงเรียน 5 แห่งที่ใกล้ที่สุด (กม.)

#### ร้านอาหาร (Food/Restaurants)
- **dist_food_1** to **dist_food_5** - ระยะห่างไปร้านอาหาร 5 แห่งที่ใกล้ที่สุด (กม.)

### 🚌 การขนส่ง (Transportation)
| Feature | ประเภท | คำอธิบาย |
|---------|--------|---------|
| **tran_type1** | String | ประเภทการขนส่งที่ 1 |
| **tran_type2** | String | ประเภทการขนส่งที่ 2 |
| **tran_type3** | String | ประเภทการขนส่งที่ 3 |
| **tran_type4** | String | ประเภทการขนส่งที่ 4 |
| **tran_type5** | String | ประเภทการขนส่งที่ 5 |
| **dist_tran_1** | Float | ระยะห่างไปสถานีขนส่งที่ 1 (กม.) |
| **dist_tran_2** | Float | ระยะห่างไปสถานีขนส่งที่ 2 (กม.) |
| **dist_tran_3** | Float | ระยะห่างไปสถานีขนส่งที่ 3 (กม.) |
| **dist_tran_4** | Float | ระยะห่างไปสถานีขนส่งที่ 4 (กม.) |
| **dist_tran_5** | Float | ระยะห่างไปสถานีขนส่งที่ 5 (กม.) |

### 🛠️ สิ่งอำนวยความสะดวก (Amenities)
| Feature | ประเภท | คำอธิบาย |
|---------|--------|---------|
| **Elevator** | Integer | จำนวนลิฟต์ในคอนโด |
| **Parking** | Integer | จำนวนที่จอดรถ |
| **Security** | Integer | จำนวนยามรักษาความปลอดภัย |
| **CCTV** | Integer | จำนวนกล้องวงจรปิด |
| **Pool** | Integer | จำนวนสระว่ายน้ำ |
| **Sauna** | Integer | จำนวนห้องซาวน่า |
| **Gym** | Integer | จำนวนสถานที่ออกกำลังกาย |
| **Garden** | Integer | จำนวนสวน/พื้นที่สีเขียว |
| **Playground** | Integer | จำนวนสนามเด็กเล่น |
| **Shop** | Integer | จำนวนร้านค้าในคอนโด |
| **Restaurant** | Integer | จำนวนร้านอาหารในคอนโด |
| **WiFi** | Integer | จำนวนจุด WiFi ฟรี |

### 🎯 Target Variable
| Feature | ประเภท | คำอธิบาย |
|---------|--------|---------|
| **price_sqm** | Float | ราคาต่อตารางเมตร (บาท/ตร.ม.) - **Target Variable** |
