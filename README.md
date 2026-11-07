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
3. Tải artifact `Personal-Development-Handbook-v1.0.6-Android-debug` ở trang run.

Workflow cài dependencies bằng `npm install`, tạo Capacitor Android project, đồng bộ nội dung web và build APK debug. Source hiện không kèm `package-lock.json`, vì vậy workflow đã bỏ npm cache trong `actions/setup-node`; đây là cách phù hợp để tránh lỗi “Dependencies lock file is not found”. Muốn phát hành Play Store cần cấu hình signing key riêng.

## Dữ liệu và riêng tư
Dữ liệu hồ sơ/worksheet được lưu trong localStorage của ứng dụng. Không có tài khoản cloud, đồng bộ thiết bị hay truyền dữ liệu ra máy chủ trong bản 1.0.0. Hãy dùng Xuất dữ liệu để sao lưu trước khi xóa ứng dụng hoặc dữ liệu trình duyệt.

## Nguồn nội dung
`data/handbook.json` và `www/handbook.json` được trích xuất từ `Personal_Development_Handbook_VN_2026_REVISED.docx`.

## Cập nhật build v1.0.2
Workflow đã bỏ `android-actions/setup-android@v3` do action có thể yêu cầu gói SDK cũ `tools` không còn được phát hành. Thay vào đó workflow dùng Android SDK có sẵn trên GitHub Ubuntu runner và cài tường minh `platform-tools`, `platforms;android-34`, `build-tools;34.0.0`. Artifact mới có tên `Personal-Development-Handbook-1.0.2-debug`.


## v1.0.3 – Android và màu giao diện
- Hỗ trợ launcher icon Android legacy + adaptive icon cho thiết bị Android hiện đại.
- Vào Cá nhân → Cài đặt giao diện để chọn 5 màu: xanh ngọc, xanh dương, tím dịu, cam ấm, hồng đất.
- Màu được lưu cục bộ và áp dụng ngay; không cần khởi động lại ứng dụng.

### Android launcher icon
Workflow copies Android mipmap launcher resources and adaptive icon resources into the generated Capacitor Android project before Gradle build.


## v1.0.5 – Vuốt để quay lại
- Thêm thao tác vuốt từ mép trái màn hình sang phải để quay về màn hình trước.
- Có ngưỡng nhận diện cử chỉ để hạn chế kích hoạt nhầm khi cuộn dọc hoặc nhập biểu mẫu.
- Nút quay lại trong trang chuyên đề và phím Escape/Backspace (khi không nhập liệu) cũng dùng chung lịch sử điều hướng.
- Tên artifact APK: `Personal-Development-Handbook-1.0.5-debug`.


## v1.0.6 – Đồng bộ phiên bản, tên APK và worksheet
- Đồng bộ phiên bản hiển thị trong ứng dụng và package.json thành 1.0.6.
- Đổi tên file APK sau build thành Personal-Development-Handbook-v1.0.6-Android-debug.apk; artifact GitHub Actions dùng cùng tên.
- Bỏ số thứ tự dạng 1.1, 2.1… khỏi tiêu đề worksheet.
- Loại tiêu đề Worksheet thực hành đánh số trong phần nội dung chương vì ứng dụng đã có tiêu đề khu vực worksheet riêng, tránh hiển thị lặp.
- Điều chỉnh khoảng cách phần giới thiệu ứng dụng và nhãn phiên bản.


## v1.0.7 – Đồng bộ toàn bộ worksheet và sửa vuốt Back
- Bỏ tiền tố số chương/mục (1.1, 2.1… và các biến thể Worksheet 1.1) khỏi tiêu đề của tất cả worksheet trong cả 10 chuyên đề, không chỉ chuyên đề 1.
- Loại tiêu đề worksheet thực hành bị lặp trong nội dung chương trên cả 10 chuyên đề.
- Sửa nhận diện vuốt trái-sang-phải: không còn chỉ nhận diện trong vùng 42px sát mép; nhận diện cử chỉ ngang rõ ràng trong vùng nội dung, tránh ô nhập liệu và ưu tiên cuộn dọc.
- Đồng bộ phiên bản ứng dụng, package và tên APK/artifact thành 1.0.7.
