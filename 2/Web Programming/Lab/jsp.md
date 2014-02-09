# JSP

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```

## Set
ใช้ตั้งค่าตัวแปร

```jsp
<c:set var="VARIABLE_NAME" value="VALUE" scope="SCOPE"/>
```

- VARIABLE_NAME = ชื่อตัวแปร
- VALUE = ค่าของตัวแปร สามารถใส่เป็น [Expression Language (EL)](https://github.com/itkmitl10/lecture/blob/master/2/Web%20Programming/Lab/jsp.md#expression-language) ได้เช่นกัน
- SCOPE = สโคปของตัวแปร
  - page (ค่าเริ่มต้นถ้าไม่กำหนด) = ใช้ในเฉพาะในเพจนั้นๆ
  - request = ใช้ได้ในรีเควสเดียวกัน เช่น มีการฟอร์เวิร์ดรีเควส
  - session = ใช้ได้ในเซสชั่นเดียวกัน
  - application = ใช้ได้ในแอพพลิเคชั่นเดียวกัน

## If
ใช้ตรวจสอบเงื่อนไข

```jsp
<c:if test="CONDITION">
  <%-- คำสั่งหรือการแสดงผลต่างๆ --%>
</c:if>
```

- CONDITION = เงื่อนไงที่ให้ตรวจสอบ ใส่เป็น [Expression Language (EL)](https://github.com/itkmitl10/lecture/blob/master/2/Web%20Programming/Lab/jsp.md#expression-language)

## Choose, When
ใช้ตรวจสอบเงื่อนไขและ**เลือกอย่างใดอย่างหนึ่งจากบนลงล่าง**

```jsp
<c:choose>
  <c:when test="CONDITION">
    <%-- คำสั่งหรือการแสดงผลต่างๆ --%>
  </c:when>
  <c:when test="CONDITION">
    <%-- คำสั่งหรือการแสดงผลต่างๆ --%>
  </c:when>
  <c:when test="CONDITION">
    <%-- คำสั่งหรือการแสดงผลต่างๆ --%>
  </c:when>
  <%-- when, when, when, ... --%>
  <c:otherwise>
    <%-- คำสั่งหรือการแสดงผลต่างๆ เมื่อไม่เข้าเงื่อนใดเลย --%>
  </c:otherwise>
</c:choose>
```

- CONDITION = เงื่อนไงที่ให้ตรวจสอบ ใส่เป็น [Expression Language (EL)](https://github.com/itkmitl10/lecture/blob/master/2/Web%20Programming/Lab/jsp.md#expression-language)

## forEach
ใช้วนลูป แบ่งเป็น 2 แบบหลักๆ

1. วนลูปตัวเลข
  ```jsp
  <c:forEach var="VARIABLE_NAME" begin="BEGIN" end="END" step="STEP">
  </c:forEach>
  ```
    - VARIABLA_NAME = ชื่อตัวแปร
    - BEGIN = เลขเริ่มต้น
    - END = เลขสุดท้าย
    - STEP = การกระโดด (ค่าเริ่มต้นถ้าไม่กำหนดคือ 1)
  
2. วนลูปสิ่งของ

  ```jsp
  <c:forEach var="VARIABLE_NAME" items="COLLECTION">
  </c:forEach>
  ```

  - VARIABLA_NAME = ชื่อตัวแปร
  - COLLECTION = สิ่งของ ส่วนใหญ่เป็นอาเรย์ ใส่เป็น [Expression Language (EL)](https://github.com/itkmitl10/lecture/blob/master/2/Web%20Programming/Lab/jsp.md#expression-language)

## Expression Language
ใช้ดึงค่าตัวแปร และคำนวณค่าต่างๆ

```jsp
${VARIABLE_NAME} <%-- คืนค่าในตัวแปร --%>
${VARIABLE_NAME == null} <%-- คืนค่า true หรือ false --%>
${empty VARIABLE_NAME} <%-- คืนค่า true หรือ false --%>
${VARIABLE_NAME != null} <%-- คืนค่า true หรือ false --%>
${not empty VARIABLE_NAME} <%-- คืนค่า true หรือ false --%>
${VARIABLE_NAME < 5} <%-- คืนค่า true หรือ false --%>
${VARIABLE_NAME <= 5} <%-- คืนค่า true หรือ false --%>
${VARIABLE_NAME > 5} <%-- คืนค่า true หรือ false --%>
${VARIABLE_NAME >= 5} <%-- คืนค่า true หรือ false --%>

${BEAN_NAME.ATTRIBUTE_NAME} <%-- คืนค่า attribute ใน bean นั้นๆ (ใช้กับออปเจคที่เป็น JavaBeans) --%>
${user.firstName} ${user.lastName} <%-- Sarach Tuomchomtam --%>
```

**หมายเหตุ: ถ้าไม่[ระบุสโคปของตัวแปร](https://github.com/itkmitl10/lecture/blob/master/2/Web%20Programming/Lab/jsp.md#pagescope)ที่จะดึง เจเอสพีจะไล่หาตัวแปรในสโคปต่างๆ ตามลำดับดังนี้ page -> request -> session -> application**

### Implicit Objects
ออปเจคที่ Expression Language มีให้ใช้อยู่แล้ว

#### param
ใช้ดึงค่าจากพารามิเตอร์ที่ได้รับมา

```jsp
${param.PARAMETER_NAME}
```

- PARAMETER_NAME = ชื่อพารามิเตอร์ที่จะดึงค่า

#### paramValues
ใช้ดึงค่าจากพารามิเตอร์ที่ได้รับมาแบบหลายค่า (คืนค่าเป็นอาเรย์)

```jsp
${paramValues.PARAMETER_NAME}
```

- PARAMETER_NAME = ชื่อพารามิเตอร์ที่จะดึงค่า

#### pageScope
ใช้ดึงค่าที่อยู่ใน page สโคป

```jsp
${pageScope.VARIABLE_NAME}
```

- VARIABLE_NAME = ชื่อตัวแปรที่จะดึงค่า

#### requestScope
ใช้ดึงค่าที่อยู่ใน request สโคป

```jsp
${requestScope.VARIABLE_NAME}
```

- VARIABLE_NAME = ชื่อตัวแปรที่จะดึงค่า

#### sessionScope
ใช้ดึงค่าที่อยู่ใน session สโคป

```jsp
${sessionScope.VARIABLE_NAME}
```

- VARIABLE_NAME = ชื่อตัวแปรที่จะดึงค่า

#### applicationScope
ใช้ดึงค่าที่อยู่ใน application สโคป

```jsp
${applicationScope.VARIABLE_NAME}
```

- VARIABLE_NAME = ชื่อตัวแปรที่จะดึงค่า
