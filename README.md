# ERPNext Vietnam — erpnextvn

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![ERPNext v16](https://img.shields.io/badge/ERPNext-v16-green.svg)](https://erpnext.com)
[![Frappe v16](https://img.shields.io/badge/Frappe-v16-green.svg)](https://frappeframework.com)

**Vietnamese Localization for ERPNext v16** — Kế toán, thuế, hóa đơn điện tử, lương, dịch thuật theo chuẩn Việt Nam.

---

## 🇬🇧 English

`erpnextvn` is a comprehensive Vietnamese localization pack for ERPNext v16 / Frappe v16. It ships:

- **Chart of Accounts** — **TT99/2025/TT-BTC (new, effective 01/01/2026)**, TT200/2014/TT-BTC (legacy), and TT133/2016/TT-BTC (SME)
- **VAT templates** — 0% / 5% / 8% / 10% Sales & Purchase
- **Payroll** — Personal Income Tax (7-bracket progressive, new deductions per Nghị quyết 110/2025/UBTVQH15 effective 2026), BHXH / BHYT / BHTN
- **E-Invoicing** — Viettel S-Invoice, VNPT, MISA meInvoice, FPT, BKAV
- **Print Formats** — 8 standard Vietnamese forms (Hóa đơn, Phiếu thu/chi/xuất/nhập, Báo giá, PO, Phiếu lương)
- **Reports** — Bảng lương tháng, Báo cáo TNCN, Bảng kê hóa đơn, Sổ cái, Cân đối phát sinh
- **Translation** — 500+ Vietnamese terms
- **63 provinces** fixture with wage region mapping (I–IV)

## 🇻🇳 Tiếng Việt

`erpnextvn` là bộ bản địa hóa đầy đủ cho ERPNext v16 / Frappe v16 theo chuẩn Việt Nam:

- **Hệ thống tài khoản** — **TT99/2025/TT-BTC (mới nhất, hiệu lực 01/01/2026)**, Thông tư 200 (cũ), và Thông tư 133 (SME)
- **Mẫu thuế GTGT** — 0% / 5% / 8% / 10% cho hóa đơn bán/mua
- **Tiền lương** — Thuế TNCN bậc thang 7 bậc (giảm trừ mới theo NQ 110/2025/UBTVQH15 áp dụng từ 2026), BHXH / BHYT / BHTN
- **Hóa đơn điện tử** — Tích hợp 5 nhà cung cấp lớn (Viettel, VNPT, MISA, FPT, BKAV)
- **Mẫu in** — 8 mẫu chuẩn Việt Nam
- **Báo cáo** — 5 báo cáo theo chuẩn kế toán VN
- **Dịch tiếng Việt** — 500+ thuật ngữ
- **63 tỉnh/thành** — Kèm vùng lương tối thiểu (I–IV)

---

## 📋 Chart of Accounts — TT99/2025 (mới nhất)

Thông tư 99/2025/TT-BTC ban hành 27/10/2025, hiệu lực **01/01/2026**, thay thế Thông tư 200/2014/TT-BTC. App mặc định load TT99 cho công ty mới.

### Thay đổi chính so với TT200

**Tài khoản đổi tên:**
- `112` Tiền gửi Ngân hàng → **Tiền gửi không kỳ hạn**
- `155` Thành phẩm → **Sản phẩm**
- `242` Chi phí trả trước → **Chi phí trả sau**
- `4112` Thặng dư vốn cổ phần → **Thặng dư vốn**

**Tài khoản bỏ:** 161 (Chi sự nghiệp), 441 (Vốn đầu tư XDCB), 461 (Nguồn KP sự nghiệp), 466 (KP hình thành TSCĐ), 611 (Mua hàng), 623 (CP máy thi công), 631 (Giá thành SX), 212/217 gộp vào 211, 337/343/347/356 bỏ.

**Tài khoản mới thêm:**
- `215` — **Tài sản sinh học** (biological assets) với 2151/2152/2153
- `332` — **Phải trả cổ tức, lợi nhuận**
- `6275` — Thuế, phí, lệ phí (con của 627)
- `6415` — Chi phí bảo hành (con của 641)
- `82112` — **Chi phí thuế TNDN bổ sung theo thuế tối thiểu toàn cầu (Pillar Two)**

**Báo cáo tài chính:** "Bảng cân đối kế toán" → **"Báo cáo tình hình tài chính"**

**Linh hoạt:** TT99 cho phép doanh nghiệp tự bổ sung/sửa tài khoản mà **không cần xin Bộ Tài chính** (quy định cũ TT200).

## 📦 Installation

```bash
# On your Frappe bench
cd frappe-bench
bench get-app https://github.com/mrhuychien/erpnextvn
bench --site [your-site] install-app erpnextvn
bench --site [your-site] migrate
```

After installation:

1. Open ERPNext → **Setup Wizard** → select country **Vietnam**
2. Go to **VN Payroll Settings** and verify statutory values
3. Go to **VN E Invoice Settings** and configure your HĐĐT provider (if used)
4. Open **VN Province** to confirm 63 provinces loaded

### Language

Installing enables the `vi` Language record. Frappe ships it **disabled**
(`frappe/geo/languages.csv` carries `vi,Tiếng Việt,0`) and
`translate.get_all_languages()` — which fills the language pickers — lists only
enabled ones, so without this step the translations load but Vietnamese never
appears in *System Settings → Language*.

The Setup Wizard path additionally sets the site language to `vi` outright. On a
site that skipped the wizard, pick it yourself in *System Settings → Language* —
search for **`Tiếng Việt`** or **`vi`**, since the record is named `vi` and
titled by `language_name`; searching "Vietnamese" finds nothing. Then
`bench --site [your-site] clear-cache`, `bench restart`, and hard-refresh
(`Ctrl+Shift+R`) — Desk strings ride along with `bootinfo`, so a stale boot is
the usual reason a correct catalogue looks like it did not apply.

For sites installed before this was automated:

```bash
bench --site [your-site] execute erpnextvn.erpnext_vietnam.setup.enable_vietnamese
```

## ⚙️ Configuration

### Payroll (Lương & Thuế TNCN)

1. Go to `VN Payroll Settings` (Single DocType).
2. Verify statutory defaults:
   - Lương cơ sở: 2,340,000 VND
   - **Giảm trừ bản thân: 15,500,000 VND** (theo NQ 110/2025/UBTVQH15, áp dụng từ 2026)
   - **Giảm trừ người phụ thuộc: 6,200,000 VND** (theo NQ 110/2025/UBTVQH15, áp dụng từ 2026)
   - Tỷ lệ BHXH / BHYT / BHTN (NLĐ 8% / 1.5% / 1%, DN 17.5% / 3% / 1%)
   - Vùng lương: Vùng I 4,960,000 / Vùng II 4,410,000 / ...
3. Khi tạo Salary Slip, các trường VN (BHXH, Thuế TNCN, Thu nhập tính thuế) sẽ được tự động tính.

### Hóa đơn điện tử

1. Go to `VN E Invoice Settings`.
2. Chọn nhà cung cấp (Viettel / VNPT / MISA / FPT / BKAV).
3. Nhập thông tin đăng nhập và chứng thư số.
4. Bật **Sandbox mode** để test trước.
5. Khi submit Sales Invoice, hoặc click nút **"Phát hành HĐĐT"**.

## 🧪 Testing

```bash
# Unit tests (no Frappe bench needed for pure-Python utilities)
cd /path/to/erpnextvn
python -m pytest erpnextvn/payroll/ -v

# Frappe-integrated tests
bench --site [site] run-tests --app erpnextvn
```

## 🤝 Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## 📄 License

GPL v3 — see [LICENSE](LICENSE).

## 👥 Credits

- **Publisher:** 1nguoi.com
- **Email:** hello@1nguoi.com
- **Repository:** https://github.com/mrhuychien/erpnextvn
