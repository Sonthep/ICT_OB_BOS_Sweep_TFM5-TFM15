# 🚀 ICT Smart Money EA v3.0

## 📋 **ภาพรวม**
Expert Advisor สำหรับ MetaTrader 5 ที่ใช้แนวทาง **Smart Money Concept (ICT Style)** สำหรับเทรดอัตโนมัติ โดยใช้การวิเคราะห์ **Liquidity Sweep**, **Break of Structure (BOS)**, และ **Order Block** เพื่อหาจุดเข้าออเดอร์ที่มีความแม่นยำสูง

## ✨ **คุณสมบัติหลัก**

### 🎯 **ICT Strategy Logic**
- **Liquidity Sweep Detection**: ตรวจจับการ False Breakout ของ Swing High/Low
- **Break of Structure (BOS)**: วิเคราะห์การเบรกโครงสร้างในทิศทางตรงข้าม
- **Order Block Identification**: หา Order Block ล่าสุดที่ยังไม่ถูกแตะ
- **Limit Entry**: ใช้ Buy/Sell Limit ที่ Order Block แทนการ Market Entry

### ⏰ **Killzone Management**
- **London Killzone**: 14:00-17:00 (เวลาไทย)
- **New York Killzone**: 19:30-23:00 (เวลาไทย)
- **Timezone Support**: รองรับ GMT+7 (เวลาไทย) และปรับได้
- **Session Filter**: สามารถเปิด/ปิดการกรองเวลาได้

### 💰 **Risk & Money Management**
- **Risk per Trade**: กำหนดเปอร์เซ็นต์ความเสี่ยงต่อเทรด (Default: 1%)
- **Risk:Reward Ratio**: ตั้งค่า RR ได้ (Default: 1:2)
- **Partial Take Profit**: ปิด 50% ที่ 1:1 RR, ที่เหลือที่ 1:2 RR
- **Break-even**: ย้าย SL ไป BE หลังจาก TP1 hit
- **Daily Trade Limit**: จำกัดจำนวนเทรดต่อวัน (Default: 2 เทรด)

### 📊 **Visual Dashboard**
- **Statistics Panel**: แสดงสถิติการเทรด, Win Rate, Profit Factor
- **Killzone Status**: แสดงสถานะ Killzone แบบ Real-time
- **Signal Status**: แสดงสถานะ Sweep, BOS, Order Block
- **Position Info**: แสดงข้อมูล Position ปัจจุบันและ RR

### 🎨 **Chart Visualization**
- **Order Block Drawing**: วาด Order Block บนชาร์ต
- **Sweep Markers**: แสดงจุด Liquidity Sweep
- **BOS Lines**: เส้น Break of Structure
- **Color Coding**: สีเขียวสำหรับ Bullish, สีแดงสำหรับ Bearish

## ⚙️ **การตั้งค่า**

### 📈 **ICT Strategy Settings**
```
RiskPercent = 1.0          // ความเสี่ยงต่อเทรด (%)
SwingLookback = 5          // จำนวนแท่งสำหรับหา Swing High/Low
BOS_Lookback = 20          // จำนวนแท่งสำหรับตรวจ BOS
SL_Buffer = 30             // Buffer สำหรับ SL (3 pips)
RR_Ratio = 2.0             // อัตราส่วน Risk:Reward
EnablePartialTP = true     // เปิดใช้ Partial TP
```

### 🕐 **Killzone Settings**
```
UseLondonKZ = true         // ใช้ London Killzone
UseNYKZ = true             // ใช้ NY Killzone
TimezoneOffset = 7         // เวลาไทย GMT+7
```

### 🛡️ **Risk Management**
```
MaxTradesPerDay = 2        // เทรดสูงสุดต่อวัน
MaxOrdersPerSymbol = 1     // Order สูงสุดต่อ Symbol
EnableTradeManagement = true // เปิดใช้ Break-even & Trailing
```

### 🎨 **Display Settings**
```
ShowKillzoneStatus = true  // แสดงสถานะ Killzone
ShowOrderBlocks = true     // วาด Order Blocks
ShowSweepMarkers = true    // แสดง Sweep markers
ShowBOSLines = true        // แสดงเส้น BOS
ShowStats = true           // แสดง Statistics panel
```

## 🔄 **Logic การทำงาน**

### 1️⃣ **Liquidity Sweep Detection**
```
- ตรวจจับการเบรก Swing High/Low ใน 3-5 แท่งล่าสุด
- ราคาต้องกลับเข้ามาในกรอบ (False Breakout)
- กำหนดทิศทางของ Setup (Bullish/Bearish)
```

### 2️⃣ **Break of Structure (BOS)**
```
- หลังจาก Sweep แล้ว ตรวจหา BOS ในทิศทางตรงข้าม
- Bullish Setup: เบรกเหนือ High ก่อนหน้า
- Bearish Setup: เบรกใต้ Low ก่อนหน้า
```

### 3️⃣ **Order Block Identification**
```
- หาแท่งเทียนตรงข้ามก่อน BOS
- Bullish Setup: หา Bearish Candle (Order Block)
- Bearish Setup: หา Bullish Candle (Order Block)
```

### 4️⃣ **Entry Execution**
```
- วาง Buy/Sell Limit ที่กลาง Order Block
- SL: หลัง Order Block + Buffer
- TP: ใช้ Risk:Reward Ratio ที่กำหนด
```

### 5️⃣ **Trade Management**
```
- TP1 (1:1 RR): ปิด 50% + ย้าย SL ไป Break-even
- TP2 (1:2 RR): ปิดที่เหลือทั้งหมด
- Auto Statistics Update
```

## 📁 **ไฟล์ที่เกี่ยวข้อง**

```
ICT_SmartMoney_EA.mq5      // EA หลัก
├── SimpleSession.mqh       // จัดการ Killzone (เวลาไทย)
├── RiskManager.mqh         // จัดการความเสี่ยงและ Lot Size
├── LimitOrderManager.mqh   // จัดการ Limit Orders
├── PartialTPManager.mqh    // จัดการ Partial Take Profit
└── DrawUtils.mqh          // วาดกราฟิกบนชาร์ต
```

## 🚀 **การติดตั้งและใช้งาน**

### 1. **การติดตั้ง**
```
1. Copy ไฟล์ทั้งหมดไปยัง MQL5/Experts/
2. Compile ICT_SmartMoney_EA.mq5
3. Attach EA ลงบนชาร์ต M5 หรือ M15
4. ตั้งค่าตามต้องการ
5. เปิด Auto Trading
```

### 2. **Timeframe ที่แนะนำ**
- **M5**: สำหรับ Scalping และ Entry ที่แม่นยำ
- **M15**: สำหรับ Swing Trading และ Filter

### 3. **Symbol ที่เหมาะสม**
- **Major Pairs**: EURUSD, GBPUSD, USDJPY, AUDUSD
- **Gold**: XAUUSD (ปรับ SL_Buffer เป็น 300-500)
- **Indices**: US30, NAS100, SPX500

## 📊 **การอ่าน Dashboard**

### **Statistics Panel (ซ้ายบน)**
```
ICT Smart Money EA v3.0
═══════════════════════
Symbol: EURUSD
Total Trades: 15
Win Rate: 73.3%
Wins: 11 | Loss: 4
Profit Factor: 2.45
Risk per Trade: 1.0%
RR Ratio: 2.0:1
═══════════════════════
Signals Status:
Sweep: ✓
BOS: ✓
OB Ready: ✗
═══════════════════════
Pos: BUY | RR: 1.2 | P/L: 45.30 | Active
```

### **Killzone Panel (ขวาบน)**
```
KILLZONE STATUS
Thai Time: 15:30
London: ACTIVE
NY: CLOSED
Trading: ALLOWED
```

## ⚠️ **ข้อควรระวัง**

### 🔴 **Risk Management**
- ตั้งค่า Risk ไม่เกิน 1-2% ต่อเทรด
- ใช้ Stop Loss เสมอ
- ไม่ควรเทรดในช่วง News ที่มี Impact สูง

### 🔴 **Market Conditions**
- EA ทำงานดีในตลาดที่มี Trend และ Structure ชัดเจน
- หลีกเลี่ยงการใช้ในตลาด Sideways หรือ Low Volatility
- ระวังช่วง Holiday และ Low Liquidity

### 🔴 **Broker Requirements**
- Spread ต่ำ (< 2 pips สำหรับ Major Pairs)
- Execution Speed ดี
- รองรับ Partial Position Close
- ไม่มี Restrictions สำหรับ EA Trading

## 🔧 **การปรับแต่งขั้นสูง**

### **สำหรับ Gold (XAUUSD)**
```
SL_Buffer = 500           // 50 pips สำหรับ Gold
RR_Ratio = 1.5            // RR ต่ำกว่าเพราะ Volatility สูง
SwingLookback = 3         // ลดลงเพราะ Gold เคลื่อนไหวเร็ว
```

### **สำหรับ Indices**
```
SL_Buffer = 100           // 10 points สำหรับ US30
RR_Ratio = 2.5            // RR สูงกว่าเพราะ Trend ชัดเจน
BOS_Lookback = 30         // เพิ่มขึ้นเพราะ Timeframe ใหญ่
```

### **สำหรับ Scalping (M1-M5)**
```
SwingLookback = 3         // ลดลงสำหรับ Entry เร็ว
MaxTradesPerDay = 5       // เพิ่มจำนวนเทรด
EnablePartialTP = false   // ปิด Partial TP สำหรับ Quick Exit
```

## 📞 **การสนับสนุน**

หากมีปัญหาหรือข้อสงสัย:
1. ตรวจสอบ Log ใน Experts Tab
2. ตรวจสอบการตั้งค่า Broker
3. ทดสอบใน Strategy Tester ก่อน
4. อ่าน Error Messages ใน Log

---

## 🎯 **เป้าหมายของ EA**

EA นี้ถูกออกแบบมาเพื่อ:
- ✅ ลดการเทรดด้วยอารมณ์
- ✅ เพิ่มความสม่ำเสมอในการเทรด
- ✅ ใช้หลักการ Smart Money Concept อย่างเป็นระบบ
- ✅ จัดการความเสี่ยงอย่างมีประสิทธิภาพ
- ✅ สร้างผลตอบแทนที่สม่ำเสมอในระยะยาว

**Happy Trading! 🚀📈** 