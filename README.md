[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23573955&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student ID:** AI20K-dang1412
**Name:** Dang
**Date:** 2026-04-15

---

## Mo ta

Bai lab xay dung mot ETL Pipeline hoan chinh (Extract → Validate → Transform → Load) xu ly du lieu san pham tu file JSON. Pipeline loai bo cac ban ghi khong hop le (gia <= 0, category rong), ap dung chiet khau 10%, chuan hoa category ve Title Case, them timestamp va luu ket qua ra CSV. Ngoai ra bai lab con thuc hien Stress Test de danh gia anh huong cua chat luong du lieu den ket qua cua AI Agent.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas pytest
```

### Chay ETL Pipeline
```bash
python solution.py
```

Ket qua: file `processed_data.csv` duoc tao ra voi cac ban ghi da duoc lam sach va transform.

### Chay Agent Simulation (Stress Test)
```bash
# Buoc 1: Tao garbage data
python generate_garbage.py

# Buoc 2: Chay agent voi ca 2 bo du lieu
python agent_simulation.py
```

### Chay tests
```bash
pytest tests/test_autograder.py -v
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script (Extract, Validate, Transform, Load)
├── raw_data.json            # Du lieu nguon dau vao
├── processed_data.csv       # Output sau khi chay pipeline
├── garbage_data.csv         # Du lieu "rác" dung cho stress test
├── generate_garbage.py      # Script tao garbage data
├── agent_simulation.py      # Script mo phong AI Agent
├── experiment_report.md     # Bao cao ket qua stress test
└── README.md                # File nay
```

---

## Ket qua

- **Tong so records doc vao:** 5
- **Records hop le (giu lai):** 3 (Laptop, Chair, Monitor)
- **Records bi loai:** 2
  - Mystery Box: price = -10 (gia am → invalid)
  - Phone: category = "" (category rong → invalid)
- **Discounted price:** giam 10% so voi gia goc
- **Stress Test:** Agent cho ket qua chinh xac voi clean data (Laptop $1200), nhung tra loi sai voi garbage data (Nuclear Reactor $999,999 — outlier cuc doan)
