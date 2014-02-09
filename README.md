lecture
=======

**itkmitl10/lecture** เป็น Repository ซึ่งถูกสร้างขึ้นเพื่อใช้ในการเก็บไฟล์ Lecture ต่างๆ ที่เพื่อนในรุ่นบันทึกไว้ โดยมีจุดมุ่งหมายเพื่อรวบรวมและแบ่งปันความรู้ซึ่งกันและกัน อีกเหตุผลซึ่งทำให้เราตระหนักได้ถึงความจำเป็นที่จะต้องมีโครงการนี้คือ การศึกษาในมหาวิทยาลัยแม้จะมีการอบรมหรือฝึกสอนโดยคณาจารย์ที่มีคุณภาพแล้ว การพึ่งพาตนเองและการช่วยเหลือซึ่งกันและกันก็เป็นปัจจัยที่สำคัญเหมือนกัน โครงการนี้จึงถูกสร้างขึ้นด้วยพื้นฐานแนวคิดนี้

> เราไม่อาจรู้ได้ว่าวันไหนอาจารย์จะไม่สอน ไม่อาจรู้ได้ว่าอารมณ์ของอาจารย์ที่มาสอนนั้นเป็นเช่นไร หรือแม้กระทั่งไม่อาจรู้ว่าหลังจบคลาสเรียนไปนั้นเราได้เรียนรู้อะไรไปบ้าง แต่สิ่งที่เรารู้คือวันสอบที่กำลังมาถึงนั้น เราจะต้องผ่านมันไปให้ได้

# Get Lecture

**itkmitl10/lecture** ใช้ซอฟต์แวร์ git ในการจัดการข้อมูล โดยผู้ใช้งานสามารถเข้าถึงข้อมูลใน Repository ได้โดยตรงผ่านทางเว็บไซต์ [GitHub](https://github.com/itkmitl10/lecture) , สามารถดาวโหลดเป็นไฟล์บีบอัดได้ และสามารถทำการ `clone` โครงการทั้งหมดได้ด้วยคำสั่ง

```git
git clone https://github.com/itkmitl10/lecture
```

lecture ใน repository ล่าสุด อัพเดตวันที่ 9 กุมภาพันธ์ 2557

```
.
├── 2
│   ├── Computer Networking for Enterprise and ISP
│   │   ├── IPv6.md
│   │   └── Lab
│   │       └── Dynamic Routing.md
│   ├── Database System and Concepts
│   │   └── Lab
│   │       ├── README.md
│   │       ├── controlling_transactions.md
│   │       ├── restricitng_and_sorting_data.md
│   │       └── writing_sql_statements.md
│   └── Web Programming
│       └── Lab
│           ├── README.md
│           ├── html.md
│           ├── jsp.md
│           └── survival_guide.md
├── 3
│   └── Information System Security
│       └── Exam
│           └── Midterm_Exam_ISS.pdf
├── LICENSE
└── README.md

10 directories, 13 files
```

# Description

**itkmitl10/lecture** ใช้ฟอแมตการแบบ Markdown เพื่อความง่ายต่อการเขียนและแสดงผลบนเว็บไซต์ (สามารถดูตัวอย่างคำสั่ง Markdown ได้[ที่นี่](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)) แต่หากต้องการแสดงผลในลักษณะอื่น ควรที่จะมีการติดตั้งปลั๊กอินที่มีความสามารถในการอ่าน Markdown ก่อน โดยโครงการเปิดรับ lecture จากเพื่อนๆ ทุกคนในทุกรูปแบบที่ส่งมา และ_อนุญาตให้มีการอ้างอิงเครดิตกลับไปยังผู้เขียนหรือผู้จดได้_

ในกรณีที่มีปัญหาการใช้งาน หรือความคิดเห็นเพิ่มเติมใดๆ เกี่ยวกับโครงการนี้สามารถติดต่อได้ที่ [@pe3zx](https://twitter.com/pe3zx) หรือการโพสต์ในหน้า [Issues](https://github.com/itkmitl10/lecture/issues)

# Q&A

- ทำไม่ใช้ cloud storage พวก Dropbox, Google Drive แชร์ให้เพื่อนแทน
    - มันไม่ Geek
- อยากจะแชร์ lecture ให้เพื่อนบ้างทำยังไง
    - ถ้าเป็น lecture ที่จดมา ให้ถ่ายรูปมาให้ชัดที่สุด หรือถ้าเป็น lecture แบบพิมพ์ก็ส่งมาได้เลย เดี๋ยวจัดการหน้าตาให้
- นอกจาก lecture แล้ว สามารถส่งอะไรได้อีก
    - ข้อสอบเก่า, แบบฝึกหัด

# License

<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by-nc/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">itkmitl10/lecture</span> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/deed.en_US">Creative Commons Attribution-NonCommercial 4.0 International License</a>.<br />Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/itkmitl10/lecture" rel="dct:source">https://github.com/itkmitl10/lecture</a>.
