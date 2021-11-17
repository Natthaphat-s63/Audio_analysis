# Audio_analysis
สำหรับโปรแกรมนี้เป็นโปรแกรมสำหรับรวมไฟล์เสียงเข้าด้วยกันพร้อมทั้งนำไฟล์เสียงมาวิเคราะห์จากกราฟทั้งแบบ Time domain และ Frequency domain โดยใช้ FFT ในการแปลง และสามารถรวมเสียงได้มากกว่า 1 ไฟล์ และ ยังสามารถเล่นเสียงที่รวมแล้วได้เพื่อฟังผลลัพธ์การรวมเสียง หน้าตาของ GUI ของ Application ก็จะเป็นตามนี้

![image](https://user-images.githubusercontent.com/87507926/142205815-62e765e6-303b-451a-89d6-4578ec424b7a.png)



# ระบบไฟล์
สามารถ import ไฟล์เสียงได้หลายไฟล์และต่างนามสกุลพร้อมกันได้ เมื่อ import มาแล้วก็จะมาอยู่ใน List box จากนั้นถ้าจะเลือกไฟล์ไหนไปรวมก็ทำเหมือนเวลาเลือกหลายไฟล์ใน windows ได้เลย 

![image](https://user-images.githubusercontent.com/87507926/142205541-ca3d234e-9b17-4258-8d6f-d1b0f562bdce.png)
![image](https://user-images.githubusercontent.com/87507926/142205554-6f79dbd9-bf54-4919-b7c9-28d2edcb85f0.png)

![image](https://user-images.githubusercontent.com/87507926/142206024-cbc6c694-cc51-40ba-84e5-2630dc2a02ab.png)

# ระบบกราฟ
หลังจากทำการเลือกไฟล์ที่จะรวมได้แล้วให้ทำการกดปุ่ม Add เป็นการรวมสัญญาณจากนั้นไฟ LED ก็จะติด แสดงว่าสัญญาณพร้อม plot แล้วให้กดปุ่ม plot กราฟก็จะขึ้นทั้ง Time domain และ Frequency domain ขึ้นมา
ในส่วนของการคำนวณและการ plotting เรื่องของค่า Sample rate ต่างๆไฟล์ทั้งหมดจะถูก resample เป็น 48000 Hz ก่อนและถ้าไฟล์เป็นระบบ mono จะถูกนำไปทำเป็น stereo แล้วค่อยนำไป รวมกับเสียงอื่นๆ ดังนั้น ผลรวมสัญญาณจะได้ Sample rate ที่ 48000 Hz 

ในการ plot กราฟฝั่ง Time domain ก็จะยึดค่า Sample rate ไว้ที่ 48000 Hz แล้วคำนวณจาก Sample rate เพื่อให้ได้ Array แกน X ที่มีหน่วยเป็น second ก่อนนำไป plot ส่วนแกน Y ก็คือค่าที่ได้จากการใช้ function audioread ก็จะได้ Array สำหรับแกน Y บน Time domain ออกมา และเนื่องจากเป็นระบบ stereo ดังนั้นก็จะมีข้อความบอกว่าสีไหนเป็นของ Left กับ Right ในฝั่ง Frequency domain ก็จะนำค่า Sample rate มาคำนวณหา Array สำหรับแกน X ที่มีหน่วยเป็น Hz นั่นเอง ส่วนแกน Y ก็นำค่าแกน Y จาก Time domain ไปผ่าน FFT พร้อมมีการ normalize และ ทำเป็นค่า absolute เพื่อได้ออกมาเป็นค่า magnitude ก่อนนำไป plot และก็ยังมีข้อความแบ่งสี Left Right เหมือนเดิม

![image](https://user-images.githubusercontent.com/87507926/142210168-ba68ae49-5c24-42e7-8b7d-4fd0a5985583.png)
![image](https://user-images.githubusercontent.com/87507926/142210176-3f0f3ba2-ab60-41b3-9b05-bc771d7632eb.png)
![image](https://user-images.githubusercontent.com/87507926/142210188-0f46eeb0-8e71-47fa-88ac-6d1bd2b1aa71.png)


# ฟีเจอร์อื่นๆเพิ่มเติม
- เราได้มีการสร้างปุ่มสำหรับสร้าง pop up ของแต่ละกราฟ เพื่อให้วิเคราะห์ได้ง่ายขึ้นนั่นคือปุ่ม inspect time กับ inspect frequency 

![image](https://user-images.githubusercontent.com/87507926/142213039-e53c261e-1c70-4456-9688-643e72021326.png)

- ต่อมาเราก็มีปุ่มสำหรับ Reset ค่าทั้งหมดทิ้งนั่นคือ Clear all 

![image](https://user-images.githubusercontent.com/87507926/142216275-6b174725-23b5-453c-b4f9-f25f19280191.png)

- เรายังได้ทำปุ่มสำหรับเล่นและหยุดเสียงที่ได้จากการรวมสัญญาณเสียงที่เราเลือกแล้วรวมได้ด้วยแต่ ถ้าอยากทดลองให้ download folder ทั้ง 2 folder ด้านบนได้เลยโดย folder sound_signal จะมีไฟล์เสียให้ลองมากมาย

![image](https://user-images.githubusercontent.com/87507926/142216686-3571a374-fec8-4aae-896b-51f48e01cfbe.png)

- และสุดท้ายเราก็ได้ทำ status bar ไว้คอยแสดงข้อความบอกผู้ใช้ถึงสิ่งที่ควรทำ หรือ ผลลัพธ์ของการทำต่างๆ

![image](https://user-images.githubusercontent.com/87507926/142217108-f9b148b8-9451-4c50-9513-56d367d90eea.png)



