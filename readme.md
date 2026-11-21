# Pixel-Art Cinematic Day/Night Toggle (Liquid Glass)

Một công tắc chuyển đổi giao diện **Light / Dark Mode** tương tác mang phong cách điện ảnh, tái hiện văn phòng pixel-art thu nhỏ (`222×120`) sống động nằm bên trong khung kim loại 3D mảnh với thấu kính **Liquid Glass** khúc xạ quang học thời gian thực bằng WebGL và âm thanh tổng hợp trực tiếp bằng Web Audio API.

- **Tác giả:** [Diep Van Tien](https://github.com/diepvantien)
- **Repository:** `https://github.com/diepvantien/pixel-liquid-glass-toggle`
- **Live Demo (GitHub Pages):** `https://diepvantien.github.io/pixel-liquid-glass-toggle/`

---

## Tính năng nổi bật

- **Thấu kính Liquid Glass khúc xạ thực (WebGL Shader):**
  - Tính toán pháp tuyến bề mặt cầu (*spherical normal*) cho hiệu ứng phóng đại trong trẻo ở tâm và bẻ cong đường thẳng dọc mép kính dày (*meniscus warping*).
  - Tán sắc quang phổ (RGB chromatic aberration) ở viền, phản xạ Fresnel, điểm sáng studio cong, hiệu ứng hội tụ caustics và phản chiếu ánh sáng đèn bàn vào ban đêm.
  - Tự động chuyển sang chế độ **Canvas 2D Fallback** nếu thiết bị không hỗ trợ WebGL.
- **Văn phòng Pixel-Art sống động (`222×120`):**
  - **Cửa sổ thành phố:** Mây trôi ban ngày, sao nhấp nháy, đèn tín hiệu tòa nhà, xe cộ di chuyển và cửa sổ cao ốc bật tắt so le vào ban đêm.
  - **Bàn làm việc & Nhân vật:** Đồng hồ treo tường chạy theo giờ thực của cảnh, tách cà phê bốc khói, nhân vật chớp mắt & gõ phím, màn hình chuyển từ ứng dụng ban ngày sang trình soạn thảo code ban đêm, đèn bàn tỏa sáng ấm với các hạt bụi bay nhẹ.
  - **Nội thất & Sàn gạch:** Tủ tài liệu, hộp cam, máy in có đèn LED nhấp nháy, cây xanh rủ đung đưa và sàn gạch đổ bóng nắng.
- **Âm thanh thời gian thực (Web Audio API):**
  - Tiếng chạm kim loại-kính (*tactile click*), tiếng trượt kính biến thiên theo vận tốc kéo thực tế, tiếng hít nam châm khi dừng khớp, tiếng *tách* công tắc đèn bàn, tiếng gõ phím nhẹ theo nhịp nhân vật và không gian nền Ngày ↔ Đêm.
- **Hệ thống ánh sáng 8 kênh & Timeline tiến tới (Forward-Time):**
  - Chuyển đổi **Ngày → Đêm** đi qua hoàng hôn vàng ấm (`day_to_night`).
  - Chuyển đổi **Đêm → Ngày** đi qua rạng đông và bình minh sáng hôm sau (`night_to_next_day`), không tua ngược hoàng hôn.
- **Studio Quay Video 9:16 tích hợp (`720×1280 @ 60fps`):**
  - Quay tự động kịch bản 10 giây hoặc tự kéo nghịch nút và xuất thẳng file video dọc `.mp4` / `.webm` kèm âm thanh thời gian thực.
- **Tích hợp Theme, Trợ năng & QA Suite:**
  - Đồng bộ với `data-theme`, class `.dark`, `localStorage`, `prefers-color-scheme` và `prefers-reduced-motion`.
  - Hỗ trợ chuột, kéo cảm ứng (Pointer/Touch drag), bàn phím (`Tab`, `Space`, `Enter`) và bảng **Inspector & QA** kiểm thử tự động.

---

## Cấu trúc dự án

Dự án được đóng gói gọn nhẹ, không cần công cụ build (zero-build):

```text
pixel-liquid-glass-toggle/
├── index.html   # Toàn bộ giao diện, CSS, PixelOfficeScene, WebGL Shader, Audio Engine & Video Studio
├── README.md    # Tài liệu giới thiệu & hướng dẫn sử dụng
└── LICENSE      # Giấy phép MIT
```

---

## Chạy thử cục bộ

Mở trực tiếp tệp `index.html` trên trình duyệt hiện đại (Chrome, Edge, Safari, Firefox), hoặc khởi chạy local server:

```bash
npx serve .
```

---

## Kiến trúc kỹ thuật chính

| Thành phần | Vai trò |
| :--- | :--- |
| `RealisticAudioEngine` | Tổng hợp âm thanh thời gian thực bằng Web Audio API & cấp luồng âm thanh cho Video Studio. |
| `LightingEngine` | Quản lý 8 kênh ánh sáng độc lập và 2 timeline tiến tới (Hoàng hôn / Bình minh). |
| `PixelOfficeScene` | Vẽ toàn bộ văn phòng pixel-art `222×120` lên một offscreen canvas duy nhất. |
| `LiquidGlassRenderer` | WebGL Fragment Shader lấy mẫu từ offscreen canvas để tạo khúc xạ, tán sắc & phản xạ kính. |
| `ThemeController` | Đồng bộ trạng thái Light/Dark với DOM, `localStorage` và hệ điều hành. |
| `CinematicThemeToggle` | Máy trạng thái điều khiển kéo/thả, bàn phím, vòng lặp `requestAnimationFrame` và ARIA. |
| `VideoStudio9x16` | Trình ghép khung hình dọc 9:16 và xuất video kèm âm thanh bằng `MediaRecorder API`. |

---

## Giấy phép

Phát hành theo giấy phép [MIT License](LICENSE).