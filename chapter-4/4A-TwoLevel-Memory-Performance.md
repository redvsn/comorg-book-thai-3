
```markdown
# Appendix 4A: Two-Level Memory Performance

## สูตรคำนวณ Effective Access Time

```
EAT = h×t1 + (1-h)×(t1 + t2)
h = Hit ratio
t1 = Cache access time
t2 = Main memory access time
ตัวอย่างคำนวณ
h = 0.95, t1 = 0.01ms, t2 = 0.1ms
EAT = 0.95×0.01 + 0.05×(0.01+0.1)
    = 0.0095 + 0.0055 = 0.015ms ✓
Hit Ratio vs Performance
Hit Ratio 90% → EAT ใกล้ t1
Hit Ratio 50% → EAT ใกล้ t2
