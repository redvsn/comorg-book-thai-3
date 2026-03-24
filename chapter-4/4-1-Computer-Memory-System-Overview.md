
```markdown
# 4.2 Cache Memory Principles

## แนวคิดพื้นฐาน

```
CPU ──[Cache: เล็ก+เร็ว]── Main Memory: ใหญ่+ช้า
         ↑ Copy ของ MM
Cache Operations
| Hit                   | Miss                          |
| --------------------- | ----------------------------- |
| พบใน Cache → ส่งทันที | ไม่พบ → โหลด Block จาก MM     |
| ใช้เวลา: T_cache      | ใช้เวลา: T_cache + T_transfer |
โครงสร้าง Cache
Cache Line = [Tag][K words][Control Bits]
Main Memory = M blocks (M >> m cache lines)
Cache Read Flow
flowchart TD
    A[CPU Address] --> B{Check Tag?}
    B -->|Match| C[Return Data]
    B -->|No Match| D[Fetch Block from MM]
    D --> E[Update Cache]
    E --> C
Hit Ratio สูง จาก Locality Principle

