# Using-Spec-kit-Step-by-Step

ใช้งานจริงบน Windows เหมาะกับเคสที่ใช้ VS / Next.js / .NET:

#

## 0. Concept สั้น ๆ ก่อนเริ่ม

**Spec-Kit คืออะไร?**
มันคือ tool ที่ช่วยให้เราพิมพ์ “สเปกของโปรเจกต์” (spec.md, plan.md, tasks.md) แล้วค่อยให้ AI ช่วย Generate โค้ดตามสเปก แทนการ “vibe code” ไปเรื่อย ๆ

Workflow หลัก:

1. `spec.md` – เขียนว่าอยากได้อะไร, ฟีเจอร์อะไร, acceptance criteria
2. `plan.md` – วางเทคนิค: ใช้ .NET 8, Next.js, MSSQL, Clean Architecture ฯลฯ
3. `tasks.md` – แตกงานย่อยเป็น task ให้ลงมือทำทีละอัน

#

## 1. ติดตั้ง UV / UVX (ครั้งเดียว)

Spec-Kit ใช้ CLI ชื่อ `specify` ที่ติดตั้งผ่าน **uv / uvx**

### 1.1 ติดตั้ง uv/uvx บน Windows

เปิด **PowerShell** แบบ Run as Administrator แล้วรัน:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

เสร็จแล้วปิด–เปิด PowerShell ใหม่ แล้วลองเช็ค:

```powershell
uv --version
uvx --version
```

ถ้าเห็นเลขเวอร์ชัน แปลว่าพร้อมแล้ว ✅

#

## 2. ติดตั้ง Specify CLI (Spec-Kit)

มี 2 แบบ เลือกแบบใดแบบหนึ่งก็ได้ (แนะนำแบบติดตั้งถาวร)

### วิธี A: ติดตั้งถาวร (Recommended)

```powershell
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
```

ทดสอบ:

```powershell
specify --help
```

### วิธี B: ใช้แบบครั้งคราว (ไม่ต้อง install)

ทุกครั้งที่ใช้ให้เรียกผ่าน `uvx`:

```powershell
uvx --from git+https://github.com/github/spec-kit.git specify --help
```

> ถ้า A ใช้ได้แล้ว ผมแนะนำเรียก `specify` ตรง ๆ เลย สะดวกกว่า

#

## 3. สร้างโปรเจกต์ใหม่ด้วย Spec-Kit

สมมติคุณอยากทำโปรเจกต์ชื่อ `SpecKitDemo` ที่มี ProductUI + ProductAPI

1. ไปที่โฟลเดอร์รวมงานของคุณ (ตัวอย่าง)

   ```powershell
   cd D:\Project\Project_2025
   ```

2. สร้างโปรเจกต์ Spec-Kit

   * ถ้าใช้แบบติดตั้งถาวร:

     ```powershell
     specify init SpecKitDemo
     ```
   * หรือถ้าใช้ผ่าน uvx:

     ```powershell
     uvx --from git+https://github.com/github/spec-kit.git specify init SpecKitDemo
     ```

3. เข้าไปในโฟลเดอร์โปรเจกต์

   ```powershell
   cd .\SpecKitDemo
   ```

ตอนนี้ในโปรเจกต์จะมีไฟล์หลัก ๆ อย่าง:

* `spec.md`
* `plan.md`
* `tasks.md`
* `.speckit/` (config ภายใน)

#

## 4. เปิดโปรเจกต์ใน ChatGPT / Copilot พร้อม Spec-Kit

ในโฟลเดอร์ `SpecKitDemo` ให้คุณ:

1. เปิด VS Code หรือ IDE ที่ใช้
2. เปิด ChatGPT / GitHub Copilot / Claude Code *ในโฟลเดอร์นี้*
3. จากนั้นคุณจะสามารถใช้ “คำสั่งแบบ slash” ของ Spec-Kit ในแชตได้ เช่น

   * `/speckit.constitution`
   * `/speckit.specify`
   * `/speckit.plan`
   * `/speckit.tasks`

> ใน ChatGPT ให้พิมพ์คำสั่งเหล่านี้ในแชต แล้วผมจะทำงานตาม spec-kit ให้

#

## 5. ใช้ Spec-Kit เป็นขั้น ๆ (สำหรับเคส ProductUI + ProductAPI)

### 5.1 ตั้งหลักการโปรเจกต์ (constitution)

ในแชต ChatGPT (ที่เปิดในโฟลเดอร์ `SpecKitDemo`) พิมพ์:

```text
/speckit.constitution
สร้างหลักการพัฒนาโปรเจกต์สำหรับระบบ CRUD Product
- Backend: C# .NET 8 WebAPI + Dapper + MSSQL Local
- Frontend: Next.js 15 + TypeScript + Pagination + Clean UI
- ต้องเน้น Clean Architecture, SOLID, Logging, Test
- รองรับการขยายเป็น Microservice ในอนาคต
```

AI จะสร้างเอกสารหลักการ (เหมือน guideline ของทีม) ลงไฟล์ให้

#

### 5.2 เขียนสเปกระบบ (spec.md) ด้วย `/speckit.specify`

ต่อด้วย:

```text
/speckit.specify
สร้างสเปกระบบ CRUD ProductData ประกอบด้วย
- Project ProductAPI (C# .NET 8 WebAPI + Dapper + MSSQL Local)
- Project ProductUI (Next.js 15 + TypeScript + Pagination + Search)
- ใช้ Clean Architecture (แยก API / Application / Domain / Infrastructure)
- มีฟีเจอร์: List, Create, Update, Delete, Pagination, Search, Validation
- เน้นให้เขียน User Story + Acceptance Criteria ชัด ๆ
```

ผลลัพธ์จะถูกเขียนลง `spec.md`
คุณควรเปิดอ่าน ปรับแก้ เพิ่มเงื่อนไขธุรกิจเองให้ตรงกับที่ต้องการ

#

### 5.3 สร้างแผนเทคนิค (plan.md) ด้วย `/speckit.plan`

เมื่อสเปกโอเคแล้ว ให้สร้างแผนเทคนิค:

```text
/speckit.plan
สร้างแผนเทคนิคสำหรับสเปก CRUD ProductData ด้านบน
- Backend: C# .NET 8, WebAPI, Dapper, MSSQL LocalDB, Clean Architecture
- Frontend: Next.js 15, App Router, TypeScript, Zustand/SWR สำหรับ State, Pagination
- โครงสร้างโฟลเดอร์ที่ต้องการ:
  - ProductAPI (API, Application, Domain, Infrastructure)
  - ProductUI (app/, components/, lib/)
- รวมทั้งแผนเรื่อง Logging, Error Handling, Config, และวิธีรันในเครื่อง
```

AI จะ generate **plan.md** ให้ เป็นเหมือน “Blueprint” วิธี implement

#

### 5.4 แตกงานย่อยเป็น Task (tasks.md) ด้วย `/speckit.tasks`

ต่อด้วย:

```text
/speckit.tasks
แตกงานจาก spec.md และ plan.md เป็น task ย่อย ๆ
- แยกส่วน ProductAPI และ ProductUI
- แต่ละ task ต้องเล็กพอ implement ใน 1-2 ชั่วโมง
- ใส่รายละเอียด acceptance criteria ต่อ task ให้ครบ
```

ระบบจะสร้าง `tasks.md` เช่น:

* Task 1: Setup ProductAPI solution structure
* Task 2: Create Product entity + repository
* Task 3: Implement GET /api/products with pagination
* Task 4: Setup ProductUI basic layout + fetch products
* ...

อันนี้คือ To-Do list ให้คุณทำตามทีละข้อ

#

## 6. ใช้ Spec-Kit ระหว่างลงมือโค้ด

เมื่อมี tasks.md แล้ว คุณทำงานตามลำดับ task และใช้ AI ช่วยเป็น “Dev คู่” เช่น

1. เลือก Task จาก `tasks.md`
2. คัดลอก Task นั้นไปถาม ChatGPT เช่น:

```text
ช่วย implement Task นี้:
[แปะข้อความ task จาก tasks.md]

ใช้เทคโนโลยีตาม plan.md ที่เราเขียนไว้
สร้างโค้ดสำหรับไฟล์ต่อไปนี้:
- ProductAPI/.../ProductsController.cs
- ProductAPI/.../ProductRepository.cs
- ProductAPI/.../DapperConnectionFactory.cs
```

3. นำโค้ดไปวางจริงใน VS / VS Code
4. รัน / แก้เทสต์ / ปรับตามจริง
5. ถ้า spec/plan เปลี่ยน ให้แก้ไฟล์ `spec.md` & `plan.md` ด้วย (spec เป็น source of truth)

#

## 7. ตรวจสุขภาพ Spec-Kit ด้วย `specify check`

เมื่อคุณมี spec/plan/tasks แล้ว สามารถให้ CLI ตรวจได้:

```powershell
specify check
```

หรือถ้าใช้ uvx:

```powershell
uvx --from git+https://github.com/github/spec-kit.git specify check
```

มันจะช่วยเช็คโครงสร้างไฟล์ของ Spec-Kit ว่าโอเคไหม

#
 

