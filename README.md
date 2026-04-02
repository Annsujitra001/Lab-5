# Lab-5
ส่วนที่ 1: Problem Statement
  
    Specific — ระบุพื้นที่และประชากร/ระบบนิเวศที่ได้รับผลกระทบได้ชัดเจน
        พื้นที่จังหวัดกรุงเทพมหานคร นนทบุรี ปทุมธานี
    Measurable — มีตัวชี้วัดที่สามารถวัดได้ด้วย Remote Sensing หรือ GIS 
         1.Land Surface Temperature (LST): MODIS 
         2.NDVI (ความหนาแน่นพืช): Sentinel-2 
         3.Soil Moisture / Rainfall (CHIRPS): NASA_USDA_HSL (SMAP10KM) 
         4.Urban built-up: Landsat classification 
    Relevant — เชื่อมโยงกับปัญหาจริงในบริบทไทยหรือภูมิภาค 
         1.ไทยเป็นเขตร้อนชื้น 
         2.พื้นที่เมือง มี heat island และน้ำขัง เชื้อราเติมโตง่าย  
         3.เชื้อราในดิน/พืช 
         4.เกี่ยวกับโรคทางเดินหายใจ 
    Researchable ใน 4 สัปดาห์ — ไม่ใหญ่เกินไปจนทำไม่ได้จริง 
         1.MODIS (LST) 
         2.Sentinel-2 (NDVI) 
         3.CHIRPS (rainfall) 
ส่วนที่ 2 Researcher Question 

    คำถาม: พื้นที่ใดในกรุงเทพมหานคร นนทบุรี และปทุมธานีมีความเหมาะสมต่อการเจริญของเชื้อราสูงที่สุด 
    Data set  
         1.Sentinel 2 ใช้ดู NDVI Band : B8 (NIR), B4 (RED) 
         2.SMAP Soil moisture variable : soil moisture  
         3.ERA5 Temperature variable: temperature_2m 
         4.Landsat Urban Classification variable : urban class 
    วิธีการวิเคราะห์ 
         1.คำนวณ NDVI จาก Sentinel-2 
         2.Normalize ทุกตัวแปรให้อยู่ในช่วง 0–1 
         3.รวมตัวแปรด้วย Weighted Overlay 
              > Soil moisture (0.4) 
              > NDVI (0.3) 
              > Temperature (0.2) 
              > Urban (0.1) 
    สร้าง Fungal Suitability Index 
         > ความละเอียด ใช้ resolution ประมาณ 500 m – 1 km 
    
    คำถาม: NDVI มีความสัมพันธ์กับการกระจายของความเสี่ยงเชื้อราอย่างไรในเชิงพื้นที่? 
    Data set  
         1.Sentinel-2 NDVI Band: B8, B4 
         2.Fungal Risk Map (จาก RQ1) 
    วิธีการวิเคราะห์ 
         1.แบ่งค่า NDVI เป็นระดับ (ต่ำ / กลาง / สูง) 
         2.Overlay กับ Fungal Risk Map 
         3.ใช้ Correlation analysis และ Zonal statistics 
         4.วิเคราะห์
              > NDVI สูง → risk สูงหรือไม่ 
    ความละเอียด 
         > ใช้ resolution 10–30 m (Sentinel-2)หรือ upscale เป็น ~500 m เพื่อให้เท่ากับตัวแปรอื่น พื้นที่ใดในกรุงเทพมหานคร นนทบุรี และปทุมธานีมีความเหมาะสมต่อการเจริญของเชื้อราสูงที่สุด 
    Data set  
         1.Sentinel 2 ใช้ดู NDVI Band : B8 (NIR), B4 (RED) 
         2.SMAP Soil moisture variable : soil moisture  
         3.ERA5 Temperature variable: temperature_2m 
         4.Landsat Urban Classification variable : urban class   
    วิธีการวิเคราะห์ 
         1.คำนวณ NDVI จาก Sentinel-2 
         2.Normalize ทุกตัวแปรให้อยู่ในช่วง 0–1 
         3.รวมตัวแปรด้วย Weighted Overlay 
              > Soil moisture (0.4) 
              > NDVI (0.3) 
              > Temperature (0.2) 
              > Urban (0.1) 
    สร้าง Fungal Suitability Index 
         > ความละเอียด ใช้ resolution ประมาณ 500 m – 1 km 
ส่วนที่ 3 Data Inventory
          
    > Sentinel-2 MSI COPERNICUS/S2 ปัญหาเมฆปกคลุม (Cloud cover) ในพื้นที่กรุงเทพฯ นนทบุรี และปทุมธานี 
    > SMAP (NASA-USDA) NASA_USDA_HSL/SMAP10KM ความละเอียดเชิงพื้นที่ต่ำ (10km) อาจต้องมีการจัดรูปแบบข้อมูลให้เข้ากับตัวแปรอื่น 
    > ERA5-Land NASA_USDA_HSL/SMAP10KM ข้อมูลเป็นค่าเฉลี่ยรายชั่วโมง/เดือน อาจไม่สะท้อน Micro-climate ในบางจุด 
    > Landsat 8/9 LANDSAT/LC08/C02/T1_L2 รอบการบันทึกภาพ (Temporal resolution) ห่างกันประมาณ 16 วัน 

ส่วนที่ 4: Methodology Flow

     ขั้นตอนการทำงาน 
          1.Data Collection 
              > โหลดข้อมูลจาก Google Earth Engine 
              > ตัดเฉพาะพื้นที่กรุงเทพมหานคร นนทบุรี ปทุมธานี 
          2.Preprocessing 
              > กำจัดเมฆ (Cloud masking) 
              > คำนวณ NDVI 
              > ปรับค่าข้อมูลให้อยู่ในช่วง 0–1 (Normalization)
          3.Feature Preparation 
              รวมตัวแปร: > NDVI 
                        > LST (Land Surface Temperature) 
                        > Urban density 
                        > Soil moisture 
          4.การวิเคราะห์ 
              วิธีที่ 1: Weighted Overlay กำหนดน้ำหนัก เช่น 
                      > Urban = 0.4 
                      > Temperature = 0.3 
                      > NDVI = 0.2 
                      > Soil moisture = 0.1 
                      > สร้าง Risk Index 
              วิธีที่ 2: Machine Learning 
                      > ใช้ Random Forest 
                      > แบ่ง train/test 
                      > ทำนายพื้นที่เสี่ยง 
          5.Validation 
              > Accuracy จาก train/test 
              > เปรียบเทียบกับพื้นที่เมืองหนาแน่น 
          6.Output 
              > แผนที่ความเสี่ยง (สูง / กลาง / ต่ำ) 
              > Visualization บน GEE 










































         
