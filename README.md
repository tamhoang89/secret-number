# 🎯 Secret Number dApp

Một ứng dụng phi tập trung (dApp) trên mạng lưới Cardano (Preprod Testnet) được xây dựng với mục đích giáo dục. Người chơi sẽ dự đoán một con số bí mật nằm trong khoảng từ `1` đến `999,999`. Nếu đoán đúng, người chơi sẽ nhận được phần thưởng bằng ADA từ kho bạc (Treasury) của Smart Contract!

## 🏗 Kiến trúc Dự án

Dự án này là một monorepo bao gồm 4 thành phần chính:

- `onchain/`: Chứa mã nguồn Smart Contract được viết bằng ngôn ngữ **[Aiken](https://aiken-lang.org/)**. Script sẽ kiểm tra xem người chơi có đoán đúng số hay không, và giới hạn số tiền rút ra.
- `offchain/`: Thư viện xử lý giao dịch TypeScript sử dụng **[MeshJS](https://meshjs.dev/)**. Đảm nhiệm việc tạo, ký và gửi giao dịch lên mạng lưới Cardano.
- `frontend/`: Giao diện người dùng Web3 hiện đại được xây dựng bằng **Next.js**, **Tailwind CSS**, và **Framer Motion**.
- `scripts/`: Chứa script triển khai (`deploy.ts`) để khởi tạo UTxO Treasury ban đầu trên mạng.

## 🚀 Hướng dẫn Cài đặt & Chạy dApp

### 1. Yêu cầu hệ thống
- **Node.js**: Phiên bản 18.x trở lên
- **Aiken CLI**: [Cài đặt Aiken](https://aiken-lang.org/installation-instructions) (để biên dịch Smart Contract)
- Một ví Cardano Testnet (như Eternl, Nami, Flint) có sẵn đồng tADA.

### 2. Cài đặt các thư viện (Dependencies)
Tại thư mục gốc của dự án, chạy lệnh:
```bash
npm install
```

### 3. Cấu hình Biến Môi trường (Environment Variables)
Tạo một file `.env` tại thư mục gốc (hoặc copy từ file mẫu nếu có) và cấu hình các thông tin sau:
```env
# Blockfrost API Key cho mạng Preprod
NEXT_PUBLIC_BLOCKFROST_API_KEY="preprod..."

# Mnemonic 15 hoặc 24 từ của ví Admin (dùng để cấp vốn ban đầu)
MNEMONIC="word1 word2 ... word24"

# Cấu hình khởi tạo Game
INITIAL_SECRET=42
INITIAL_TREASURY_ADA=50
```

> [!NOTE]
> Next.js yêu cầu tiền tố `NEXT_PUBLIC_` cho biến API Key để có thể chạy trên trình duyệt.

### 4. Biên dịch Smart Contract (On-chain)
Trước khi chạy dự án, bạn cần biên dịch mã nguồn Aiken thành file `plutus.json`:
```bash
cd onchain
aiken build
cd ..
```

### 5. Triển khai Treasury (Deploy)
Để bắt đầu trò chơi, cần có một quỹ thưởng ban đầu. Lệnh deploy sẽ sử dụng ví Admin của bạn để nạp tADA vào địa chỉ Smart Contract cùng con số bí mật đầu tiên.
```bash
npm run deploy
```

### 6. Chạy Giao diện Front-end
Khởi động máy chủ Next.js để chơi game:
```bash
npm run dev
```
Mở trình duyệt và truy cập: `http://localhost:3000`

## 💡 Bài tập Thực hành (Dành cho học viên)
Dự án này được thiết kế như một công cụ học tập. Trong mã nguồn, có một số phần được đánh dấu là `TODO` để học viên tự hoàn thiện:
- Mở file `offchain/src/decode.ts` và implement hàm `decodeDatum()` để chuyển đổi Raw CBOR Hex từ UTxO thành số nguyên Secret Number.

---
*Dự án này được xây dựng như một bản demo phục vụ cho khóa học lập trình Cardano. Vui lòng cân nhắc kỹ trước khi sử dụng trong môi trường production.*

*Happy Coding! 🚀*
