# Minecraft 3D Video Architecture & Assets Guide

Tài liệu chuẩn về kiến trúc tài nguyên, thư viện và quy trình tích hợp mô hình Minecraft cho các dự án làm phim 3D bằng Three.js.

## 1. Nguyên Tắc Kho Tài Nguyên Tập Trung (Centralized Vault)

Không lưu trữ trực tiếp các file jar game gốc hoặc file pack mod nặng hàng chục megabyte vào trong repository code của từng dự án.

Mô hình chuẩn:
- Một kho tài nguyên bên ngoài dùng chung: Chứa client.jar gốc, mcasset dữ liệu thực thể, rig nhân vật MCprep và các gói mod hoặc resource pack đã tải.
- Mỗi dự án làm phim chỉ trích xuất cục bộ: Khi kịch bản cần đạo cụ nào (ví dụ bàn làm việc, ghế, cửa sắt), giải nén hoặc copy đúng file json mô hình và file png texture tương ứng đưa vào thư mục pack nội bộ của dự án đó.
- Lợi ích: Dung lượng dự án nhẹ gọn, tránh xung đột định danh giữa các mod, và giữ ngữ cảnh sạch để AI không bị nhầm lẫn giữa hàng ngàn khối gạch không liên quan.

## 2. Các Trụ Cột Kỹ Thuật

### block-model-renderer
- Vai trò: Dựng toàn bộ thế giới khối tĩnh, tường nhà, địa hình, bàn ghế, đồ đạc và đạo cụ nội thất.
- Điểm mạnh: Đọc trực tiếp định dạng Block JSON chuẩn (elements, from, to, faces). Tự động tính culling khử mặt khuất, gộp lưới tối ưu hóa draw call và đổ bóng chuẩn từng điểm ảnh.
- Cách dùng:
  - Nạp thế giới: createScene([packHandler, clientJarBytes], blockList, { lighting: "scene" })
  - Nạp đạo cụ cử động riêng: loadModel(scene, [packHandler, clientJarBytes], modelData, { mergeElements: false }) để tách các hộp riêng biệt cho phép xoay hoặc trượt bằng code theo biến thời gian t.

### MineRender
- Vai trò: Vẽ giao diện 2D, phông chữ pixel Minecraft và hoạt ảnh động vật sống.
- Điểm mạnh:
  - GuiObject: In chữ pixel chuẩn game (ví dụ nhãn camera an ninh, phụ đề, mã phòng) và các bảng giao diện hotbar, thanh máu lên lớp phủ 2D.
  - EntityObject: Chứa sẵn 209 mô hình sinh vật trích xuất từ Java code kèm xương và hoạt ảnh bước chân (walk cycle) tự nhiên khớp với trục thời gian.
- Cách dùng:
  - Giao diện 2D: new GuiObject([{ text: [{ text: "CELL 0412", color: 0xffffff }], position: [10, 8] }])
  - Động vật: new EntityObject("minecraft:cat") kết hợp tham số thời gian để bước đi theo nhịp.

### MCprep (player.glb)
- Vai trò: Diễn viên người chơi chính (Steve, Alex hoặc skin tùy biến).
- Điểm mạnh: Khớp uốn cong khuỷu tay và đầu gối 90 độ mượt mà không rách lưới, có sẵn hệ thống xương điều khiển mắt, miệng và cử chỉ ngón tay.
- Ghi nhận quyền tác giả: BoxScape Studios và TheDuckCow theo giấy phép CC-BY 3.0.

### Modrinth API
- Vai trò: Tìm kiếm và tải tài nguyên tự động, sạch bản quyền.
- Điểm mạnh: API mở không cần khóa truy cập, hỗ trợ lọc theo giấy phép thương mại thoáng (MIT, CC0, CC-BY-4.0).
- Endpoint tìm kiếm: https://api.modrinth.com/v2/search?query=KEYWORD&facets=[["license:MIT","license:CC0-1.0","license:CC-BY-4.0"],["project_type:mod","project_type:resourcepack"]]

## 3. Danh Mục Các Gói Tài Nguyên Đã Kiểm Chứng

Danh sách các gói mô hình chuẩn Block JSON có giấy phép mở, tương thích hoàn toàn với Three.js và block-model-renderer:

| Gói | Định dạng | Giấy phép | Link tải / Trang chủ | Công năng chính |
| --- | --- | --- | --- | --- |
| Simplistic 3D Doors | Resource Pack (.zip) | CC0-1.0 | https://modrinth.com/resourcepack/simplistic-3d-doors | Cửa sắt và cửa sập sắt 3D nổi khối, dùng lại ảnh gốc từ client.jar |
| NhatJS Furniture Mod | Mod (.jar) | MIT | https://modrinth.com/mod/nhatjs-furniture-mod | Bàn làm việc đen, ngăn kéo đơn lẻ, ghế văn phòng, thùng máy tính, cụm màn hình bật tắt |
| Modern Furniture | Mod (.jar) | CC-BY-4.0 | https://modrinth.com/mod/modern-furniture | 437 khối nội thất hiện đại: ghế công thái học, đèn ốp trần, bàn đứng, điều hòa |
| Dusty Decorations | Mod (.jar) | MIT | https://modrinth.com/mod/dusty-decorations | 370 khối đạo cụ bám bụi: xà ngang, giá kệ, thùng hàng, rổ đan, đệm ngồi |
| Decorative Blocks | Mod (.jar) | MIT | https://modrinth.com/mod/decorative-blocks | Xà gỗ trợ lực chống trần, xích sắt treo, vạc lửa, cột đá chịu lực |
| SecurityCraft | Mod (.jar) | MIT | https://modrinth.com/mod/security-craft | Cửa sắt bấm mã, bảng phím số, còi báo động, máy quét, lồng giam an ninh |
| Artemis Laboratory Blocks | Mod (.jar) | MIT | https://modrinth.com/mod/artemis-laboratory-blocks | 100 khối phòng thí nghiệm: ống thông gió, màn hình vi tính, ốp tường cách âm |
| Actually 3D Blocks & Items | Resource Pack (.zip) | CC-BY-4.0 | https://modrinth.com/resourcepack/actually-3d-blocks-and-items | Mô hình 3D cho các vật phẩm cầm tay, sách vở tài liệu đặt trên bàn, dụng cụ |

## 4. Quy Trình Trích Xuất Đạo Cụ Vào Dự Án

1. Xác định món đồ cần dùng trong kịch bản (ví dụ bàn đen black_desk).
2. Mở file nén .jar hoặc .zip trong kho lưu trữ bằng công cụ giải nén tiêu chuẩn.
3. Tìm đến đường dẫn assets/<namespace>/models/block/ để lấy file json mô hình.
4. Tìm đến đường dẫn assets/<namespace>/textures/block/ để lấy các file ảnh png vân bề mặt tương ứng.
5. Sao chép các file này vào thư mục pack/assets/ của dự án và đăng ký vào bộ nạp mô hình ảo.
6. Gọi tên khối trong hàm dựng thế giới hoặc hàm loadModel để hiển thị trên màn hình.

## 5. Các Bẫy Kỹ Thuật Thường Gặp & Cách Xử Lý

- Mô hình xoay bằng code Java trong mod: Một số mod (như camera an ninh của SecurityCraft) có file json mô hình rỗng vì được xoay động bằng code Java. Cách xử lý: tự viết một file Block JSON đơn giản gồm 4 đến 5 khối hộp đặt trong thư mục pack nội bộ để chủ động kiểm soát góc nhìn và độ xoay.
- Định dạng .geo.json của GeckoLib: Một số mod trang trí chứa mô hình dạng .geo.json mà block-model-renderer không hỗ trợ. Cách xử lý: mở file bằng phần mềm Blockbench và xuất sang định dạng chuẩn .glb.
- Gói vật phẩm tùy biến CIT thiếu blockstates: Các gói mô hình 3D cho vật phẩm cầm tay (như Actually 3D Blocks & Items) đặt file trong thư mục models/item/ mà không có thư mục blockstates/. Cách xử lý: nạp riêng lẻ qua hàm loadModel hoặc khai báo thêm một file blockstate ảo trong thư mục pack của dự án.
- Cử động từng bộ phận của khối tĩnh (ví dụ mở ngăn kéo, xoay cần gạt): Khi cần di chuyển một phần của khối theo thời gian phim draw(t), bắt buộc nạp mô hình qua hàm loadModel kèm tùy chọn mergeElements: false để tách rời các khối hộp Mesh con, sau đó thay đổi tọa độ Mesh theo hàm thời gian.
