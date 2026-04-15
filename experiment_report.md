# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600023
**Name:** Dang Thanh Tung
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Based on my data, the best choice is Laptop at $1200." | 10 | Correct — Laptop la san pham electronics dat nhat trong du lieu sach |
| Garbage Data (`garbage_data.csv`) | "Based on my data, the best choice is Nuclear Reactor at $999999." | 1 | Sai — Nuclear Reactor la outlier voi gia 999,999 USD, khong phai san pham thuc te |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi su dung garbage data, Agent tra lai ket qua sai hoan toan vi cac van de chat luong du lieu sau:

**Extreme Outlier (gia tri bat thuong):** Ban ghi "Nuclear Reactor" co gia 999,999 USD — mot gia tri bat hop ly va khong co thuc trong thuc te. Agent su dung logic chon san pham co gia cao nhat trong danh muc "electronics", nen no luon chon san pham nay. Du lieu sach da loai bo cac outlier nhu vay ngay tu buoc Validate.

**Duplicate IDs:** Garbage data co hai ban ghi voi id = 1 (Laptop va Banana). Dieu nay gay nham lan khi truy vet nguon goc du lieu, va co the dan den tinh toan sai neu logic phu thuoc vao ID duy nhat.

**Wrong Data Types:** Ban ghi "Broken Chair" co truong price la chuoi "ten dollars" thay vi so. Neu Agent co xu ly tinh toan so hoc tren truong nay, se xay ra loi kieu du lieu (TypeError), khien Agent crash hoac tra loi sai.

**Null Values:** Ban ghi "Ghost Item" co id = None va category = None. Nhung gia tri null nay co the vuot qua bo loc neu Validate khong duoc viet chat, va gay ra loi khi Agent co tinh toan tren chung.

Ket qua cho thay du lieu chat luong thap truc tiep dan den phan tich sai, khuyen nghi sai, va mat tin nhiem vao he thong AI.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Dong y hoan toan.

Du cho prompt co tot den dau, neu du lieu dau vao chua nhieu loi (outlier, null, sai kieu), AI Agent se cho ra ket qua sai va thieu tin cay. Buoc ETL Validate la lop bao ve quan trong nhat — no loai bo nhung "bom hua hen" truoc khi chung anh huong den ket qua cua Agent. Trong thuc te, cham soc du lieu (data quality) can duoc uu tien truoc khi toi uu hoa prompt hay mo hinh.
