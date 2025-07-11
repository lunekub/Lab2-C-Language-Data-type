# ใบงานที่ 02.02 การคำนวณและแปลงชนิดข้อมูลเบื้องต้น


### 1. การคำนวณด้วยชนิดข้อมูลต่างกัน (Type Promotion)

__วัตถุประสงค์__ 

ทำความเข้าใจว่าการคำนวณระหว่างชนิดข้อมูลต่างกันมีผลลัพธ์อย่างไร

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`


``` c
Serial.println("\n--- ทดสอบการคำนวณระหว่างชนิดข้อมูล ---");
int numA = 10;
float numB = 3.0;
double numC = 3.0;

float resultFloat = numA / numB; // int หาร float ผลลัพธ์จะเป็น float
Serial.print("10 / 3.0 (ผลลัพธ์ float): ");
Serial.println(resultFloat, 2);

double resultDouble = numA / numC; // int หาร double ผลลัพธ์จะเป็น double
Serial.print("10 / 3.0 (ผลลัพธ์ double): ");
Serial.println(resultDouble, 10);

int resultInt = numA / (int)numB; // int หาร int ผลลัพธ์จะเป็น int (ทศนิยมถูกตัดทิ้ง)
Serial.print("10 / (int)3.0 (ผลลัพธ์ int): ");
Serial.println(resultInt);
```

- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว

__คำถาม__ 

1.1  ทำไม 10 / 3.0 (เมื่อตัวหารเป็น float หรือ double) ถึงได้ผลลัพธ์เป็นทศนิยม แต่เมื่อตัวหารถูกแปลงเป็น int แล้วผลลัพธ์เป็นจำนวนเต็ม?

- เมื่อทำการ หารระหว่าง int กับ float หรือ double เช่น 10 / 3.0
ตัวแปรที่เป็น int จะถูกแปลงเป็นชนิดข้อมูลที่มีความแม่นยำสูงกว่า (เช่น float หรือ double) อัตโนมัติ
จากนั้นการหารจะทำแบบ เลขทศนิยม (floating-point division)
ผลลัพธ์จึงเป็นทศนิยม เช่น 3.3333...

แต่เมื่อแปลงตัวหารเป็น int ก่อน เช่น 10 / (int)3.0 หรือ 10 / 3
การหารจะเป็นการหารระหว่าง int กับ int
การหารระหว่างจำนวนเต็มจะทำ หารจำนวนเต็ม (integer division) ซึ่งจะตัดทิ้งส่วนที่เป็นทศนิยม
ผลลัพธ์จึงเป็นจำนวนเต็ม เช่น 3 (ส่วน .3333 ถูกตัดทิ้ง)



### 2. การแปลงชนิดข้อมูล (Explicit Type Casting)

__วัตถุประสงค์__ 

ฝึกการแปลงชนิดข้อมูลด้วยตัวเอง

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`


``` c
Serial.println("\n--- ทดสอบการแปลงชนิดข้อมูล (Type Casting) ---");
float temperatureCelsius = 25.789;
Serial.print("อุณหภูมิ Celsius (float): ");
Serial.println(temperatureCelsius);

int temperatureInteger = (int)temperatureCelsius; // แปลง float เป็น int
Serial.print("อุณหภูมิ Celsius (แปลงเป็น int): ");
Serial.println(temperatureInteger);

// ตัวอย่างการใช้ char เป็นตัวเลข
char letter = 'P';
int asciiValue = (int)letter;
Serial.print("อักขระ 'P' มีค่า ASCII: ");
Serial.println(asciiValue);

// ตัวอย่างการแปลง int เป็น float
int count = 7;
int total = 20;
float average = (float)count / total; // ต้องแปลงอย่างน้อยหนึ่งตัวให้เป็น float ก่อนหาร
Serial.print("ค่าเฉลี่ย (7/20): ");
Serial.println(average);
```

- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว


__คำถาม__

- ในการเขียนโปรแกรม ต้องทำ Type Casting ในสถานการณ์ใดบ้าง

- ป้องกันการตัดทศนิยม

เช่น: (float)7 / 20 เพื่อให้ผลลัพธ์เป็น 0.35 แทน 0

แปลงค่าทศนิยมเป็นจำนวนเต็ม

เช่น: (int)25.789 ได้ 25 (ตัดเศษ)

แปลงตัวอักษรเป็นรหัส ASCII

เช่น: (int)'A' ได้ 65

ให้ชนิดข้อมูลตรงกันในการคำนวณ

เช่น: (double)x + y เมื่อ x เป็น int, y เป็น double

ใช้กับฟังก์ชันที่ต้องการชนิดเฉพาะ

เช่น: delay((unsigned long)time)

ปรับขนาดค่าหรือหน่วยเพื่อจัดเก็บหรือแสดงผล

เช่น: (int)(voltage * 100) เพื่อให้ได้ค่าจำนวนเต็ม
