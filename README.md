# gospel-data

Dữ liệu tĩnh cho app đọc Lời Chúa — **không cần server**. Mỗi URL là một API.

Hiện có:

- **bibles/cgkpv2011** — Kinh Thánh CGKPV 2011 (73 sách)
- **calendars/lichvn** — Lịch phụng vụ Giáo hội Việt Nam (2026)

Thêm bản dịch mới: tạo thư mục `bibles/{id}/` theo cùng cấu trúc.  
Thêm giáo phận / lịch mới: tạo `calendars/{id}/{year}/`.

## API

Base URL (chọn một):

```
https://raw.githubusercontent.com/ndagnhat/gospel-data/main
https://cdn.jsdelivr.net/gh/ndagnhat/gospel-data@main
https://ndagnhat.github.io/gospel-data
```

### Kinh Thánh

| Mục | Path |
|---|---|
| Danh sách bản dịch | `/bibles/index.json` |
| Một bản dịch + danh sách sách | `/bibles/{id}/index.json` |
| Một sách (metadata + số chương) | `/bibles/{id}/{BOOK}/index.json` |
| Cả sách (đầy đủ câu) | `/bibles/{id}/{BOOK}/book.json` |
| Một chương | `/bibles/{id}/{BOOK}/{n}.json` |

Ví dụ:

```
GET /bibles/cgkpv2011/index.json
GET /bibles/cgkpv2011/JHN/index.json
GET /bibles/cgkpv2011/JHN/book.json
GET /bibles/cgkpv2011/JHN/1.json
```

`BOOK` dùng mã 3–4 ký tự: `GEN`, `PSA`, `MAT`, `JHN`, `1CO`, `EZK`, …

### Lịch phụng vụ

| Mục | Path |
|---|---|
| Danh sách lịch | `/calendars/index.json` |
| Một lịch | `/calendars/{id}/index.json` |
| Cả năm (rút gọn, không bài đọc) | `/calendars/{id}/{year}/index.json` |
| Một tháng | `/calendars/{id}/{year}/{MM}.json` |
| Một ngày | `/calendars/{id}/{year}/{MM}/{DD}.json` |

Ví dụ:

```
GET /calendars/lichvn/2026/index.json
GET /calendars/lichvn/2026/08.json
GET /calendars/lichvn/2026/08/21.json
```

Bài đọc trong lịch chỉ lưu **tham chiếu** (`bookCode`, chương, câu). Lấy nguyên văn từ API Kinh Thánh rồi cắt theo `startVerse`/`endVerse` (hoặc `selectedVerses` nếu có).

## CORS

`raw.githubusercontent.com`, jsDelivr và GitHub Pages đều cho phép GET từ trình duyệt.

## Tái dựng

```
python3 scripts/build.py
```
