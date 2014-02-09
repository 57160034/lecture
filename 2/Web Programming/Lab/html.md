# HTML

## Form
ใช้รับข้อมูลจากผู้ใช้และส่งค่าไปยังหน้าต่างๆ

```html
<form action="ACTION" method="METHOD">
  <!-- อินพุตต่างๆ -->
</form>
```

- ACTION = หน้าที่จะส่งข้อมูลไป
- METHOD = วิธีที่จะใช้ในการส่งข้อมูล
  - get = ข้อมูลที่ส่งจะต่อท้าย URL ไป เช่น login.jsp?username=admin&password=P@ssw0rd
  - post = ข้อมูลที่ส่งจะ**ไม่**ต่อท้าย URL ไป

### Input Type
ประเภทต่างๆ ที่ใช้ในการรับข้อมูล

#### Text
ข้อความทั่วไป

```html
<input type="text" name="PARAMETER_NAME"/>
```

- PARAMETER_NAME = ชื่อพารามิเตอร์ที่จะส่งไป

#### Password
รหัสผ่าน

```html
<input type="password" name="PARAMETER_NAME"/>
```

- PARAMETER_NAME = ชื่อพารามิเตอร์ที่จะส่งไป

#### Radio
เลือกหนึ่งอย่าง

```html
<input type="radio" name="PARAMETER_NAME" value="VALUE1"/> Value 1
<input type="radio" name="PARAMETER_NAME" value="VALUE2"/> Value 2
<input type="radio" name="PARAMETER_NAME" value="VALUE3"/> Value 3
```

- PARAMETER_NAME = ชื่อพารามิเตอร์ที่จะส่งไป
- VALUE = ค่าที่จะส่งไป

#### Checkbox
เลือกหลายอย่าง

```html
<input type="checkbox" name="PARAMETER_NAME" value="VALUE1"/> Value 1
<input type="checkbox" name="PARAMETER_NAME" value="VALUE2"/> Value 2
<input type="checkbox" name="PARAMETER_NAME" value="VALUE3"/> Value 3
```

- PARAMETER_NAME = ชื่อพารามิเตอร์ที่จะส่งไป
- VALUE = ค่าที่จะส่งไป

#### Select
เลือกหนึ่งอย่าง

```html
<select name="PARAMETER_NAME">
  <option value="VALUE1">Value 1</option>
  <option value="VALUE2">Value 2</option>
  <option value="VALUE3">Value 3</option>
</select>
```

- PARAMETER_NAME = ชื่อพารามิเตอร์ที่จะส่งไป
- VALUE = ค่าที่จะส่งไป

#### Hidden
ส่งค่าไปโดยไม่ให้ผู้ใช้เห็น

```html
<input type="hidden" name="PARAMETER_NAME" value="VALUE"/>
```

- PARAMETER_NAME = ชื่อพารามิเตอร์ที่จะส่งไป
- VALUE = ค่าที่จะส่งไป

#### Submit
"ทำการส่งค่า" ทั้งหมดในฟอร์มและค่าของตัวเองไปด้วย

```html
<input type="submit" name="PARAMETER_NAME" value="VALUE"/>
```

- PARAMETER_NAME = ชื่อพารามิเตอร์ที่จะส่งไป
- VALUE = ค่าที่จะส่งไป

## Link
ใช้สร้างลิงค์ให้ผู้ใช้คลิก

```html
<a href="LOCATION">TEXT</a>
```

ตัวอย่าง:
<a href="http://www.google.com/">Google</a>

- LOCATION = หน้าที่จะไป
- TEXT ข้อความที่แสดง

## Image
ใช้แสดงรูปภาพ

```html
<img src="LOCATION" width="WIDTH" height="HEIGHT"/>
```

ตัวอย่าง:
<img src="https://uploads.github.com/raw/github/media/master/octocats/octocat.png" width="256" height="256"/>

- LOCATION = ตำแหน่งไฟล์รูปภาพ
- WIDTH = ความกว้างของรูป
- HEIGHT = ความสูงของรูป

## Table
ใช้สร้างตาราง

```html
<table>
  <thead>
    <tr>
      <th>HEADER1</th>
      <th>HEADER2</th>
      <th>HEADER3</th>
      <!-- th, th, th, ... -->
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>DATA1</td>
      <td>DATA2</td>
      <td>DATA3</td>
      <!--- td, td, td, ... -->
    </tr>
    <tr>
      <td>DATA1</td>
      <td>DATA2</td>
      <td>DATA3</td>
      <!--- td, td, td, ... -->
    </tr>
    <tr>
      <td>DATA1</td>
      <td>DATA2</td>
      <td>DATA3</td>
      <!--- td, td, td, ... -->
    </tr>
    <!-- tr, tr, tr, ... -->
  </tbody>
</table>
```

ตัวอย่าง:
<table>
  <thead>
    <tr>
      <th>HEADER1</th>
      <th>HEADER2</th>
      <th>HEADER3</th>
      <!-- th, th, th, ... -->
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>DATA1</td>
      <td>DATA2</td>
      <td>DATA3</td>
      <!--- td, td, td, ... -->
    </tr>
    <tr>
      <td>DATA1</td>
      <td>DATA2</td>
      <td>DATA3</td>
      <!--- td, td, td, ... -->
    </tr>
    <tr>
      <td>DATA1</td>
      <td>DATA2</td>
      <td>DATA3</td>
      <!--- td, td, td, ... -->
    </tr>
    <!-- tr, tr, tr, ... -->
  </tbody>
</table>

- HEADER = หัวข้อของคอลัมน์นั้น
- DATA = ข้อมูลในคอลัมน์นั้น

## Header
ใช้แสดงข้อความหัวข้อ (H1 ใหญ่สุด, H6 เล็กสุด)

```html
<h1>H1</h1>
<h2>H2</h2>
<h3>H3</h3>
<h4>H4</h4>
<h5>H5</h5>
<h6>H6</h6>
```

ตัวอย่าง:
<h1>H1</h1>
<h2>H2</h2>
<h3>H3</h3>
<h4>H4</h4>
<h5>H5</h5>
<h6>H6</h6>
