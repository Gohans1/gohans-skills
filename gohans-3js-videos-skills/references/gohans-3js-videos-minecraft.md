# Minecraft 3D Video Architecture & Assets Guide

## Setup
- không tải trực tiếp các folder/file nặng như .jar, full modpack,etc... vào thẳng project. Lưu bọn minecraft assets nặng gốc đã tải về ở khu riêng biệt trong máy để các project dùng chung
- Khi Project cần đạo cụ/assets/ảnh/nhân vật/sự vật/mô hình/etc... Cụ thể nào trong đống đó thì hãy chỉ kéo riêng mình nó về dùng vào `pack/` 

Dùng symlink nối kho gốc với project (nhớ gitignore)
- <vault_path>/jar     -> assets/public/mc
- <vault_path>/mcasset -> assets/public/mcasset
- <vault_path>/mcprep  -> assets/public/rig

- Nếu đã setup thì có thể bỏ qua bước này

## Using
- Tìm và cho dev xem mẫu 3-6 variants mà m cho là hợp lý nhất

## Repo

### block-model-renderer
- Vai trò: Dựng toàn bộ thế giới khối tĩnh, tường nhà, địa hình, bàn ghế, đồ đạc và đạo cụ nội thất.
- Điểm mạnh: Đọc trực tiếp định dạng Block JSON chuẩn (elements, from, to, faces). Tự động tính culling khử mặt khuất, gộp lưới tối ưu hóa draw call và đổ bóng chuẩn từng điểm ảnh.

### MineRender
- Vai trò: Vẽ giao diện 2D, phông chữ pixel Minecraft và hoạt ảnh động vật sống.
- Điểm mạnh:
  - GuiObject: In chữ pixel chuẩn game (ví dụ nhãn camera an ninh, phụ đề, mã phòng) và các bảng giao diện hotbar, thanh máu lên lớp phủ 2D.
  - EntityObject: Chứa sẵn toàn bộ mô hình sinh vật trích xuất từ Java code kèm xương và hoạt ảnh bước chân (walk cycle) tự nhiên khớp với trục thời gian.

### MCprep (player.glb)
- Vai trò: Diễn viên người chơi chính (Steve, Alex hoặc skin tùy biến).
- Điểm mạnh: Khớp uốn cong khuỷu tay và đầu gối 90 độ mượt mà không rách lưới, có sẵn hệ thống xương điều khiển mắt, miệng và cử chỉ ngón tay.
- Ghi nhận quyền tác giả: BoxScape Studios và TheDuckCow theo giấy phép CC-BY 3.0.

### Modrinth API
- Vai trò: Tìm kiếm và tải tài nguyên tự động, sạch bản quyền.
- Điểm mạnh: API mở không cần khóa truy cập, hỗ trợ lọc theo giấy phép thương mại thoáng (MIT, CC0, CC-BY-4.0).
- Endpoint tìm kiếm: https://api.modrinth.com/v2/search?query=KEYWORD&facets=[["license:MIT","license:CC0-1.0","license:CC-BY-4.0"],["project_type:mod","project_type:resourcepack"]]

## Danh Mục Các Gói Tài Nguyên Đã Kiểm Chứng

Danh sách các gói mô hình chuẩn Block JSON có giấy phép mở, tương thích hoàn toàn với Three.js và block-model-renderer, sắp xếp theo số lượt tải giảm dần:

| Gói | Lượt tải | Use case | Định dạng | Giấy phép | Link tải / Trang chủ | Công năng chính |
| --- | --- | --- | --- | --- | --- | --- |
| Farmer's Delight | 25.5M | Bếp ăn, sinh hoạt đời thường, thùng chứa đồ | Mod (.jar) | MIT | https://modrinth.com/mod/farmers-delight | Thớt gỗ, chảo nấu, bếp lò, dao thái, kệ treo gia vị, rổ đựng thức ăn |
| Motschen's Better Leaves | 21.4M | Tán cây ngoài trời, đại cảnh thiên nhiên, flycam bao quát | Resource Pack (.zip) | MIT | https://modrinth.com/resourcepack/better-leaves | Tán lá cây 3D xòe nhánh bông xù, tăng chiều sâu và đổ bóng ambient occlusion |
| Iron Furnaces | 10.1M | Cụm năng lượng kim loại, máy phát điện ngầm, lò đốt công nghiệp | Mod (.jar) | Apache-2.0 | https://modrinth.com/mod/iron-furnaces | Lò kim loại nguyên khối thép, đồng, vàng, obsidian có khe tản nhiệt và khe sáng |
| Macaw's Doors | 8.3M | Cửa kính trượt văn phòng, lối vào sảnh công nghệ, cửa showroom | Mod (.jar) | MIT | https://modrinth.com/mod/macaws-doors | Cửa kính trượt, cửa kính văn phòng 2 cánh, cửa gỗ thanh lịch, cửa xếp |
| Decorative Blocks | 6.4M | Gia cố kiến trúc nhà xưởng, xà treo, công trình lớn | Mod (.jar) | MIT | https://modrinth.com/mod/decorative-blocks | Xà gỗ trợ lực chống trần, xích sắt treo, vạc lửa, cột đá chịu lực |
| SecurityCraft | 5.9M | Lối đi bảo mật, nhà tù, căn cứ bí mật, lồng giam | Mod (.jar) | MIT | https://modrinth.com/mod/security-craft | Cửa sắt bấm mã, bảng phím số, còi báo động, máy quét, lồng giam an ninh |
| CC: Tweaked | 5.3M | Phòng máy chủ AI, trung tâm điều khiển, màn hình vi tính | Mod (.jar) | MPL-2.0 | https://modrinth.com/mod/cc-tweaked | Máy tính để bàn, cụm màn hình lớn, modem mạng, loa phát tín hiệu, ổ đĩa |
| Mekanism | 3.9M | Phòng thí nghiệm sci-fi, máy móc lượng tử, bồn hóa chất | Mod (.jar) | MIT | https://modrinth.com/mod/mekanism | Bồn hóa chất, máy phân tách phân tử, máy phát laser, tủ điều khiển bo mạch |
| Dusty Decorations | 3.5M | Hiện trường bỏ hoang, căn phòng bám bụi, kho hàng cũ | Mod (.jar) | MIT | https://modrinth.com/mod/dusty-decorations | 370 khối đạo cụ bám bụi: xà ngang, giá kệ, thùng hàng, rổ đan, đệm ngồi |
| Refined Storage | 3.0M | Tủ rack máy chủ AI, trung tâm dữ liệu, mạng lưới cáp server | Mod (.jar) | MIT | https://modrinth.com/mod/refined-storage | Tủ rack ổ cứng server đèn LED nhấp nháy, màn hình lưới dữ liệu, dây cáp mạng |
| RAY's 3D Ladders | 2.8M | Cảnh leo trèo thoát hiểm, giếng trời, hầm thông gió có chiều sâu | Resource Pack (.zip) | MIT | https://modrinth.com/resourcepack/rays-3d-ladders | Thang leo 3D chân thực, thanh ngang tròn nổi khối thay cho decal phẳng |
| Modern Industrialization | 2.0M | Đại cảnh nhà máy ngầm, cơ sở hạt nhân, bồn bể công nghiệp nặng | Mod (.jar) | MIT | https://modrinth.com/mod/modern-industrialization | Cụm máy hơi nước, tuabin điện, đường ống dẫn chất lỏng, lò phản ứng hạt nhân |
| Actually 3D Blocks & Items | 283K | Đạo cụ tài liệu trên bàn, đồ vật cầm tay, sách vở | Resource Pack (.zip) | CC-BY-4.0 | https://modrinth.com/resourcepack/actually-3d-blocks-and-items | Mô hình 3D cho các vật phẩm cầm tay, sách vở tài liệu đặt trên bàn, dụng cụ |
| NhatJS Furniture Mod | 121K | Bàn làm việc tối giản, diễn cảnh cạy tủ văn phòng, góc máy tính | Mod (.jar) | MIT | https://modrinth.com/mod/nhatjs-furniture-mod | Bàn làm việc đen, ngăn kéo đơn lẻ, ghế văn phòng, thùng máy tính, cụm màn hình bật tắt |
| Modern Furniture | 107K | Văn phòng công nghệ cao, trần nhà hiện đại, không gian làm việc sạch | Mod (.jar) | CC-BY-4.0 | https://modrinth.com/mod/modern-furniture | 437 khối nội thất hiện đại: ghế công thái học, đèn ốp trần, bàn đứng, điều hòa |
| Simplistic 3D Doors | 21K | Cửa sắt và cửa sập phòng giam dày dặn bắt sáng nổi khối | Resource Pack (.zip) | CC0-1.0 | https://modrinth.com/resourcepack/simplistic-3d-doors | Cửa sắt và cửa sập sắt 3D nổi khối, dùng lại ảnh gốc từ client.jar |
| Artemis Laboratory Blocks | 13K | Phòng nghiên cứu sinh hóa, cửa kính vi tính, phòng sạch cách âm | Mod (.jar) | MIT | https://modrinth.com/mod/artemis-laboratory-blocks | 100 khối phòng thí nghiệm: ống thông gió, màn hình vi tính, ốp tường cách âm |
