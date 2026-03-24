```markdown
# 4.3 Elements of Cache Design

## องค์ประกอบหลัก (Table 4.2)

| **Element** | **Options** |
|-------------|-------------|
| Cache Addresses | Logical/Physical |
| Cache Size | 8KB-หลายMB |
| **Mapping** | Direct/Associative/Set-Associative |
| **Replacement** | LRU/FIFO/LFU/Random |
| **Write Policy** | Write-through/Write-back |
| Line Size | 32-256 bits |
| # Caches | L1/L2/L3 |

## 1. Mapping Functions

### Direct Mapping
```
i = j mod m
Block j → Line เดียว
Pros: ง่าย ถูก
Cons: Conflict Miss เยอะ

Fully Associative
Block j → ทุก Line
Pros: ยืดหยุ่น
Cons: Hardware ซับซ้อน

Set-Associative (แนะนำ)

2. Replacement Algorithms
i = j mod v, Set i มี k lines
2-way/4-way = สมดุลดีที่สุด
| LRU            | FIFO         | LFU        | Random |
| -------------- | ------------ | ---------- | ------ |
| ไม่ใช้มานานสุด | เข้ามานานสุด | ใช้น้อยสุด | สุ่ม   |
3. Write Policies
| Write-through | Write-back     |
| ------------- | -------------- |
| Cache + MM    | Cache เท่านั้น |
| ปลอดภัย       | เร็ว           |
| ช้า           | ใช้ Dirty Bit  |