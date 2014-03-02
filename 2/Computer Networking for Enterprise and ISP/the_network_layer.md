# The Network Layer

## 4.1 Introduction

### 4.1.1 Forwarding and Routing

- Forwarding: เมื่อแพ็คเกตที่ถูกส่งมาจากโฮสต์ทางขาเข้า (input link) แล้ว กระบวนการที่ทำการย้ายแพ็คเกตดังกล่าวนี้ไปยังขาออก (output link) ที่เหมาะสมเรียกว่าการ forwarding
- Routing: เป็นกระบวนการที่ใช้ในการค้นหาเส้นทางที่เหมาะสมให้กับแพ็คเกต เพื่อให้การส่งแพ็คเกตเป็นไปอย่างมีประสิทธิภาพมากที่สุด โดยจะมีการใช้อัลกอริธึมที่เรียกว่า Routing Algorithms ในการหาเส้นทาง

Forwarding Table (a.k.a. Routing Table): เป็นองค์ประกอบของเราท์เตอร์ที่ใช้เก็บข้อมูลที่ได้มาจากการตรวจสอบส่วนหัวของแพ็คเกตกับอินเตอร์เฟสขาออกของเราท์เตอร์ โดยค่าที่อยู่ใน Forwarding table อาจถูกกำหนดจากผู้ใช้งาน หรือจากการใช้ Routing Algorithms ช่วยก็ได้

โดยลักษณะของการ forwarding จะถูกใช้อีกครั้งในกระบวนการ Packet switch ซึ่งอยู่ใน Link-layer โดยใน Link-layer (layer 2) นั้น กระบวนการตัดสินใจว่าจะส่งแพ็คเกตไปยังอินเตอร์เฟสใดจะขึ้นอยู่กับค่าที่อยู่ในฟิลด์ของเฟรมของ Link-layer ในขณะที่การ forwarding ใน Network layer นั้นจะขึ้นอยู่กับที่อยู่ในฟิลด์ของ Network layer

เราท์เตอร์เป็นอุปกรณ์ที่อยู่ใน Network layer (layer 3) แต่ก็ยังต้องมีการประยุกต์ใช้คุณสมบัติของ Link-layer (layer 2) ด้วย ในทางการตลาดนั้นจะเรียกเราท์เตอร์ที่มีอินเตอร์เฟส Ethernet ว่าเป็น "สวิตซ์ในเลเยอร์ที่ 3"

### 4.1.2 Network Service Models

เมื่อมีการส่งข้อมูลโดยใช้โปรโตคอลที่ต้องอาศัยความเชื่อถือจากชั้น Transport layer ลงมายังชั้นของ network layer คุณสมบัติต่างๆ ที่ Network layer จะต้องมีเพื่อสนับสนุนการทำงานของ Transport layer นั้นจะเรียกว่า Network service model

ตัวอย่างของ Network service model เช่น

- Guaranteed delivery: จะต้องการันตีว่าแพ็คเกตที่ถูกส่งนั้นจะต้องถึงโฮสต์ปลายทาง
- Guaranteed delivery with bounded delay: นอกจากจะมีการการันตีว่าแพ็คเกตนั้นจะถูกส่งถึงโฮส์เป้าหมายแล้ว ยังมีการกำหนดขอบเขตของดีเลย์ด้วย

นอกจากในเรื่องของความน่าเชื่อถือในการส่งแพ็คเกตแล้ว ยังมี network service model ที่จัดการเกี่ยวกับการไหลของแพ็คเกตด้วย

- In-order packet delivery: การันตีว่าแพ็คเกตที่ถูกส่งนั้นจะถึงผู้รับด้วยลำดับรูปแบบเดียวกันกับตอนที่ผู้ส่งส่งออกมา
- Guaranteed minimal bandwidth: การันตีแบนด์วิธที่น้อยที่สุดที่จะสามารถใช้ในการส่งข้อมูลได้ โดยที่ข้อมูลจะต้องถึงผู้รับอย่างสมบูรณ์
- Guaranteed maximum jitter: การันตีในเรื่องของเวลาที่จะต้องเท่ากันหรือไม่มากกว่าค่าๆ หนึ่ง
- Security services: ในกรณีที่มีการใช้เข้ารหัสด้วยคีย์ network layer ฝั่งผู้รับจะต้องสามารถเข้ารหัส Payloads ของ Datagram ด้วยคีย์นั้นได้เช่นเดียวกันฝั่งผู้ส่งที่จะต้องรับหน้าที่ในการเข้ารหัส payloads และยังต้องสามารถให้บริการในเรื่องของความสมบูรณ์ของข้อมูล และการระบุตัวตนด้วย

ในเครือข่ายอินเทอร์เน็ตใน network layer จะมีการให้บริการที่เรียกว่า *Best-effort service* ซึ่งหมายความง่ายๆ ว่า *No service at all* หรือไม่ให้บริการใดๆ เลย เพื่อทำให้เครือข่ายนี้ใช้งานได้ง่ายที่สุด

เครือข่ายอินเทอร์เน็ตถือเป็นสถาปัตยกรรมทางเครือข่ายแบบหนึ่ง (Network architecture) และยังมีสถาปัตยกรรมเครือข่ายอื่นๆ อีกด้วย เช่น ATM (Asynchronous Transfer Mode) โดยตัว ATM จะมีการใช้ service model สำคัญๆ สองบริการ ดังนี้

- Constant bit rate (CBR): มีการการันตีค่าที่แน่นอนของแบนด์วิธ, มีการการันตีว่าข้อมูลจะไม่สูญหาย, มีการการันตีว่าจะถูกส่งตามลำดับที่ถูกต้อง, มีการจัดการเวลาในการส่ง และมีการป้องกันการเกิดความคับคั่งระหว่างการส่งข้อมูล
- Available bit rate (ABR): มีการการันตีค่าแบนด์วิธที่น้อยที่สุด, การการันตีในเรื่องลำดับของข้อมูล และมีตัวตรวจสอบความคับคั่ง (นอกเหนือจากนี้คือไม่มีการให้บริการ)

## 4.2 Virtual Circuit and Datagram Networks

ในเรื่องของ Transport layer ได้มีการกล่าวถึงตัวเลือกสำหรับแอพพลิเคชัน หากต้องหากใช้ลักษณะการเชื่อมต่อที่น่าจะเชื่อถือก็จะใช้ TCP ที่มี cnnection-oriented แต่ถ้าต้องการความสะดวกรวดเร็วก็ใช้ UDP ที่เป็น connectionless ซึ่งใน Network layer นี้ก็มีตัวเลือกเช่นเดียวกับใน Transport layer

แม้ว่าการมี Connection กับ Connectionless ของ Transport layer กับ Network layer จะค่อนข้างคล้ายกัน แต่ก็มีจุดที่แตกต่างกันคือ

- Network layer เป็นกระบวนการที่ให้ความสนใจในการติดต่อระหว่าง host-to-host ในขณะที่ Transport layer มุ่งไปที่ process-to-process
- แม้ว่าในเครือข่ายปัจจุบันจะมีการใช้ทั้ง connection และ connectionless แต่ก็ยังคงมีบางเครือข่ายที่ใช้เพียงอย่างใดอย่างหนึ่ง เราจะเรียกเครือข่ายที่มีการใช้ connection เพียงอย่างเดียวว่า **Virtual-circuit (VC) networks** ในขณะเดียวกันเราเรียกเครือข่ายที่มีการใช้ connectionless เพียงอย่างเดียวว่า **Datagram networks**

### 4.2.1 Virtual-Circuit Networks

กระบวนการทำงานของ VC networks นั้นมีองค์ประกอบสำคัญ 3 อย่าง ดังนี้

1. Path: กลุ่มของลิงก์และเราท์เตอร์ที่เชื่อมหากันระหว่างโฮสต์ต้นทางกับโฮสต์ปลายทาง
2. VC numbers: เป็นตัวเลข VC ที่กำหนดไว้ในแต่ละลิงก์
3. Forwarding table: ตารางที่ใช้ในการควบคุมการส่งในแต่ละเราท์เตอร์

โดยจะแบ่งกระบวนการทำงานออกเป็น 3 ขั้นตอนดังนี้

1. VC setup: Transport layer มีการส่งสัญญาณมาให้กับ Network layer  โดยจะมีการระบุที่อยู่ของผู้รับไว้ และรอการตอบรับจาก Network layerNetwork layer ทำการหาเส้นทางที่เหมาะสมจากต้นทางไปยังปลายทาง เมื่อได้เส้นทางแล้ว Network layer ทำการตรวจสอบ VC numbers ของแต่ละลิงก์ แล้วทำการเพิ่มใส่ใน Forwarding table ของแต่ละเราท์เตอร์ในเส้นทาง
2. Data Transfer: หลังจากมีการตั้งค่า VC เสร็จแล้ว ก็จะส่งสัญญาณให้มีการส่งข้อมูลได้ โดยก่อนที่แพ็คเกตจะออกจากเราท์เตอร์ ก็จะมีการเปลี่ยนส่วนหัวของแพ็คเกตเป็น VC numbers ตัวถัดไป และเมื่อแพ็คเกตเข้าไปยังขาเข้าก็จะมีการอ่านค่าจากส่วนนี้เช่นกัน
3. VC teardown: หากมีการจะปิด VC ก็จะมีการสั่งให้เราท์เตอร์ในเส้นทางทำการอัพเดต forwarding table

ภายใน Forwarding table จะมีการเก็บอินเตอร์เฟสขาเข้า, VC number ที่จะรับ, อินเตอร์เฟสขาออก และ VC number ที่จะส่งออกไปด้วย และสัญญาณที่ใช้ในการควบคุม VC นั้นจะเรียกว่า signaling messages อยู่ใน signaling protocols

### 4.2.2 Datagram Networks

ในกระบวนการทำงานของ Datagram networks นั้นเราท์เตอร์จะทำเพียงแค่ตรวจสอบที่อยู่ของโฮสต์ปลายทางบนส่วนหัวของแพ็คเกต และดูใน Forwarding table เพื่อที่จะหาเส้นทางที่เหมาะสม 

ขั้นตอนในการจับคู่ที่อยู่ของโฮสต์ปลายกับข้อมูลที่อยู่ใน Forwarding table นั้น จะใช้วิธีที่เรียกว่า **Longest prefix matching rule** ซึ่งก็คือ เราท์เตอร์จะเลือกให้อินเตอร์เฟสขาออกให้กับแพ็คเกตในกรณีที่ที่อยู่ของโฮสต์ปลายทางมีความเหมือนกับข้อมูลใน Forwarding table มากที่สุด

Forwarding table สามารถถูกกำหนดโดยผู้ใช้งานเอง หรือจะใช้อัลกอริธึมในการกำหนดก็ได้

### 4.2.3 Origins of VC and Datagram Networks

**ข้าม**

## 4.3 What's Inside a Router?

ในเราท์เตอร์มีองค์ประกอบสำคัญอยู่ 4 ส่วนด้วยกันคือ

1. Input ports
2. Switching fabric
3. Output ports
4. Routing Processor

### 4.3.1 Input Processing

**ข้าม**

### 4.3.2 Switching

- Switching via memory: ใช้การคัดลอกแพ็คเกตจากบัฟเฟอร์ขาเข้าไปยังหน่วยความจำ ทำการประมวลผลเพื่อหาโฮสต์ปลาย และทำการคัดลอกไปยังบัฟเฟอร์ขาออก
- Switching via bus: ขาเข้าทำการส่งแพ็คเกตไปยังขาออกโดยตรงผ่านทาง shared bus เนื่องจากเมื่อแพ็คเกตมาถึงขาเข้าแล้วมีการเพิ่ม switch-internal label ไปยังส่วนหัวของแพ็คเกตเพื่อบ่งบอกขาออกของแพ็คเกต โดยขาออกก็จะตรวจสอบผ่าน label นี้ว่าใช่ของตนเองหรือไม่ หากใช่ก็จะทำการส่ง
- Switching via interconnection network: ใช้รูปแบบของ cross bar switch ในการส่งข้อมูล ประกอบด้วย bus หลายๆ ตัวเพื่อจัดการปัญหาในเรื่องแบนด์วิธและดีเลย์

### 4.3.3 Output Processing

**ข้าม**

### 4.3.4 Where Does Queueing Occur?

การที่มีการ queueing เกิดขึ้นนั้นมีสาเหตุได้หลายกรณี เช่น การที่แพ็คเกตถูกเก็บอยู่ในหน่วยความจำเพื่อที่จะรอส่งมากเกินไป หรือแบนด์วิธที่น้อย โดยทางขาออกมีวิธีการจัดการยกตัวอย่างเช่น ใช้หลักการ first-come-first-serve

ในอีกกรณีหนึ่งถ้ามีการรอของแพ็คเกตมากเกินไปจนเกิดกว่า drop แพ็คเกตทิ้งนั้น สามารถหาจำนวนแพ็คเกตที่ถูกดรอปไปได้จากการใช้อัลกอริธึมแบบ Active queue management (AQM) เช่น Random early detection (RED) 

ปัญหา head-of-the-line (HOL) blocking เกิดจากกรณีที่อินเตอร์เฟสขาออกไม่สามารถให้บริการได้ ถึงแม้ว่าแพ็คเกตจะสามารถถูกส่งไปยังขาอื่นได้และถึงปลายทางเดียวกันแต่ก็ไม่ได้ถูกส่ง ทำให้เกิดการรออยู่ในหน่วยความจำหรือบัพเฟอร์ วิธีแก้ไขปัญหานี้คือการใช้ HOL blocking prevention ในการพักแพ็คเกตไว้และยังไม่ดรอป แล้วไปส่งแพ็คเกตอื่นไว้จนกว่าอินเตอร์เฟสขาออกจะสามารถใช้งานได้

### 4.3.5 The Routing Control Plane

**ข้าม**

## 4.4 The Internet Protocol (IP): Forwarding and Addressing in the Internet

### 4.4.1 Datagram Format

ดู IPv4 datagram ได้[ที่นี่](https://en.wikipedia.org/wiki/IPv4) โดยมีส่วนประกอบสำคัญคือ

- Version number: เป็นฟิลด์ที่ใช้บอกเวอร์ชันของ IP
- Header length: เป็นฟิลด์ที่ใช้บอกขนาดของส่วนหัวของแพ็คเกต
- Type of service: เป็นฟิลด์ที่ใช้ในกรณีที่ต้องการใช้ IP datagram รูปแบบอื่น เช่น ต้องการลดดีเลย์ลง หรือเพิ่มความน่าเชื่อถือ
- Datagram segment: เป็นฟิลด์ที่ใช้เก็บขนาดของแพ็คเกตทั้งหมด
- Identifier flags, fragmentation offset: ใช้จัดการในเรื่องของ IP fragmentation
- Time-to-live: ใช้เก็บค่าเพื่อควบคุมไม่ให้แพ็คเกตเกิดลูปในเครือข่าย (default = 32)
- Protocol: ใช้ในการระบุโปรโตคอลใน Transport layer ที่ใช้
- Header checksum: ใช้ในการตรวจสอบความผิดพลาดของ IP datagram
- Source and destination IP addresses: ใช้เก็บที่อยู่ของผู้ส่งและผู้รับ
- Options
- Data (payload): ส่วนของข้อมูลจากชั้นก่อน

IP datagram fragmentation เป็นปัญหาที่เกิดขึ้นในกรณีที่ในเลเยอร์ถัดไปมีการกำหนดค่า Maximum transmission unit (MTU) ไว้น้อยกว่าขนาดของแพ็คเกตจริง ทำให้ต้องมีการแบ่งแพ็คเกตเป็นส่วนๆ เพื่อให้สามารถส่งไปได้ (เรียกแต่ละส่วนว่า fragment) โดยจะมีการกำหนดค่า identification, ค่า offset เพื่อบอกว่า fragment นี้เริ่มที่ไบต์ไหน และค่า flag เพื่อบอกในกรณีที่เป็น fragment สุดท้าย

### 4.4.2 IPv4 Addressing

*ข้ามเรื่องการแบ่งไอพี*

DHCP เป็นโปรโตคอลที่ใช้ในการแจกไอพีอัตโนมัติ อยู่ในรูปแบบของ client กับ server โดยที่ client จะต้องทำส่งคำขอไปยัง DHCP server เพื่อให้แจกไอพีมา โดยมีการทำงาน 4 ขั้นตอน คือ

1. DHCP server discovery: เมื่อ client เข้ามาในเครือข่ายแล้ว จะมีการ broadcast DHCP discover message โดยใส่ไอพีตัวเองเป็น 0.0.0.0 ส่งผ่านทาง UDP พอร์ต 67 ไปหา DHCP server
2. DHCP server offer(s): DHCP server ได้รับ DHCP discover message จาก client และทำการตอบด้วย DHCP offer message แบบ broadcast โดยใน DHCP offer message จะประกอบไปด้วย ID ของ discover message, IP address สำหรับ client, mask และเวลาที่ IP นี้จะสามารถใช้งานได้ (IP address lease time)
3. DHCP request: client ตอบ DHCP offer message ด้วย DHCP request message เพื่อขอใช้งานพารามิเตอร์ต่างๆ
4. DHCP ACK: DHCP server ตอบ client ด้วย DHCP ACK message เพื่อยืนยันว่า client สามารถใช้การตั้งค่าดังกล่าวได้

Network address translation (NAT) เป็นกระบวนการในการแปลง private IP ใน LAN ให้เป็น public IP ใน WAN ผ่านทางการกำหนดค่าของ NAT table

UPnP = Universal Plug-n-Play Protocol

### 4.3.4 Internet Control Message Protocol (ICMP)

ICMP เป็นโปรโตคอลที่ใช้ในการตรวจสอบสถานะของระบบ โดยเมื่อส่ง ICMP ไป ผู้รับก็จะทำการตอบค่าตามตารางเพื่อบอกสถานะ [ดูตาราง](https://en.wikipedia.org/wiki/Internet_Control_Message_Protocol)

### 4.4.4 IPv6

[ดูเนื้อหา IPv6](https://github.com/itkmitl10/lecture/blob/master/2/Computer%20Networking%20for%20Enterprise%20and%20ISP/IPv6.md#ipv6)

### 4.4.5 IP Security

*ข้าม*

## 4.5 Routing Algorithms

Routing algorithms แบ่งได้หลายประเภท ตามหนังสือจะแบ่งโดยใช้เกณฑ์ global/decentralized คือ

- Global routing algorithm ใช้หลักการการคำนวณหาเส้นทางที่ดีที่สุดจากต้นทางไปยังปลายทางโดยใช้ข้อมูลทั้งหมดในเครือข่าย หมายความว่าจะต้องมีการติดต่อกับโหนดทุกโหนดในเครือข่าย เช่น Link-state (LS) algorithm
- Decentralized routing algorithm ใช้หลักการคำนวณหาเส้นทาง โดยเริ่มจากการมีข้อมูลเพียงแค่โหนดที่อยู่รอบตัวเท่านั้น หลังจากนั้นจึงค่อยแลกเปลี่ยนข้อมูลกันและคำนวณหาเส้นทางที่ดีขึ้นเรื่อย เช่น Distance-vector (DV) algorithm

นอกจากนั้นยังมี Static routing algorithms ซึ่งผู้ใช้งานกำหนดเอง Dynamic routing algorithm ที่เปลี่ยนไปตามลักษณะของเครือข่าย

### 4.5.1 The Link-State (LS) Routing Algorithm

LS ใช้หลักการของ Dijkstra algorithm ในการหาเส้นทางที่สั้นที่สุด โดยมีขั้นตอนคร่าวๆ ดังนี้

1. โหนดเริ่มต้นจะทำการค้นหาโหนดที่อยู่รอบๆ และเก็บค่า cost มาใส่ตาราง forwarding table (หรือ routing table) และเก็บด้วยว่าโหนดก่อนหน้านี้คือโหนดอะไร 
2. โหนดเริ่มต้นทำการพิจารณาค่า cost ที่ได้ แล้วเลือกเส้นทางที่ค่า cost น้อยที่สุดไปยังโหนดต่อไป
3. ทำซ้ำข้อ 1 ใหม่ โดยในการทำทุกครั้งจะมีการคำนวณ cost ใหม่ และถ้าหากมี cost ที่น้อยลงก็จะมีการอัพเดตตารางตามค่านั้น

ปัญหาที่มีเจอใน LS คือการอัพเดตค่าวนซ้ำในกรณีที่โทโปโลยีเป็นวงกลม (Oscillations)

### 4.5.2 The Distance-Vector (DV) Routing Algorithm

### 4.5.3 Hierarchical Routing

ปัญหาของ LS และ DV จะเกิดขึ้นเมื่อนำไปใช้ในเครือข่ายๆ ขนาดใหญ่มากๆ เพราะจะทำให้เราท์เตอร์ต้องมีการเก็บข้อมูลขนาดใหญ่อย่างสิ้นเปลือง จึงมีการแบ่งกลุ่มของเราท์เตอร์ออกเป็น Autonomous system (AS) โดยในหนึ่ง AS จะมีการใช้อัลกอริธึมเดียวกันหมดเรียกว่า Intra-autonomous system routing protocol โดยมีเราท์เตอร์ตัวหนึ่งทำหน้าที่เชื่อมต่อกับ AS อื่นเรียกว่า Gateway router

สำหรับการพูดคุยกันระหว่าง AS นั้นก็จะใช้โปรโตคอลอีกตัวนึงคือ Inter-autonomous system routing protocol

การทำ Hot-potato routing คือการที่ AS เมื่อได้รับแพ็คเกตมาแล้วจะทำการส่งให้เร็วที่สุด ไปยัง Gateway ที่มีค่า cost น้อยที่สุด

## 4.6 Routing in the Internet

### 4.6.1 Intra-AS Routing in the Internet: RIP

Intra-AS Routing เป็นอัลกอริธึมที่ใช้ภายใน AS หรือเรียกอีกอย่างว่า Interior gateway protocols เช่น **Routing Information Protocol (RIP)**, **Open Shortest Path First (OSPF)** หรือโปรโตคอลใหม่อย่าง **IS-IS**

RIP เป็น Distance vector โดยมีการใช้ RIP response message และ RIP advertisements ในการร้องขอการแลกเปลี่ยนข้อมูลทุกๆ 30 วินาที ค่า cost ที่มากที่สุดที่ RIP ทำงานได้คือ 15 hop โดยจะมี RIP table ซึ่งรู้จักกันในชื่อ Routing table คอยเก็บข้อมูลซับเน็ตปลายทาง, เราท์เตอร์ตัวถัดไป และจำนวน hop ก่อนจะถึงโฮสต์ปลายทางอยู่

### 4.6.2 Intra-AS Routing in the Internet: OSPF

OSPF เป็น Link state ที่ใช้วิธีในการ broadcast ข้อมูลไปยังทุกๆ โหนดภายในเวลา 30 นาที  โดยโปรโตคอล OSPF ยังมีความสามารถในการ authentication ด้วย MD5, สนับสนุนการใช้งานผ่าน Multicast หรือในกรณีที่เส้นทางไปยังโฮสต์ปลายทางมีค่า cost เท่ากัน ก็จะสามารถใช้งานเส้นทางทั้งหมดนั้นได้เลยโดยไม่ได้เลือกให้ใช้เส้นทางใดเพียงเส้นทางเดียว

ในการใช้งานจริงนั้น มีการกำหนด Area border routers เพื่อรับผิดชอบในการ routing ออกไปยังนอก OSPF AS และมี Backbone area ซึ่งทำหน้าที่เป็นส่วนหลักในการเชื่อมแต่ละ AS เข้าด้วยกัน

### 4.6.3 Inter-AS Routing

**ข้าม**

### Important!

- Interior gateway routing via link state routing protocols, such as OSPF and IS-IS
- Interior gateway routing via distance vector routing protocols, such as RIPv2, IGRP and EIGRP
- Exterior gateway routing. The Border Gateway Protocol (BGP), a path vector routing protocol, is the routing protocol used on the Internet for exchanging traffic between Autonomous Systems.

## 4.7 Broadcast and Multicast Routing

- Broadcast Routing: การส่งแพ็คเกตจากโหนดที่เป็นผู้ส่ง (source node) หนึ่งโหนดไปยังโหนดผู้รับ (destination node) หลายๆ โหนด
- Multicast Routing: การส่งแพ็คเกตจากโหนดที่เป็นผู้ส่ง (source node) หนึ่งโหนดไปยังโหนดผู้รับ (destination node) หลายๆ โหนด **โดยที่สามารถข้ามซับเน็ตได้**

### 4.7.1 Broadcast Routing Algorithm

- อัลกอริธึมแบบ N-way-unicast อธิบายง่ายๆ คือ เรามีโหนดผู้ส่งหนึ่งโหนดและจะทำการส่งไปยังโหนดผู้รับจำนวน N โหนด ในอัลกอริธึมนี้โหนดผู้ส่งจะทำการคัดลอกแพ็คเกตที่จะส่งไว้จำนวน N แพ็คเกต และทำการส่งแบบ Unicast Routing ไปยังแต่ละโหนดผู้รับ
    - ข้อดี
        - ง่าย
    - ข้อเสีย
        - ไม่มีประสิทธิภาพ เพราะว่า ผู้ส่งจะต้องทำการส่งหลายรอบ
        - ผู้ส่งจำเป็นต้องรู้รายละเอียดของผู้รับทั้งหมด ทำให้ต้องมีการเพิ่มโปรโตคอลเพิ่มเติม
        - ปัญหาการ Flooding: กรณีการ Flooding จะเกิดขึ้นจากการแก้ปัญหาผู้ส่งคนเดียวส่งให้ผู้ใช้หลายคนโดยใช้วิธีให้โหนดที่ใกล้กันทำการส่งหาโหนดที่ใกล้กันเอง ในกรณีนี้หากมีโทโปโลยีที่มีลักษณะพิเศษ อาจเกิดการ Flooding แบบไม่มีที่ิสิ้นสุดซึ่งเรียกว่า Broadcast Storm ได้
    - ฟีเจอร์เพิ่มเติม
        - การแก้ไขปัญหา Source-duplication แก้ได้โดยการใช้การกระจายเพียงแค่โหนดข้างเคียงและส่งต่อไปเรื่อยๆ ( แต่จะเกิดปัญหาแบบ Broadcast srom ได้ )
        - การแก้ไขปัญหา Flooding ทำได้สองวิธีคือ
            1. การใข้วิธี Sequence-number-controlled flooding 
            2. การใช้วิธี Reverse Path Forwarding (RPF)
        - การแก้ปัญหาแพ็คเกตซ้ำทำได้โดยการใช้วิธี Spanning-Tree Broadcast

### 4.7.2 Multicast
