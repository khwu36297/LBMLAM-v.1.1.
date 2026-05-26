# LBMLAB v1.1 — Advanced Lattice Boltzmann Flow Simulator

[![Framework](https://img.shields.io/badge/Front--End-HTML5%20%2F%20CSS3%20%2F%20JavaScript-orange.svg)]()
[![Field](https://img.shields.io/badge/Domain-Computational%20Fluid%20Dynamics%20(CFD)-blueviolet.svg)]()

**LBMLAB v1.1** เป็นระบบจำลองการไหลของของไหลขั้นสูงแบบ Web-based Application ที่พัฒนาขึ้นโดยใช้วิธี **Lattice Boltzmann Method (LBM)** บนโมเดล **D2Q9-BGK** เพื่อขับเคลื่อนงานวิจัยทางด้านพลศาสตร์ของไหล (Fluid Dynamics) และช่วยลดต้นทุนด้านซอฟต์แวร์ลิขสิทธิ์ราคาแพงสำหรับภาคการศึกษา พัฒนาการวิจัย และผู้ประกอบการขนาดกลางและขนาดย่อม (SMEs)

โปรแกรมนี้ออกแบบมาให้ใช้งานได้ทันทีผ่าน Web Browser โดยไม่ต้องติดตั้ง (Zero-Installation) มีจุดเด่นด้านความแม่นยำสูงระดับอุตสาหกรรมด้วยการประเมินความคลาดเคลื่อนผ่าน Grid Convergence Index (GCI) และสอดคล้องกับผลเฉลยแม่นตรง (Analytical Solution) อย่างสมบูรณ์

---

## 🚀 Key Features (คุณสมบัติเด่น)

* **D2Q9 Lattice Boltzmann Solver:** คำนวณการไหลแบบ 2 มิติผ่านสมการขนส่งของ Boltzmann (Boltzmann Transport Equation) ที่มีความละเอียด 9 ทิศทางความเร็ว
* **Guo Forcing Scheme:** รองรับการใส่แรงขับเคลื่อนทางฟิสิกส์ (Body Force) ความละเอียดถูกต้องอันดับสอง (2nd-Order Accuracy) เหมาะสำหรับการจำลอง Pressure-driven Hydrodynamics เช่น Poiseuille Flow
* **Half-way Bounce-Back Boundary Condition:** ขอบเขตแบบไม่มีการลื่นไถล (No-slip Wall) ที่มีความแม่นยำระดับ $O(\Delta x^2)$
* **Real-time Visualization & Post-processing:** แสดงผลโครงสร้างการไหล (Velocity Profile) และการลดลงของค่าความคลาดเคลื่อน (Residuals Log) แบบ Real-time สูงสุดถึงระดับ $10^{-11}$
* **Rigorous Verification Toolkit:** ระบบตรวจวัดและทวนสอบความถูกต้องในตัว ประกอบด้วย:
    * การคำนวณ **$L_2$ Relative Error Norm** เทียบกับ Analytical Solution (ความแม่นยำสูงถึง 99.99%)
    * การประเมิน **Grid Convergence Index (GCI)** เพื่อตรวจสอบความเป็นอิสระของตารางคำนวณ (Grid Independence Study)
* **Data Export:** รองรับการส่งออกข้อมูลจำลองในรูปแบบ `.csv` เพื่อนำไปวิเคราะห์ต่อในโปรแกรมอื่น เช่น MATLAB, Python (Matplotlib) หรือ ParaView

---

## 📐 Mathematical & Physical Foundation

ระบบคำนวณถูกขับเคลื่อนด้วยสมการหลักของวิธี Lattice Boltzmann ภายใต้แบบจำลองเวลาผ่อนคลายเดี่ยว (Single-Relaxation-Time / BGK Model):

$$f_i(\mathbf{x} + \mathbf{e}_i\Delta t, t + \Delta t) = f_i(\mathbf{x}, t) - \frac{1}{\tau}\left[f_i(\mathbf{x}, t) - f_i^{eq}(\mathbf{x}, t)\right] + \Delta t F_i$$

โดยมีฟังก์ชันกระจายตัวสภาวะสมดุล (Equilibrium Distribution Function) คือ:

$$f_i^{eq} = w_i \rho \left[ 1 + \frac{\mathbf{e}_i \cdot \mathbf{u}}{c_s^2} + \frac{(\mathbf{e}_i \cdot \mathbf{u})^2}{2c_s^4} - \frac{\mathbf{u} \cdot \mathbf{u}}{2c_s^2} \right]$$

* **Lattice Structure:** D2Q9 ($\mathbf{e}_0$ ถึง $\mathbf{e}_8$) พร้อมความเร็วเสียงในโครงข่าย $c_s = 1/\sqrt{3}$
* **Forcing Implementation:** Guo Forcing Method ($F_i$) เพื่อรักษาความแม่นยำของพจน์ความหนืดและแรงภายนอกให้สอดคล้องกับสมการ Navier-Stokes

---

## 🛠️ Tech Stack & Architecture

โปรแกรมนี้ถูกสถาปัตยกรรมขึ้นมาภายใต้แนวคิด **High-Performance Web Computing** เพื่อให้คอมพิวเตอร์ทั่วไปสามารถประมวลผล CFD ได้ทันทีบน Browser:

* **Core Engine:** Pure Vanilla JavaScript (ES6+) คำนวณแบบสตรีมไลน์เพื่อประสิทธิภาพสูงสุด
* **UI/UX Framework:** Modern CSS พร้อมระบบธีมแบบ Futuristic/Cyberpunk (Space Mono & Syne Typeface) ออกแบบมาให้เป็นมิตรต่อผู้ใช้งาน (User-Centric Design)
* **Rendering:** HTML5 Canvas API สำหรับการพล็อต Velocity Profile แบบไดนามิกส์

---

## 📈 Verification Results (ผลการทวนสอบความถูกต้อง)

จากการทดสอบจำลอง **2D Poiseuille Flow (Streamwise-optimized grid)** ตัวโปรแกรมให้ผลลัพธ์ที่มีความน่าเชื่อถือสูง:
* **Convergence Status:** ลู่เข้าสู่สภาวะคงตัว (Steady State) ได้อย่างเด็ดขาดที่ Residual $< 10^{-11}$
* **Velocity Accuracy:** ค่าความเร็วสูงสุด ($U_{max}$) มีความนิ่งและตรงตามทฤษฎีที่ $0.05$
* **$L_2$ Error Norm:** ต่ำเพียง **0.0058%** (Excellent agreement) ยืนยันความถูกต้องของแนวคิดทางฟิสิกส์และการเขียนโปรแกรม

---

## 📂 Project Structure

```text
LBMLAB-v1.1/
├── index.html            # โค้ดอินเตอร์เฟสและซอฟต์แวร์คำนวณหลัก (All-in-one Web App)
└── README.md             # เอกสารอธิบายรายละเอียดโครงการ
