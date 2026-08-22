# 🐍 Snake — Huyền Thoại

Con rắn săn mồi huyền thoại viết bằng **HTML + CSS + JavaScript** thuần, gói gọn trong **một file duy nhất**. Không cài đặt, không build, không server — mở là chơi.

> Made with ☕ and 🐍 by **Pt**

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?logo=tailwind-css&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-green)

---

## ✨ Tính năng

- 🎮 **Một file duy nhất** — `snake.html`, không phụ thuộc ngoài (Tailwind và font nạp qua CDN).
- 🎨 **Giao diện neon** tối, bóng đổ phát sáng, gradient, họa tiết lưới.
- 🐍 **Rắn có mắt** nhìn theo hướng di chuyển, thân chuyển màu và mảnh dần về đuôi.
- 🍎 **Mồi phát sáng** với hiệu ứng pulse.
- 💥 **Hiệu ứng hạt (particles)** nổ tung khi ăn mồi, kèm flash trắng toàn màn hình.
- 🔊 **Âm thanh Web Audio** tự tạo — tiếng ăn, tiếng quay đầu, tiếng chết, tiếng bắt đầu — không cần file ngoài.
- 📈 **Tốc độ tự tăng** mỗi lần ăn (9 → 22 bước/giây), hiển thị nhân tốc độ.
- 🏆 **Lưu kỷ lục** bằng `localStorage`.
- ⏸ **Tạm dừng / chơi lại** bằng nút hoặc phím tắt.
- 📱 **Hỗ trợ mobile** — D-pad cảm ứng + vuốt trực tiếp trên màn hình.
- ⌨️ **Điều khiển bàn phím** — mũi tên hoặc WASD.

---

## 🚀 Chơi nhanh

### Cách 1 — Mở trực tiếp

1. Tải file [`snake.html`](./snake.html) về máy.
2. Double-click để mở bằng trình duyệt (Chrome, Edge, Firefox, Safari…).
3. Bấm **▶ Bắt đầu** và chơi.

### Cách 2 — Chạy qua server local (tùy chọn)

```bash
# Python 3
python -m http.server 8000

# hoặc Node
npx serve .
```

Sau đó mở `http://localhost:8000/snake.html`.

> Game chạy hoàn toàn ở phía client, không thu thập dữ liệu, không cần mạng sau khi CDN tải xong.

---

## 🎹 Điều khiển

| Phím / Thao tác | Tác dụng |
|---|---|
| `↑` `↓` `←` `→` hoặc `W` `A` `S` `D` | Chuyển hướng rắn |
| `Space` / `P` | Tạm dừng / tiếp tục |
| `R` | Chơi lại |
| `Esc` / `Q` | Thoát (đóng tab) |
| Vuốt trên màn hình (mobile) | Chuyển hướng |
| D-pad cảm ứng (mobile) | Chuyển hướng |
| Nút 🔊 / 🔇 | Bật/tắt âm thanh |

---

## 🛠️ Công nghệ

| Thành phần | Công nghệ |
|---|---|
| Giao diện | [Tailwind CSS](https://tailwindcss.com/) (CDN) |
| Font chữ | [JetBrains Mono](https://www.jetbrains.com/lp/mono/) + [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk) |
| Đồ họa | HTML5 Canvas 2D |
| Âm thanh | Web Audio API (sóng sine/square/sawtooth/triangle) |
| Lưu trữ | `localStorage` |
| Logic | JavaScript ES6+ (IIFE, không framework) |

---

## 📐 Cấu trúc code

Toàn bộ trong `snake.html`:

```
snake.html
├── <head>
│   ├── Tailwind CDN + cấu hình theme
│   ├── Google Fonts
│   └── <style> custom (grid, button, animation, D-pad)
├── <body>
│   ├── Header (logo + trạng thái)
│   ├── HUD (Điểm / Kỷ lục / Tốc độ)
│   ├── <canvas> 28×24 ô × 24px = 672×576
│   ├── Overlay (start / pause / game over)
│   ├── Hàng nút (âm thanh, tạm dừng, chơi lại)
│   └── D-pad cho mobile
└── <script> (IIFE)
    ├── Cấu hình (CELL, COLS, ROWS, SPEED, COLORS)
    ├── Trạng thái (snake, dir, food, score, …)
    ├── Web Audio (beep, sfx)
    ├── reset() / spawnFood()
    ├── setDir() — chặn đảo ngược
    ├── step() — một nhịp game
    ├── gameOver()
    ├── Hiệu ứng (burst particles, flash)
    ├── Vẽ (draw, drawSnake, drawFood, drawParticles)
    ├── Vòng lặp requestAnimationFrame
    └── Gắn sự kiện (bàn phím, chuột, cảm ứng)
```

---

## ⚙️ Tùy chỉnh dễ dàng

Mở `snake.html`, tìm khối **Cấu hình** ở đầu `<script>`:

```js
const CELL = 24;              // kích thước 1 ô (px)
const COLS = 28;              // số ô ngang
const ROWS = 24;              // số ô dọc
const START_SPEED = 9;        // tốc độ khởi đầu (bước/giây)
const MAX_SPEED = 22;         // tốc độ tối đa
const SPEED_STEP = 0.35;      // tăng mỗi lần ăn
```

Đổi màu ở `COLORS`:

```js
const COLORS = {
  head: '#74db81',
  body: '#48bb78',
  tail: '#2e8860',
  food: '#e85c6a',
  // ...
};
```

> Nếu đổi `COLS` / `ROWS` / `CELL`, nhớ kiểm tra kích thước `canvas` ở thẻ `<canvas>` cho khớp.

---

## 🧪 Kiểm thử

Logic game đã được test bằng Node với mock trình duyệt:

- ✅ Khởi tạo rắn 3 khúc, đi sang phải
- ✅ Di chuyển theo hướng
- ✅ Ăn mồi → cộng điểm, dài thêm, tăng tốc
- ✅ Chặn đảo ngược tức thì
- ✅ Tự cắn thân → game over
- ✅ Va tường → game over
- ✅ `spawnFood` không trùng thân rắn (50/50)
- ✅ Tốc độ bị chặn ở `MAX_SPEED`
- ✅ Kỷ lục lưu vào `localStorage`

Chạy test:

```bash
node /tmp/snake_logic_test2.js
```

(script test nằm ngoài repo, dùng cho môi trường dev).

---

## 🗺️ Có thể mở rộng

- 🧱 Chế độ tường xuyên (wrap-around)
- 🌟 Mồi vàng / mồi đặc biệt cho điểm cao
- ⚡ Vật phẩm tốc độ / khiên
- 👾 Hai người chơi chung bàn phím
- 🗺️ Bản đồ có chướng ngại vật
- 🌗 Chuyển theme sáng/tối
- 🏅 Bảng xếp hạng nhiều người

Cứ mở issue / pull request hoặc tự nhánh mà chơi.

---

## 📄 Giấy phép

[MIT](./LICENSE) — tự do dùng, sửa, chia sẻ.

---

<div align="center">
  <sub>Được tạo bởi <b>Pt</b> · cảm tình với con rắn huyền thoại một thời.</sub><br>
  <sub>🐍 ☕ 🎮</sub>
</div>
