<!--
  โครงเปล่า — prose ทุกบรรทัดเป็นของ T เท่านั้น (กติกาเดียวกับ micrograd-from-scratch)
  วิธีใช้: อ่านคอมเมนต์ในแต่ละช่อง แล้วพูด(อังกฤษ)ทับคอมเมนต์นั้น ลบคอมเมนต์ทิ้ง
  ยังไม่ต้องเรียงจากบนลงล่าง — เริ่มจากช่องที่พูดได้คล่องที่สุดก่อน
  ยังไม่ต้องเขียนตอนนี้ก็ได้ เขียนตอนมีของให้เล่าแล้ว
-->

# makemore-from-scratch

<!-- 1 ประโยค: repo นี้คืออะไร. คนอ่านที่ตัดสินใจใน 5 วินาทีเห็นแค่บรรทัดนี้
     สิ่งที่ทำให้อันนี้ต่างจาก makemore fork เป็นพัน ๆ อัน คือประโยคเดียว: เขียนโดยไม่เปิดคลิป -->

<!-- one-liner ของ stack: PyTorch, N tests, ไม่มีบรรทัดไหนที่ก๊อปมา -->

---

<!-- ↓ รูปวางตรงนี้ ก่อนตัวหนังสือใดๆ ทั้งสิ้น
     ตัวที่แรงที่สุดสำหรับเดือนนี้คือ histogram ของ activation ก่อน/หลังแก้ init
     — รูปที่เห็นแล้วรู้ทันทีว่าอะไรพัง คือรูปที่ recruiter หยุดดู -->

![activation histograms](docs/activations.png)

<!-- caption 1 บรรทัด: ซ้ายคืออะไร ขวาคืออะไร แล้วเปลี่ยนอะไรระหว่างสองรูป -->

---

## Why this repo exists

<!-- 3-4 ประโยค ไม่เกินนี้
     - M1 คือดูคลิปแล้วพิมพ์ตาม / M2 คือปิดคลิปแล้วเขียน — บอกความต่างนี้ตรง ๆ
     - ทำไมถึงคุ้มที่จะอ่าน: มันบันทึกว่าตอนไม่มีคลิปแล้วพังตรงไหนบ้าง
     - ห้ามมีย่อหน้าอธิบายว่า language model คืออะไร ← ย้ายไป learning site -->

## The problem this month: a model that trains but does not learn

<!-- ประโยคที่คมที่สุดใน README ทั้งไฟล์ — เขียนตอนเจอของจริงแล้ว
     ธีมของ Part 3: loss ลง แต่ลงช้าผิดปกติ แล้วสาเหตุมองไม่เห็นจาก loss
     ต้องไปดู histogram ของ activation กับ gradient ถึงจะเห็น
     ใส่ตัวเลขจริงจากรันของตัวเอง ไม่ใช่ตัวเลขจากคลิป -->

## What is in here

<!-- ตารางสั้น อัปเดตเรื่อย ๆ ไม่ต้องเขียนล่วงหน้า -->

| part | code | contract | status |
|---|---|---|---|
| bigram (retype from empty) | | | ยังไม่เริ่ม |
| MLP (Bengio 2003) | | | ยังไม่เริ่ม |
| activations / init / BatchNorm | | | ยังไม่เริ่ม |
| manual backprop | | | ยังไม่เริ่ม |
| WaveNet | | | ยังไม่เริ่ม |

## The bugs worth reading

<!-- ส่วนที่มีค่าที่สุดของ repo ในสายตาคนอ่าน — bug จริงที่เจอเอง ไม่ใช่โค้ดที่ทำงานได้
     ลิงก์ไป learning/lessons/ -->

## Running it

One venv, two platforms. The only real difference is where the venv puts its
binaries: `.venv/bin/` on macOS and Linux, `.venv/Scripts/` on Windows.

**macOS / Linux**

```bash
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/python -m pytest -x
```

**Windows (PowerShell or cmd)**

```bash
python -m venv .venv
.venv/Scripts/python.exe -m pip install -r requirements.txt
.venv/Scripts/python.exe -m pytest -x
```

Calling the venv's interpreter by path means no `activate` step and no way to
install into the system Python by accident. If you would rather activate it,
`source .venv/bin/activate` (macOS/Linux) or `.venv\Scripts\Activate.ps1`
(PowerShell) — after that plain `python` and `pytest` are the venv's.

For the notebook, register the venv as a kernel once, then pick
`makemore` in the Jupyter/VS Code kernel picker:

```bash
.venv/bin/python -m ipykernel install --user --name makemore   # Windows: .venv/Scripts/python.exe
```

Notes:

- `requirements.txt` is a pinned freeze. The pins resolve on both platforms —
  `torch==2.13.0` has wheels for Windows x86-64 and macOS arm64 alike, so the
  same file works untouched.
- On Apple Silicon, `torch.backends.mps.is_available()` is `True`. Nothing here
  needs it — the models are small enough to stay on CPU — but a `.to("mps")`
  is there if a run gets slow.
- `pytest` exits with code 5 and "no tests ran" until `tests/` has something in
  it. That is the expected state of a repo that starts empty.

## Where this sits

<!-- 2 ประโยค: M2 ของ roadmap 17 เดือน · ก่อนหน้าคือ micrograd-from-scratch · ถัดไปคือ nanoGPT
     ไม่ต้องอธิบายทั้งระบบ ลิงก์พอ -->

- ก่อนหน้า: [`micrograd-from-scratch`](../micrograd-from-scratch) — M1, ปิดแล้ว
