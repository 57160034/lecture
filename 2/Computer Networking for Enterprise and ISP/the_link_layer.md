# Chapter 5 The Link Layer: Links, Access Networks, and LANs

## 5.1 Introduction to Link Layer

### 5.1.1 The Services Provided by the Link Layer

- Framming: เป็นลักษณะของข้อมูลในชั้น Link-layer
- Link access: เป็นกำหนดคุณลักษณะในการเชื่อมต่อและส่งข้อมูลบนลิงก์ใช้โปรโตคอล MAC
- Reliable delivery: การันตีว่าข้อมูลที่ถูกส่งบนลิงก์จะสามารถส่งได้อย่างไม่มีปัญหา
- Error detection and correction: มีการตรวจสอบและแก้ไขข้อผิดพลาด

### 5.1.2 Where Is the Link Layer Implemented?

ใน Network adapter ที่รู้จักกันในชื่อว่า Network interface card (NIC)

## 5.2 Error-Detection and -Correction Techniques

### 5.2.1 Parity Checks

[Parity checks](https://en.wikipedia.org/wiki/Parity_bit)

### 5.2.2 Checksumming Methods

[Checksumming Methods](https://en.wikipedia.org/wiki/Checksum)

### 5.2.3 Cyclic Redundancy Check (CRC)

[Cyclic Redundancy Check](https://en.wikipedia.org/wiki/Cyclic_redundancy_check)

## 5.3 Multiple Access Links and Protocols

ลิงก์ในเครือข่ายมี 2 ประเภท คือ

1. Point-to-point link: หนึ่งผู้รับกับหนึ่งผู้ส่ง โดยมีโปรโตคอลที่มีลักษณะนี้ เช่น Point-to-point protocol (PPP) หรือ High-level data link control (HDLC)
2. Broadcast link: มีผู้รับและผู้ส่งหลายๆ คน

บทนี้จะมาพูดถึงปัญหาการใช้แบบ Multiple access เนื่องจาก Link-layer นั้นถูกสร้างมาเพื่อเป็น Point-to-point link อย่างเดียว จึงต้องมีการพัฒนาโปรโตคอลใหม่เพื่อสนับสนุนการทำงานแบบ Broadcast ให้มากขึ้น

### 5.3.1 Channel Partitioning Protocols

แบ่งเป็น 3 วิธี คือ

1. Time-division multiplexing (TDM): แบ่งการใช้งานตามระยะเวลา หนึ่งระยะเวลาจะมีผู้ใช้ได้เพียงโฮสต์เดียว และผลัดเปลี่ยนกันไปเรื่อยๆ
2. Frequency-division multiplexing (FDM): แบ่งช่องการส่งออกเป็นความถี่ย่อย และอนุญาตให้ผู้ใช้งานเข้าใช้ตามความถี่ย่อยได้พร้อมๆ กัน
3. Code-division multiple access(CDMA): ใช้การใส่ unique code ลงไปในเฟรม และในแต่ละโหนด โหนดที่รับข้อมูลจะทำการถอดรหัสโดยใช้ code ดังกล่าวนี้ หมายความว่าสามารถส่งไปได้พร้อมกันแต่จะเพียงโหนดที่ระบุเท่านั้นถึงจะได้เฟรมข้อมูล

### 5.3.2 Random Access Protocols

อนุญาตให้แต่ละโหนดส่งได้เต็มอัตรา และหากมีการชนกันของข้อมูลเกิดขึ้นก็จะมีการสุ่มเวลาเพื่อทำการรอก่อนที่จะส่งใหม่ในอัตราเดิม

ALOHA เป็นโปรโตคอลที่ใช้ Random access protocols โดยมีการแบ่งเฟรมออกเป็นสล็อตตามสล็อตของเวลา การที่เฟรมนั้นจะถูกส่งออกไปได้ต้องรอให้มีการเริ่มสล็อตของเวลาใหม่ก่อน โหนดสามารถตรวจจับการชนกันของข้อมูลได้ก่อนจะหมดสล็อตของเวลาและจะส่งใหม่โดยการสุ่มเวลาและความน่าจะเป็นที่เฟรมข้อมูลจะมีการชนกัน

ความน่าจะเป็นนี้ถูกแบ่งตามสองเหตุการณ์คือ เหตุการณ์แรกที่จะเกิดการส่งใหม่ทันที กับเหตุการณ์ที่สองที่จะมีการข้ามสล็อตเวลา และจะคำนวณค่าความน่าจะเป็นนี้ใหม่ในสล็อตเวลาต่อไป โดยมีความน่าจะเป็นเท่ากับ `(1-p)`

แต่เมื่อมีการเพิ่มจำนวนโหนดมากขึ้น ก็จะเกิดสิ่งที่เรียกว่า empty slot ซึ่งเป็นช่วงที่มีการสุ่มเวลาและรอ ทำให้เกิดการสิ้นเปลือง ความน่าจะเป็นที่โหนดอื่นจะไม่มีการส่งซ้ำมีค่าเท่ากับ `(1-p)^(N-1)` ในขณะเดียวกัน ความน่าจะเป็นที่โหนดใดโหนดหนึ่งจะส่งสำเร็จมีค่าเท่ากับ `Np(1-p)^(N-1)`ALOHA จะมีการ Synchronize กันระหว่างโหนดในขณะที่มีการส่งข้อมูลด้วย

Carrier Sense Multiple Access (CSMA)  แบ่งเป็น 2 รูปแบบคือ

1. Carrier sense multiple access with collision detection  (CSMA/CD): ถ้าหากชนกัน (โดยใช้การ monitoring signal energy) ยุติการส่ง รอ และทำการส่งใหม่ โดยช่วงเวลาที่จะส่งใหม่นั้นใช้การคำนวณจาก Binary exponential backoff algorithm
2. Carrier sense multiple access with collision avoidance (CSMA/CA): ถ้า carrier sensing แล้วพบว่า channel ไม่ว่างก็จะไม่เสี่ยงส่งข้อมูลเลย

### 5.3.3 Taking-Turn Protocols

แบ่งเป็น 2 โปรโตคอลคือ

1. Polling protocols: มี master node คอยควบคุมว่า node จะได้ส่งแบบ round-robin 
2. Token-passing protocols: ไม่มี master node ใช้การแลกเปลี่ยน token กัน ใครได้ token ก็จะสามารถส่งได้

### 5.3.4 DOCSIS: The Link-Layer Protocol for Cable Internet Access

เป็นรูปแบบการส่งข้อมูลบนสายเคเบิล ใช้ FDM ในการแบ่งช่องสัญญาณ และใช้ TDM ในการแบ่งช่องสัญญาณให้กับผู้ใช้อีกที มีการส่ง control message เรียกว่า MAP ในการอนุญาตให้แต่ละผู้ใช้ใช้งานในแต่ละสล็อตของเวลา และหากมีการชนกันของข้อมูลก็จะใช้ binary exponential backoff เพื่อส่งใหม่

ครบเลยทีเดียว!!

## 5.4 Switch Local Area Networks

Switch ใน LAN ทำหน้าที่ในการ forwarding link-layer โดย ใช้ link-layer address ในเลเยอร์ที่ 2 ดังนั้นใน switch จึงไม่มีการทำ routing ใดๆ

### 5.4.1 Link-Layer Addressing and ARP

การ addressing ใน Link-layer ทำได้โดยการใช้ link-layer address ที่เรียกว่า MAC มีลักษณะเป็น hexadecimal notation ขนาด 6 ไบต์ โดยทุกๆ NIC จะมี MAC address ไม่ซ้ำกัน และมีค่าถาวร การกำหนด MAC address ให้กับอุปกรณ์มีการแบ่งโดย IEEE

MAC address เป็น flat structure แตกต่างกับ IP ที่เป็น hierarchical structure ซึ่งมีการแบ่งเป็น network part, host part

ในเลเยอร์ 2 การจะส่งข้อมูลจะใช้ MAC address ของโฮส์ปลายทางในการอ้างอิง และ broadcast ออกไป (โดยใช้ MAC broadcast address = FF-FF-FF-FF-FF-FF) จะมีเพียงโฮสต์ที่มี MAC address ตรงกันเท่านั้นที่จะทำการรับเฟรมข้อมูล นอกเหนือจากนั้นก็จะดร็อปเฟรมข้อมูลทิ้งไป

### 5.4.2 Ethernet

### 5.4.3 Link-Layer Switches

### 5.4.4 Virtual Local Area Netowkrs (VLANs)

## 5.5 Link Virtualization: A Network as a Link Layer

### 5.5.1 Multiprotocol Label Swiching

## 5.6 Data Center Networking

## 5.7 Retrospective: A Day in the Life of a Web Page Request

## 5.8 Summary
