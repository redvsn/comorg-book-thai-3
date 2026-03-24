# 8.6 Design Issues for Paging Systems

**ประเด็นการออกแบบระบบ Paging** - การตัดสินใจสำคัญที่กระทบ Performance และ Complexity

---

## 🎯 **6 Design Issues หลัก**
Page Size → Performance vs Management

Page Tables → Size vs Speed

TLB Design → Hit Rate vs Size

Page Replacement → Optimal vs Practical

Frame Allocation → Global vs Local

Thrashing → Prevention Mechanisms

---

## 📏 **1. Page Size**

### **Trade-offs**
Page Size ↑ Page Size ↓
✅ TLB Coverage ↑ ✅ No Internal Frag
✅ TLB Miss ↓ ❌ Internal Frag ↑
✅ Page Fault ↓ ❌ Page Table ใหญ่
✅ Transfer Time ↑ ❌ Transfer Time ↓

### **Optimal Size**
Common: 4KB-64KB
Modern: 4KB (default) + 2MB (THP)
x86-64: Supports 4KB, 2MB, 1GB

**กราฟ**:
Page Fault Rate
│
↓ │ Optimal
─────┼─────→ Page Size
Internal Frag ↑

---

## 📋 **2. Page Table Structure**

### **Problem: Large Virtual Space**
32-bit: 4GB → 1M PTE × 4B = 4MB
64-bit: 2^48 → 256TB Page Table!

### **Solutions**

#### **A. Multi-level Page Tables**
x86-64 (4-Level):
PML4(9b) → PDPT(9b) → PD(9b) → PT(9b) + Offset(12b)
Total Resident: 4KB/Page เท่านั้น!

Access 0x123456789ABC:
PML4 → PDPT → PD → PT → Frame + 0x5ABC

#### **B. Inverted Page Tables**
1 Entry/Frame แทน 1 Entry/Page
32-bit, 1M Pages, 4GB RAM → 1M vs 4M Entries

---

## 🚀 **3. TLB Design**

### **Fully Associative TLB**
Size: 32-256 entries
Hit Rate: 95-99%
Access: Parallel Tag Compare

### **Split TLB**
ITLB (Instruction) + DTLB (Data)
Dual Port → No Contention

### **Modern Features**
ASID (Process ID) → No Flush Context Switch

Huge Page Support (2MB/1GB)

Variable Page Size TLB

---

## 🔄 **4. Page Replacement Policy**

| **Policy** | **Pros** | **Cons** | **Use** |
|------------|----------|----------|---------|
| **FIFO** | Simple | **Belady Anomaly** | Rare |
| **LRU** | Optimal | **Hardware Complex** | Servers |
| **Clock** | **Simple + Good** | Not Perfect | **Linux** |
| **Clock-Pro** | **Adaptive** | Complex | **Modern Linux** |

**Linux Clock-Pro**:
---

## 🔄 **4. Page Replacement Policy**

| **Policy** | **Pros** | **Cons** | **Use** |
|------------|----------|----------|---------|
| **FIFO** | Simple | **Belady Anomaly** | Rare |
| **LRU** | Optimal | **Hardware Complex** | Servers |
| **Clock** | **Simple + Good** | Not Perfect | **Linux** |
| **Clock-Pro** | **Adaptive** | Complex | **Modern Linux** |

**Linux Clock-Pro**:
Uses R + M + Age Bits
Cold Pages (R=0 นาน) → Evict First

---

## 🎯 **5. Frame Allocation**

### **Global vs Local Replacement**
Global: Fault A → Replace Any Process
Local: Fault A → Replace A's Pages Only

| **Global** | **Local (Working Set)** |
|------------|------------------------|
| **Simple** | **Fair** |
| **Interference** | Isolation |
| **Good Avg** | Predictable |

**Hybrid**: Per-Process LRU Lists

---

## 🛡️ **6. Thrashing Control**

### **Working Set Monitor**
WS(τ) = Pages ใน Window τ instructions
Allocate: |WS| + α frames

### **Page Fault Frequency (PFF)**
PFF > Threshold → Suspend Process

### **System Monitor**
Total Fault Rate ↑ → ลด Multiprogramming

---

## 📊 **Page Size Selection**
Page Size Matrix:
Internal Fragmentation
Large Low High Fault Rate
Optimal Optimal Optimal
Small High Low Fault Rate

Page Fault Rate
│
─────┼─────→ Page Size ───────┐
Internal Frag ↑ │
Optimal ~8KB

---

## 🔮 **Modern Design (2026)**
Page Size: 4KB + 2MB THP (Auto)
Page Table: 5-Level (Intel) / 4-Level (AMD)
TLB: 64-entry DTLB + 32-entry ITLB
Replacement: Clock-Pro (Linux)
Allocation: Per-Process LRU
Thrashing: PSI (Pressure Stall Info)

**Intel PSI**: 
Memory Pressure Metric
Applications Auto Slow Down

---

## 🎯 **สรุป 8.6 Design Issues**
🏆 Key Decisions:
├── Page Size: 4-64KB (4KB+2MB Modern)
├── Page Table: Multi-level (4-5 Levels)
├── TLB: Fully-Assoc 32-256 entries
├── Replacement: Clock-Pro (Practical)
├── Allocation: Per-Process LRU
└── Thrashing: WS + PFF Monitor

"Balance Complexity vs Performance!"

**เป้าหมาย**: **High Performance + Low Overhead** [file:11]
