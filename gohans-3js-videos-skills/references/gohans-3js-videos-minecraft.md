# Minecraft 3D Video Architecture & Assets Guide

Tai lieu chuan ve kien truc tai nguyen, thu vien va quy trinh tich hop mo hinh Minecraft cho cac du an lam phim 3D bang Three.js.

## 1. Nguyen Tac Kho Tai Nguyen Tap Trung (Centralized Vault)

Khong luu tru truc tiep cac file jar game goc hoac file pack mod nang hang chuc megabyte vao trong repository code cua tung du an.

Mo hinh chuan:
- Mot kho tai nguyen ben ngoai dung chung: Chua client.jar goc, mcasset du lieu thuc the, rig nhan vat MCprep va cac goi mod hoac resource pack da tai.
- Moi du an lam phim chi trich xuat cuc bo: Khi kich ban can dao cu nao (vi du ban lam viec, ghe, cua sat), giai nen hoac copy dung file json mo hinh va file png texture tuong ung dua vao thu muc pack noi bo cua du an do.
- Loi ich: Dung luong du an nhe gon, tranh xung dot dinh danh giua cac mod, va giu ngu canh sach de AI khong bi nham lan giua hang ngan khoi gach khong lien quan.

## 2. Cac Tru Cot Ky Thuat

### block-model-renderer
- Vai tro: Dung toan bo the gioi khoi tinh, tuong nha, dia hinh, ban ghe, do dac va dao cu noi that.
- Diem manh: Doc truc tiep dinh dang Block JSON chuan (elements, from, to, faces). Tu dong tinh culling khu mat khuat, gop luoi toi uu hoa draw call va do bong chuan tung diem anh.
- Cach dung:
  - Nap the gioi: createScene([packHandler, clientJarBytes], blockList, { lighting: "scene" })
  - Nap dao cu cu dong rieng: loadModel(scene, [packHandler, clientJarBytes], modelData, { mergeElements: false }) de tach cac hop rieng biet cho phep xoay hoac truot bang code theo bien thoi gian t.

### MineRender
- Vai tro: Ve giao dien 2D, phong chu pixel Minecraft va hoat anh dong vat song.
- Diem manh:
  - GuiObject: In chu pixel chuan game (vi du nhan camera an ninh, phu de, ma phong) va cac bang giao dien hotbar, thanh mau len lop phu 2D.
  - EntityObject: Chua san 209 mo hinh sinh vat trich xuat tu Java code kem xuong va hoat anh buoc chan (walk cycle) tu nhien khop voi truc thoi gian.
- Cach dung:
  - Giao dien 2D: new GuiObject([{ text: [{ text: "CELL 0412", color: 0xffffff }], position: [10, 8] }])
  - Dong vat: new EntityObject("minecraft:cat") ket hop tham so thoi gian de buoc di theo nhip.

### MCprep (player.glb)
- Vai tro: Dien vien nguoi choi chinh (Steve, Alex hoac skin tuy bien).
- Diem manh: Khop uon cong khuyu tay va dau goi 90 do muot ma khong rach luoi, co san he thong xuong dieu khien mat, mieng va cu chi ngon tay.
- Ghi nhan quyen tac gia: BoxScape Studios va TheDuckCow theo giay phep CC-BY 3.0.

### Modrinth API
- Vai tro: Tim kiem va tai tai nguyen tu dong, sach ban quyen.
- Diem manh: API mo khong can khoa truy cap, ho tro loc theo giay phep thuong mai thoang (MIT, CC0, CC-BY-4.0).
- Endpoint tim kiem: https://api.modrinth.com/v2/search?query=KEYWORD&facets=[["license:MIT","license:CC0-1.0","license:CC-BY-4.0"],["project_type:mod","project_type:resourcepack"]]

## 3. Danh Muc Cac Goi Tai Nguyen Da Kiem Chung

Danh sach cac goi mo hinh chuan Block JSON co giay phep mo, tuong thich hoan toan voi Three.js va block-model-renderer:

| Goi | Dinh dang | Giay phep | Link tai / Trang chu | Cong nang chinh |
| --- | --- | --- | --- | --- |
| Simplistic 3D Doors | Resource Pack (.zip) | CC0-1.0 | https://modrinth.com/resourcepack/simplistic-3d-doors | Cua sat va cua sap sat 3D noi khoi, dung lai anh goc tu client.jar |
| NhatJS Furniture Mod | Mod (.jar) | MIT | https://modrinth.com/mod/nhatjs-furniture-mod | Ban lam viec den, ngan keo don le, ghe van phong, thung may tinh, cum man hinh bat tat |
| Modern Furniture | Mod (.jar) | CC-BY-4.0 | https://modrinth.com/mod/modern-furniture | 437 khoi noi that hien dai: ghe cong thai hoc, den op tran, ban dung, dieu hoa |
| Dusty Decorations | Mod (.jar) | MIT | https://modrinth.com/mod/dusty-decorations | 370 khoi dao cu bam bui: xa ngang, gia ke, thung hang, ro dan, dem ngoi |
| Decorative Blocks | Mod (.jar) | MIT | https://modrinth.com/mod/decorative-blocks | Xa go tro luc chong tran, xich sat treo, vac lua, cot da chiu luc |
| SecurityCraft | Mod (.jar) | MIT | https://modrinth.com/mod/security-craft | Cua sat bam ma, bang phim so, coi bao dong, may quet, long giam an ninh |
| Artemis Laboratory Blocks | Mod (.jar) | MIT | https://modrinth.com/mod/artemis-laboratory-blocks | 100 khoi phong thi nghiem: ong thong gio, man hinh vi tinh, op tuong cach am |
| Actually 3D Blocks & Items | Resource Pack (.zip) | CC-BY-4.0 | https://modrinth.com/resourcepack/actually-3d-blocks-and-items | Mo hinh 3D cho cac vat pham cam tay, sach vo tai lieu dat tren ban, dung cu |

## 4. Quy Trinh Trich Xuat Dao Cu Vao Du An

1. Xac dinh mon do can dung trong kich ban (vi du ban den black_desk).
2. Mo file nen .jar hoac .zip trong kho luu tru bang cong cu giai nen tieu chuan.
3. Tim den duong dan assets/<namespace>/models/block/ de lay file json mo hinh.
4. Tim den duong dan assets/<namespace>/textures/block/ de lay cac file anh png van be mat tuong ung.
5. Sao chep cac file nay vao thu muc pack/assets/ cua du an va dang ky vao bo nap mo hinh ao.
6. Goi ten khoi trong ham dung the gioi hoac ham loadModel de hien thi tren man hinh.
