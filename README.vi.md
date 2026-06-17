[English](README.md) | [한국어](README.ko.md) | [Español](README.es.md) | [Français](README.fr.md) | [中文](README.zh.md) | [日本語](README.ja.md) | **Tiếng Việt**

# teach-me-a-lesson — một skill đóng vai người thầy kiên nhẫn, gần gũi cho người mới học AI và lập trình

Một [skill của Claude](https://docs.claude.com/en/docs/claude-code/skills) giải thích Claude, các công cụ AI và các khái niệm lập trình/CNTT **theo cách một người thầy tốt sẽ làm với người mới hoàn toàn và người không chuyên về kỹ thuật**, đồng thời tiếp tục hỗ trợ bạn trong lúc làm việc.

Thay vì chỉ đưa ra đáp án, nó tập trung tạo ra khoảnh khắc **"à, *thì ra là vậy*!"** chỉ bằng một phép so sánh hay.

## Nó làm gì

Nó hoạt động ở sáu chế độ (kích hoạt bằng cách hỏi trực tiếp, hoặc bằng lệnh slash).

| Chế độ | Lệnh | Chức năng |
|--------|------|-----------|
| **explain** | `/tl-explain <chủ đề>` | Giải thích một khái niệm bằng phép so sánh, bảng biểu và các ý chính (mặc định) |
| **mistake** | `/tl-mistake` | Chẩn đoán điều gì đã sai và vì sao — không trách móc — cùng cách khắc phục |
| **bad-habit** | `/tl-bad-habit` | Phát hiện những thói quen xấu lặp lại và gợi ý cách làm tốt hơn |
| **knowledge** | `/tl-knowledge <chủ đề>` | Lưu điều bạn vừa học thành tệp kiến thức (ghi chú markdown) |
| **token** | `/tl-token` | Quan sát cách bạn làm việc và chỉ ra chỗ lãng phí token/ngữ cảnh, kèm cách sửa cụ thể |
| **config** | `/tl-config` | Đặt ngôn ngữ, mức độ trang trọng, giọng điệu/nhân cách, lượng emoji và cách xưng hô với bạn |

Khi skill được nạp, nó còn đóng vai **người trợ giúp luôn bên cạnh**: khi thấy hành động rủi ro (dán lệnh không rõ nguồn gốc, để lộ khóa API, thao tác không thể hoàn tác), yêu cầu dựa trên hiểu lầm, hoặc cách làm vòng vo kém hiệu quả, nó **nhắc nhẹ nhàng** — không cằn nhằn — và để bạn tự quyết định.

> Lưu ý: việc hỗ trợ liên tục hoạt động khi skill được nạp (trong ngữ cảnh hội thoại). Đây không phải là một hook tự động kiểm tra mọi lần nhập.

### Ví dụ kích hoạt

- "Giải thích MCP là gì, thật đơn giản — mình là người mới hoàn toàn"
- "Mình hay lẫn lộn API và SDK. Giải thích sự khác nhau bằng một phép so sánh đi"
- "Mình sợ terminal — có nhất thiết phải dùng không?"
- "Hình như mình vừa commit tệp .env lên GitHub — vấn đề là gì?" → mistake
- "Chỉ ra những thói quen xấu của mình đi" → bad-habit
- "Mình thấy như đang đốt token — xem giúp mình với?" → token

## Cài đặt

### 1) Sao chép thư mục skill

```bash
# macOS / Linux
cp -r teach-me-a-lesson ~/.claude/skills/

# Windows (PowerShell)
Copy-Item -Recurse teach-me-a-lesson $env:USERPROFILE\.claude\skills\
```

### 2) Cài đặt các lệnh slash (tùy chọn, để dùng /tl-*)

Sao chép các tệp trong thư mục `commands/` của skill vào thư mục lệnh của bạn.

```bash
# macOS / Linux
cp teach-me-a-lesson/commands/tl-*.md ~/.claude/commands/

# Windows (PowerShell)
Copy-Item teach-me-a-lesson\commands\tl-*.md $env:USERPROFILE\.claude\commands\
```

Skill cũng tự kích hoạt từ những câu đơn giản như "giải thích cái này đơn giản thôi". Các lệnh chỉ là cách tiện lợi để gọi rõ một chế độ cụ thể.

## (Tùy chọn) Kết nối tệp kiến thức của riêng bạn

Nếu bạn có **tệp kiến thức** (một thư mục ghi chú markdown), skill sẽ dùng chúng làm nguồn ưu tiên. Nếu không có, nó quay về dùng kiến thức sẵn có của Claude — nên **vẫn hoạt động tốt mà không cần bất kỳ tệp kiến thức nào**.

- Thư mục tra cứu/lưu mặc định: `./knowledge/` trong thư mục làm việc của bạn, hoặc `~/.claude/teach-me-a-lesson/knowledge/`
- Nếu đã có sẵn một thư mục ghi chú, chỉ cần trỏ tới đó.
- Về quy tắc chi tiết và định dạng chỉ mục tùy chọn, xem `references/knowledge-files.md`.

> Kho lưu trữ này **không** kèm theo bất kỳ tài liệu kiến thức cá nhân nào. Chỉ có phương pháp giảng dạy (bản thân skill) được công bố.

## Thiết lập giọng điệu và ngôn ngữ

Bạn có thể tùy chỉnh **ngôn ngữ, mức độ trang trọng và phong cách** của người thầy theo ý thích. Ví dụ với tiếng Hàn, nó điều chỉnh không chỉ mức lịch sự (존댓말/반말) mà cả **bầu không khí** (ấm áp, mộc mạc, sôi nổi, trang trọng).

- `/tl-config` — lần lượt hỏi: ngôn ngữ → mức trang trọng → giọng điệu/nhân cách → lượng emoji → cách xưng hô, rồi lưu lại
- Dùng ngôn ngữ tự nhiên cũng được — "nói chuyện thoải mái và hào hứng đi", "giải thích bằng tiếng Anh", "bớt emoji lại"
- Thiết lập được lưu trong `~/.claude/teach-me-a-lesson/config.json` (tệp giọng điệu cá nhân, nên **không** đi kèm trong bản phân phối). Khi không có thiết lập, nó chạy theo **mặc định (người thầy ấm áp, tiếng Hàn lịch sự 해요체)**.
- Dù ở giọng điệu nào, chất lượng giảng dạy (phép so sánh, không trách móc, không quá tải, dẫn nguồn) vẫn giữ nguyên. Xem `references/tone-config.md`.

## Cấu trúc

```
teach-me-a-lesson/
├── SKILL.md                      # Điều kiện kích hoạt + 6 chế độ + hỗ trợ liên tục + cấu hình giọng + quy trình
├── references/
│   ├── teaching-style.md         # Cách tạo phép so sánh, ví dụ tốt/xấu, cách chỉnh sửa nhẹ nhàng
│   ├── knowledge-files.md        # Quy tắc tra cứu/lưu tệp kiến thức (tổng quát)
│   ├── modes.md                  # Chi tiết 6 chế độ + ví dụ hỗ trợ liên tục
│   └── tone-config.md            # Lược đồ và nhân cách cho ngôn ngữ/mức trang trọng/giọng/emoji/xưng hô
├── commands/                     # Lệnh slash /tl-* (sao chép vào thư mục lệnh của bạn)
├── evals/
│   └── evals.json
├── README.md                     # Tiếng Anh (mặc định)
├── README.{ko,es,fr,zh,ja,vi}.md # Bản dịch (KO/ES/FR/ZH/JA/VI)
└── LICENSE
```

## Giấy phép

Giấy phép MIT. Tự do sử dụng, chỉnh sửa và phân phối lại.
