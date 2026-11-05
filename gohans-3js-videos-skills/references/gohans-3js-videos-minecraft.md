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
| Presence Footsteps | 41.2M | Âm thanh bước chân chân thực cho từng bề mặt sàn | Mod (.jar) | Polyform Shield | https://modrinth.com/mod/presence-footsteps | Âm thanh bước chân trên đá, gỗ, kim loại, cát, nước, thảm |
| AmbientSounds | 41.1M | Âm thanh môi trường điện ảnh, thiên nhiên, thời tiết | Mod (.jar) | LGPL-3.0 | https://modrinth.com/mod/ambientsounds | Tiếng gió rít, tiếng sấm dội, tiếng mưa rào, chim muông, hang động |
| [TaCZ] Timeless and Classics Zero | 32.5M | Vũ trang tác chiến, cảnh đấu súng, đặc nhiệm, lính canh | Mod (.jar) | GPL-3.0 | https://modrinth.com/mod/timeless-and-classics-zero | Súng trường AK, M4A1, súng tỉa AWP, súng lục, shotgun, ống ngắm, laser |
| Visuality | 30.8M | Hiệu ứng hạt điện ảnh, khói lửa, tia sáng môi trường | Mod (.jar) | MIT | https://modrinth.com/mod/visuality | Tia lửa hàn, khói bốc nghi ngút, đốm sáng ma mị, bọt nước bắn tóe |
| Supplementaries | 29.0M | Đạo cụ làng mạc, lồng treo, cờ phướn, biển chỉ đường | Mod (.jar) | Custom | https://modrinth.com/mod/supplementaries | Bình gốm, vòi nước chảy, bảng gỗ chỉ đường, lồng giam tù nhân, đồng hồ cát |
| Create | 27.9M | Cơ khí truyền động khổng lồ, nhà máy tự động hóa | Mod (.jar) | Custom | https://modrinth.com/mod/create | Bánh răng gỗ khổng lồ, trục quay cơ học, băng chuyền, bánh đà trợ lực, cẩu tháp |
| Waystones | 27.5M | Điểm dịch chuyển tức thời, phong ấn không gian sci-fi | Mod (.jar) | All Rights Reserved | https://modrinth.com/mod/waystones | Trụ đá cổ ngữ phát sáng ma mị, cuộn giấy phong ấn không gian |
| Farmer's Delight | 25.5M | Bếp ăn, sinh hoạt đời thường, thùng chứa đồ | Mod (.jar) | MIT | https://modrinth.com/mod/farmers-delight | Thớt gỗ, chảo nấu, bếp lò, dao thái, kệ treo gia vị, rổ đựng thức ăn |
| YUNG's Better Dungeons | 23.0M | Hầm ngục tăm tối, pháo đài ngầm, tàn tích bỏ hoang | Mod (.jar) | LGPL-3.0 | https://modrinth.com/mod/yungs-better-dungeons | Hầm ngục đá rêu phong, mê cung ngầm, phòng giam bí mật dưới lòng đất |
| Particle Rain | 22.5M | Hiệu ứng mưa bão, bão tuyết điện ảnh, thời tiết khắc nghiệt | Mod (.jar) | MIT | https://modrinth.com/mod/particle-rain | Hạt mưa rơi dày đặc, bão tuyết xối xả, hiệu ứng sương mù và gió giật rợp màn hình |
| Motschen's Better Leaves | 21.4M | Tán cây ngoài trời, đại cảnh thiên nhiên, flycam bao quát | Resource Pack (.zip) | MIT | https://modrinth.com/resourcepack/better-leaves | Tán lá cây 3D xòe nhánh bông xù, tăng chiều sâu và đổ bóng ambient occlusion |
| YUNG's Better Mineshafts | 21.3M | Hầm mỏ bỏ hoang, giàn giáo hầm mỏ, đường ray ngầm | Mod (.jar) | LGPL-3.0 | https://modrinth.com/mod/yungs-better-mineshafts | Giàn giáo gỗ hầm mỏ khổng lồ, đường ray bỏ hoang ngập mạng nhện, trục thông gió |
| Immersive Aircraft | 15.5M | Đại cảnh không chiến, vận tải đường không, thám hiểm bầu trời | Mod (.jar) | GPL-3.0 | https://modrinth.com/mod/immersive-aircraft | Máy bay hai tầng cánh, trực thăng gyrodyne, khí cầu Zeppelin, phi thuyền chở hàng |
| Exposure | 14.8M | Nhiếp ảnh điều tra, chụp lén hiện trường, phóng sự báo chí | Mod (.jar) | MIT | https://modrinth.com/mod/exposure | Máy ảnh cơ cổ điển, ảnh chụp Polaroid, cuộn phim 35mm, đèn flash, tripod |
| Create: Steam 'n' Rails | 13.5M | Đại cảnh ga tàu, logistics công nghiệp, vận tải xe lửa | Mod (.jar) | LGPL-3.0 | https://modrinth.com/mod/create-steam-n-rails | Đường ray xe lửa khổ lớn, cụm bánh bogey, toa chở hàng, đầu máy hơi nước |
| Spartan Weaponry | 13.3M | Vũ khí cận chiến, binh khí cổ, cảnh giao chiến sinh tồn | Mod (.jar) | Apache-2.0 | https://modrinth.com/mod/spartan-weaponry | Đại đao, trường thương, kiếm bản rộng, phi tiêu, nỏ liên châu, búa tạ |
| [Let's Do] Vinery | 12.6M | Hầm rượu cổ, nhà hàng sang trọng, trang trại nho | Mod (.jar) | Custom | https://modrinth.com/mod/lets-do-vinery | Thùng ủ rượu gỗ sồi, kệ rượu vang, chai rượu và ly thủy tinh tinh xảo |
| Naturalist | 11.6M | Cảnh rừng rậm hoang dã, safari, sinh thái tự nhiên | Mod (.jar) | Custom | https://modrinth.com/mod/naturalist | 47 loài động vật hoang dã: sư tử, voi, gấu trúc, hươu nai, chim chóc, cá sấu |
| The Lost Cities | 11.5M | Đại cảnh thành phố đổ nát, tòa nhà chọc trời, đô thị hậu tận thế | Mod (.jar) | MIT | https://modrinth.com/mod/the-lost-cities | Cao ốc văn phòng bỏ hoang, đường cao tốc nứt nẻ, ga tàu điện ngầm ngập đổ nát |
| Macaw's Fences and Walls | 11.4M | Rào chắn an ninh, khuôn viên biệt thự, tường bảo vệ | Mod (.jar) | MIT | https://modrinth.com/mod/macaws-fences-and-walls | Hàng rào thép gai an ninh, tường rào bê tông cao cấp, cổng sắt trượt ra vào |
| Iron Furnaces | 10.1M | Cụm năng lượng kim loại, máy phát điện ngầm, lò đốt công nghiệp | Mod (.jar) | Apache-2.0 | https://modrinth.com/mod/iron-furnaces | Lò kim loại nguyên khối thép, đồng, vàng, obsidian có khe tản nhiệt và khe sáng |
| Macaw's Bridges | 9.7M | Cầu vượt sông, lối đi hẻm núi, cảnh quan giao thông | Mod (.jar) | All Rights Reserved | https://modrinth.com/mod/macaws-bridges | Cầu treo dây văng, cầu đá vòm, cầu gỗ bắc qua sông suối có lan can |
| Immersive Melodies | 9.3M | Ban nhạc biểu diễn, phòng thu âm, sự kiện âm nhạc | Mod (.jar) | GPL-3.0 | https://modrinth.com/mod/immersive-melodies | Đàn piano đại dương cầm, guitar điện, sáo trúc, trống jazz, micro đứng, loa thùng |
| Macaw's Doors | 8.3M | Cửa kính trượt văn phòng, lối vào sảnh công nghệ, cửa showroom | Mod (.jar) | MIT | https://modrinth.com/mod/macaws-doors | Cửa kính trượt, cửa kính văn phòng 2 cánh, cửa gỗ thanh lịch, cửa xếp |
| Macaw's Roofs | 8.2M | Nóc nhà hiện đại, mái ngói kiến trúc, khu dân cư | Mod (.jar) | All Rights Reserved | https://modrinth.com/mod/macaws-roofs | Mái ngói dốc, máng xối thoát nước mưa, kết cấu nóc nhà đa góc cạnh |
| Nyf's Spiders | 7.7M | Hang động rùng rợn, sinh vật bò trườn 3D, cảnh giật gân | Mod (.jar) | LGPL-2.1 | https://modrinth.com/mod/nyfs-spiders | Nhện 3D chân khớp bò trườn tường và trần nhà chân thực, giăng tơ nhện chằng chịt |
| Better Archeology | 7.5M | Khám phá lăng mộ cổ, khai quật hóa thạch, thám hiểm di tích | Mod (.jar) | MIT | https://modrinth.com/mod/better-archeology | Hóa thạch xương khủng long khổng lồ, cổ vật chôn vùi, bình gốm cổ đại, bàn giám định |
| Decorative Blocks | 6.4M | Gia cố kiến trúc nhà xưởng, xà treo, công trình lớn | Mod (.jar) | MIT | https://modrinth.com/mod/decorative-blocks | Xà gỗ trợ lực chống trần, xích sắt treo, vạc lửa, cột đá chịu lực |
| Simple Hats | 6.1M | Hóa trang nhân vật, nghề nghiệp, trang phục hoạt hình | Mod (.jar) | Multiple | https://modrinth.com/mod/simple-hats | Mũ thám tử, mũ cảnh sát tuần tra, mũ bảo hộ công trình, mũ đầu bếp, mũ len |
| Ad Astra | 6.0M | Cơ sở không gian, bệ phóng rocket, phòng lab NASA | Mod (.jar) | Terrarium | https://modrinth.com/mod/ad-astra | Bàn kỹ thuật NASA, bệ phóng tên lửa khổng lồ, cửa khoang kín khí airlock, tấm pin năng lượng |
| SecurityCraft | 5.9M | Lối đi bảo mật, nhà tù, căn cứ bí mật, lồng giam | Mod (.jar) | MIT | https://modrinth.com/mod/security-craft | Cửa sắt bấm mã, bảng phím số, còi báo động, máy quét, lồng giam an ninh |
| Small Ships | 5.6M | Đại cảnh bến cảng, hải chiến, thám hiểm đại dương | Mod (.jar) | All Rights Reserved | https://modrinth.com/mod/small-ships | Thuyền buồm hai cột, thuyền chiến đại bác, bè nổi di chuyển trên mặt nước |
| Automobility | 5.6M | Giao thông đô thị, rượt đuổi đường phố, bãi đỗ xe | Mod (.jar) | MIT | https://modrinth.com/mod/automobility | Khung gầm ô tô, xe địa hình, lốp cao su, vô lăng, động cơ, biển báo phân làn |
| CC: Tweaked | 5.3M | Phòng máy chủ AI, trung tâm điều khiển, màn hình vi tính | Mod (.jar) | MPL-2.0 | https://modrinth.com/mod/cc-tweaked | Máy tính để bàn, cụm màn hình lớn, modem mạng, loa phát tín hiệu, ổ đĩa |
| The Man From The Fog | 5.0M | Phim kinh dị, thực thể bóng đêm, rượt đuổi giật gân | Mod (.jar) | All Rights Reserved | https://modrinth.com/mod/the-man-from-the-fog | Thực thể bóng đen lẩn khuất trong màn sương mù dày đặc, ánh mắt phát sáng ma quái |
| Numismatic Overhaul | 4.8M | Cảnh giao dịch tiền mặt, mua bán, tích trữ tài sản | Mod (.jar) | MIT | https://modrinth.com/mod/numismatic-overhaul | Cọc tiền xu đồng, bạc, vàng sáng bóng và túi da đựng tiền |
| Macaw's Lights and Lamps | 4.2M | Chiếu sáng đô thị, đèn đường phố, đèn trang trí trần | Mod (.jar) | All Rights Reserved | https://modrinth.com/mod/macaws-lights-and-lamps | Cột đèn đường cao áp, đèn gắn tường công nghiệp, đèn chùm hiện đại, đèn lồng giấy |
| Mekanism | 3.9M | Phòng thí nghiệm sci-fi, máy móc lượng tử, bồn hóa chất | Mod (.jar) | MIT | https://modrinth.com/mod/mekanism | Bồn hóa chất, máy phân tách phân tử, máy phát laser, tủ điều khiển bo mạch |
| Dusty Decorations | 3.5M | Hiện trường bỏ hoang, căn phòng bám bụi, kho hàng cũ | Mod (.jar) | MIT | https://modrinth.com/mod/dusty-decorations | 370 khối đạo cụ bám bụi: xà ngang, giá kệ, thùng hàng, rổ đan, đệm ngồi |
| Lightman's Currency | 3.4M | Cảnh rút tiền ngân hàng, quầy thu ngân, tài chính hiện đại | Mod (.jar) | Apache-2.0 | https://modrinth.com/mod/lightmans-currency | Cây ATM rút tiền, máy tính tiền quầy thu ngân, két sắt bảo mật, máy bán hàng tự động |
| Superb Warfare | 3.4M | Khí tài quân sự hạng nặng, pháo kích, bệ rocket vác vai | Mod (.jar) | GPL-3.0 | https://modrinth.com/mod/superb-warfare | Pháo cối hạng nặng, bệ phóng rocket vác vai, súng máy gắn bệ, lựu đạn khói |
| Refined Storage | 3.0M | Tủ rack máy chủ AI, trung tâm dữ liệu, mạng lưới cáp server | Mod (.jar) | MIT | https://modrinth.com/mod/refined-storage | Tủ rack ổ cứng server đèn LED nhấp nháy, màn hình lưới dữ liệu, dây cáp mạng |
| Immersive Weathering | 2.9M | Cảnh quan thời gian trôi, rêu phong cổ kính, rỉ sét tàn tích | Mod (.jar) | LGPL-3.0 | https://modrinth.com/mod/immersive-weathering | Rêu phong bám tường đá, gỉ sét loang lổ trên kim loại, nứt vỡ gạch theo thời gian |
| RAY's 3D Ladders | 2.8M | Cảnh leo trèo thoát hiểm, giếng trời, hầm thông gió có chiều sâu | Resource Pack (.zip) | MIT | https://modrinth.com/resourcepack/rays-3d-ladders | Thang leo 3D chân thực, thanh ngang tròn nổi khối thay cho decal phẳng |
| Eureka! Ships | 2.8M | Tàu bay cơ khí, tàu thám hiểm tự chế, vật lý nổi | Mod (.jar) | Apache-2.0 | https://modrinth.com/mod/eureka | Vô lăng tàu thủy, động cơ hơi nước, mỏ neo và bong bóng nâng khí cầu |
| Modern Industrialization | 2.0M | Đại cảnh nhà máy ngầm, cơ sở hạt nhân, bồn bể công nghiệp nặng | Mod (.jar) | MIT | https://modrinth.com/mod/modern-industrialization | Cụm máy hơi nước, tuabin điện, đường ống dẫn chất lỏng, lò phản ứng hạt nhân |
| Immersive Portals | 1.9M | Cổng không gian vô cực, gương soi phòng, bẻ cong không gian | Mod (.jar) | Apache-2.0 | https://modrinth.com/mod/immersiveportals | Cổng dịch chuyển tức thời nhìn xuyên thấu, gương soi phản chiếu, không gian phi Euclid |
| Weather Storms & Tornadoes | 1.9M | Thảm họa thiên nhiên, bão lốc tàn phá, tình huống khẩn cấp | Mod (.jar) | All Rights Reserved | https://modrinth.com/mod/weather-storms-tornadoes | Lốc xoáy F1-F5 cuốn phăng công trình, bão cát sa mạc, hệ thống còi báo động rú vang |
| [Let's Do] Bakery | 1.7M | Tiệm bánh ngọt, bữa tiệc sinh nhật, quầy cafe sáng | Mod (.jar) | Custom | https://modrinth.com/mod/lets-do-bakery | Quầy bánh ngọt, lò nướng bánh mì, bánh sinh nhật, bánh cupcake trang trí |
| [Let's Do] Candlelight | 1.5M | Bữa tối nến lãng mạn, nhà hàng cafe, tiệc rượu | Mod (.jar) | Custom | https://modrinth.com/mod/lets-do-candlelight | Bàn ăn nến lãng mạn, đĩa thức ăn chế biến sẵn, ly cafe, bộ đồ ăn quý tộc |
| Create Nuclear | 1.1M | Thảm họa nổ hạt nhân, nhà máy điện nguyên tử, phóng xạ sci-fi | Mod (.jar) | LGPL-3.0 | https://modrinth.com/mod/createnuclear | Lò phản ứng hạt nhân uranium, thanh nhiên liệu phát sáng, lõi làm mát, ống dẫn phóng xạ |
| FirstAid | 667K | Hộp sơ cứu dã chiến, băng bó vết thương, cấp cứu sinh tồn | Mod (.jar) | GPL-3.0 | https://modrinth.com/mod/firstaid | Hộp cứu thương medkit, cuộn băng gạc y tế, nẹp gãy xương, ống tiêm morphin |
| Underground Bunkers | 644K | Boong-ke ngầm Fallout, hầm trú ẩn tận thế, căn cứ ngầm | Mod (.jar) | All Rights Reserved | https://modrinth.com/mod/underground-bunkers | Hầm ngầm trú ẩn chống phóng xạ, cửa vòm xoay thép tròn nặng, giường tầng, kho đồ hộp |
| Fossils and Archeology: Revival | 583K | Viện bảo tàng tiền sử, công viên kỷ Jura, hồi sinh sinh vật cổ | Mod (.jar) | Custom | https://modrinth.com/mod/fossils-and-archeology-revival | Bàn chiết xuất DNA cổ đại, máy ấp phôi trứng khủng long, hóa thạch trưng bày bảo tàng |
| Etched | 462K | Phòng nhạc cổ điển, máy quay đĩa than, giai điệu hoài niệm | Mod (.jar) | GPL-3.0 | https://modrinth.com/mod/etched | Máy phát đĩa than vinyl bằng gỗ cổ điển, đĩa than xoay tròn phát nhạc chân thực |
| Actually 3D Blocks & Items | 284K | Đạo cụ tài liệu trên bàn, đồ vật cầm tay, sách vở | Resource Pack (.zip) | CC-BY-4.0 | https://modrinth.com/resourcepack/actually-3d-blocks-and-items | Mô hình 3D cho các vật phẩm cầm tay, sách vở tài liệu đặt trên bàn, dụng cụ |
| NhatJS Furniture Mod | 122K | Bàn làm việc tối giản, diễn cảnh cạy tủ văn phòng, góc máy tính | Mod (.jar) | MIT | https://modrinth.com/mod/nhatjs-furniture-mod | Bàn làm việc đen, ngăn kéo đơn lẻ, ghế văn phòng, thùng máy tính, cụm màn hình bật tắt |
| Modern Furniture | 108K | Văn phòng công nghệ cao, trần nhà hiện đại, không gian làm việc sạch | Mod (.jar) | CC-BY-4.0 | https://modrinth.com/mod/modern-furniture | 437 khối nội thất hiện đại: ghế công thái học, đèn ốp trần, bàn đứng, điều hòa |
| Simplistic 3D Doors | 22K | Cửa sắt và cửa sập phòng giam dày dặn bắt sáng nổi khối | Resource Pack (.zip) | CC0-1.0 | https://modrinth.com/resourcepack/simplistic-3d-doors | Cửa sắt và cửa sập sắt 3D nổi khối, dùng lại ảnh gốc từ client.jar |
| Hospitals - Medical Blocks & Items | 16K | Phòng mổ bệnh viện, khu xét nghiệm vô trùng, cấp cứu lâm sàng | Mod (.jar) | MIT | https://modrinth.com/mod/hospitals | Máy gây mê, máy ly tâm xét nghiệm, bảng điều khiển đầu giường, bàn phẫu thuật inox, cọc truyền dịch |
| Artemis Laboratory Blocks | 13K | Phòng nghiên cứu sinh hóa, cửa kính vi tính, phòng sạch cách âm | Mod (.jar) | MIT | https://modrinth.com/mod/artemis-laboratory-blocks | 100 khối phòng thí nghiệm: ống thông gió, màn hình vi tính, ốp tường cách âm |
| CCTV Camera | 4.8K | Góc máy giám sát an ninh, camera quan sát phòng giam | Resource Pack (.zip) | All Rights Reserved | https://modrinth.com/resourcepack/cctv-camera | Mô hình 3D camera giám sát CCTV góc tường, mắt kính lồi bảo mật cao |
