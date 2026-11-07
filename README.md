# Phát triển bản thân — Mobile App

Ứng dụng tiếng Việt offline-first chuyển thể từ Personal Development Handbook 2026.

## Nội dung
- 10 chương với nội dung bài học được trích xuất từ DOCX bản cập nhật.
- 30 worksheet tương tác; nội dung nhập được lưu tự động trên thiết bị.
- Dashboard theo dõi tiến độ học; đánh dấu hoàn thành chương.
- Mục tiêu 90 ngày, theo dõi thói quen 7 ngày, phản tư cuối tuần và ghi nhanh ngân sách.
- Nhiều hồ sơ người dùng cục bộ; xuất/nhập bản sao lưu JSON.
- PWA có thể cài lên màn hình chính và sử dụng offline sau lần tải đầu.
- Capacitor Android wrapper và GitHub Actions build debug APK.

## Chạy thử PWA
Mở thư mục `www` qua một static web server (không mở trực tiếp file:// để service worker hoạt động). Có thể deploy lên GitHub Pages/Netlify.

## Build APK trên GitHub
1. Tạo repository mới và push toàn bộ source.
2. Mở tab Actions, chọn `Build Android APK` và chạy workflow (hoặc push lên main/master).
3. Tải artifact `Personal-Development-Handbook-1.0.0-debug` ở trang run.

Workflow cài dependencies bằng `npm install`, tạo Capacitor Android project, đồng bộ nội dung web và build APK debug. Source hiện không kèm `package-lock.json`, vì vậy workflow đã bỏ npm cache trong `actions/setup-node`; đây là cách phù hợp để tránh lỗi “Dependencies lock file is not found”. Muốn phát hành Play Store cần cấu hình signing key riêng.

## Dữ liệu và riêng tư
Dữ liệu hồ sơ/worksheet được lưu trong localStorage của ứng dụng. Không có tài khoản cloud, đồng bộ thiết bị hay truyền dữ liệu ra máy chủ trong bản 1.0.0. Hãy dùng Xuất dữ liệu để sao lưu trước khi xóa ứng dụng hoặc dữ liệu trình duyệt.

## Nguồn nội dung
`data/handbook.json` và `www/handbook.json` được trích xuất từ `Personal_Development_Handbook_VN_2026_REVISED.docx`.
