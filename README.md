# Claude

Personal Claude Code setup — configs, agents, and prompts I reuse across projects.

## Personal Advisory Board — 5 Agents

บอร์ดที่ปรึกษาส่วนตัว 5 agent สำหรับ Claude Code (subagents) พร้อมเวอร์ชัน portable prompt ใช้ที่ไหนก็ได้

### สมาชิกบอร์ด (5 agent)

| Agent | ไฟล์ | หน้าที่หลัก |
|---|---|---|
| นักวิเคราะห์เศรษฐกิจและการลงทุน | `agents/finance-analyst.md` | ติดตามข่าว วิเคราะห์เศรษฐกิจ/การลงทุน |
| FIRE Planner | `agents/fire-planner.md` | วางแผน financial freedom & early retirement |
| นักเขียนบทความการแพทย์ | `agents/medical-writer.md` | เขียนคอนเทนต์สุขภาพเข้าใจง่าย |
| Healthcare Data & Strategy Analyst | `agents/healthcare-strategist.md` | วิเคราะห์ข้อมูล & กลยุทธ์โรงพยาบาลเอกชน กทม |
| Side-Project & Income Coach | `agents/side-project-coach.md` | คิด/ประเมินโปรเจกต์หารายได้เสริม |

### วิธีติดตั้งใน Claude Code (ใช้ได้ทุกโปรเจกต์)

Subagent ระดับ **user** (global) จะใช้งานได้จากทุกโปรเจกต์ที่เปิด Claude Code บนเครื่องเดียวกัน — เหมาะกับกรณีนี้เพราะบอร์ดเป็นเรื่องส่วนตัว ไม่ผูกกับโปรเจกต์ใดโปรเจกต์หนึ่ง

```bash
git clone https://github.com/theantares/claude.git ~/claude-config
mkdir -p ~/.claude/agents
cp ~/claude-config/agents/*.md ~/.claude/agents/
```

หรือถ้าอยาก sync ทุกครั้งที่อัปเดต repo นี้ ให้ทำ symlink แทนการ copy:

```bash
mkdir -p ~/.claude/agents
ln -sf ~/claude-config/agents/*.md ~/.claude/agents/
```

จากนั้นในเซสชัน Claude Code ใด ๆ (โปรเจกต์ไหนก็ได้) เรียกใช้ได้ทันที เช่น:

```
ใช้ finance-analyst ช่วยสรุปข่าวเศรษฐกิจไทยสัปดาห์นี้
```

หรือให้ Claude เรียกหลาย agent พร้อมกันแล้วสรุปให้ (โหมด "ประชุมบอร์ด"):

```
เรียกทั้ง 5 agent ในบอร์ดมาช่วยดูเรื่อง [สถานการณ์/คำถามของคุณ] แต่ละคนวิเคราะห์อิสระ
แล้วสรุปจุดร่วม-จุดที่เห็นต่างให้ฉันตัดสินใจเอง
```

### วิธีใช้แบบ portable (ChatGPT, Claude.ai, ที่ไหนก็ได้)

ดูไฟล์ [`portable-prompts.md`](./portable-prompts.md) — copy system prompt ของแต่ละ agent ไปวางเป็น custom instruction / system prompt ในแชทแยกกัน 5 แชท แล้วถามคำถามเดียวกันในแต่ละแชท

### วิธีใช้บอร์ดให้ได้ประโยชน์สูงสุด

1. **ตั้งคำถาม/สถานการณ์ให้เจาะจง** พร้อมบริบทจริง (ตัวเลข ข้อจำกัด เป้าหมาย) — ยิ่งให้ context เยอะ คำตอบยิ่งใช้งานได้จริง
2. **ให้แต่ละ agent วิเคราะห์แยกกันก่อน** อย่าเพิ่งให้เห็นคำตอบของกันและกัน จะได้มุมมองที่ไม่ถูกครอบงำ
3. **คุณ (หรือ Claude หลัก) เป็นประธานบอร์ด** สรุปจุดร่วม/จุดขัดแย้ง แล้วตัดสินใจเอง — บอร์ดให้ input ไม่ใช่ตัดสินใจแทน
4. **ทบทวนเป็นรอบ** เช่น finance-analyst + fire-planner คุยกันทุกเดือน, medical-writer ใช้ตอนมีโปรเจกต์คอนเทนต์, healthcare-strategist ใช้ตอนวางแผนไตรมาส/ปี, side-project-coach ใช้ตอนมีเวลาว่าง/อยากเริ่มของใหม่
5. **ปรับ system prompt ได้เสมอ** — ไฟล์เหล่านี้เป็นจุดเริ่มต้นที่ดี ปรับให้เข้ากับสถานการณ์จริงมากขึ้นเรื่อย ๆ เมื่อรู้ว่าอะไรได้ผล/ไม่ได้ผล

### ข้อควรระวังร่วมกันทุก agent

- ทุก agent เตือนไว้แล้วว่าไม่ใช่คำแนะนำทางการเงิน/การแพทย์/กฎหมายที่เป็นทางการ 100% — ใช้ประกอบการตัดสินใจ เรื่องสำคัญมาก (ภาษี, การรักษา, การลงทุนก้อนใหญ่) ควรปรึกษาผู้เชี่ยวชาญที่มีใบอนุญาตควบคู่ไปด้วย
- agent ที่ต้องค้นข้อมูลสด (ข่าว, ตลาด) ต้องมี WebSearch/WebFetch เปิดใช้งานในเซสชันนั้น ๆ
