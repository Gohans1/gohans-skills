---
name: gohans-3js-videos-skills
description: Dùng khi cần biết Stack làm 3js videos của gohans cần những gì. Curated 64-repository Three.js and 3D video production tech stack with battle-tested libraries and a Before/After reference guide. Planning, building, rendering, reviewing, debugging, or advising on Three.js scenes, 3D explainer or documentary videos, WebCodecs MP4 export, camera math, glTF optimization, post-processing, ambient occlusion, lip-sync, 3D characters, audio loudness normalization, 2.5D parallax, geospatial maps, physics fracture, or Minecraft 3D films
license: MIT
---

# Overview
Khi dev muốn Separate Fresh Agent Review video -> dùng [references/gohans-separate-agent-review](./references/gohans-separate-agent-review.md)
Kiến trúc, thư viện & kho tài nguyên làm phim Minecraft 3D -> xem [references/gohans-3js-videos-minecraft](./references/gohans-3js-videos-minecraft.md)
# Gohans Three.js Third Party Stack
- chi tiết công năng, cách sử dụng, khi nào dùng, dùng thế nào, etc... Cho từng repo: [references/gohans-threejs-stack.md](./references/gohans-threejs-stack.md)
- Để sử dụng thực chiến/code thực sự -> ưu tiên research best-prarctice/latest để viết chuẩn nhất có thể

## Thực chiến cho mọi video all time
https://github.com/Vanilagy/mediabunny (https://mediabunny.dev/llms.txt; mediabunny.d.ts)
https://github.com/pmndrs/math (`math` skill)
https://github.com/donmccurdy/glTF-Transform
https://github.com/zeux/meshoptimizer
https://github.com/KhronosGroup/glTF-Validator
https://github.com/m-bain/whisperX
https://github.com/pmndrs/postprocessing
https://github.com/N8python/n8ao
https://github.com/csteinmetz1/pyloudnorm
https://github.com/slhck/ffmpeg-normalize
https://github.com/Netflix/vmaf
https://github.com/mapbox/pixelmatch
https://github.com/gkjohnson/three-mesh-bvh
https://github.com/Evercoder/culori
https://github.com/ashima/webgl-noise
https://github.com/protectwise/troika
https://github.com/lovell/sharp
https://github.com/yt-dlp/yt-dlp
https://github.com/Breakthrough/PySceneDetect

## 3d models & Characters
https://github.com/DanielSWolf/rhubarb-lip-sync
https://github.com/microsoft/Microsoft-Rocketbox

## Chủ đề tương lai rất có thể thích
https://github.com/sparkjsdev/spark
https://github.com/Alchemist0823/three.quarks
https://github.com/DepthAnything/Depth-Anything-V2
https://github.com/danielgatis/rembg
https://github.com/advimman/lama
https://github.com/vasturiano/three-forcegraph
https://github.com/vasturiano/three-globe
https://github.com/NASA-AMMOS/3DTilesRendererJS
https://github.com/maplibre/maplibre-gl-js
https://github.com/protomaps/PMTiles
https://github.com/Turfjs/turf
https://github.com/mapbox/supercluster
https://github.com/d3/d3
https://github.com/greensock/GSAP
https://github.com/takram-design-engineering/three-geospatial
https://github.com/dimforge/rapier/tree/master/typescript
https://github.com/dgreenheck/three-pinata
https://github.com/FarazzShaikh/THREE-CustomShaderMaterial
https://github.com/pmndrs/drei-vanilla
https://github.com/instruktlabs/kiln
https://github.com/nv-tlabs/kimodo

## Specific
### Minecraft
https://github.com/ewanhowell5195/block-model-renderer
https://github.com/InventivetalentDev/MineRender (https://beta-docs.minerender.org)
https://github.com/Moo-Ack-Productions/MCprep
https://github.com/JannisX11/wintersky
https://github.com/misode/deepslate
https://github.com/Schem-at/Nucleation
https://github.com/erich666/Mineways
https://github.com/Mojang/bedrock-samples
https://github.com/JannisX11/blockbench
https://github.com/jasonjgardner/blockbench-mcp-plugin

## Hiếm khi
https://github.com/nomadkaraoke/python-audio-separator
https://github.com/mikedh/trimesh
https://github.com/f3d-app/f3d
https://github.com/elalish/manifold
https://github.com/dgreenheck/ez-tree
https://github.com/gkjohnson/three-edge-projection
https://github.com/opentypejs/opentype.js
https://github.com/rough-stuff/rough
https://github.com/cosinekitty/astronomy
https://github.com/shashwatak/satellite-js
https://github.com/KhronosGroup/KTX-Software
https://github.com/agargaro/instanced-mesh

# Video editor tools 
- WebGL (không WebGPU)
- 3js

## Voice
- Dùng `ElevenLabs` v4 qua `genvoice.pro`. API/tham số/endpoint/etc... research nếu cần

### Audio Tags (research nếu cần)
- Không giới hạn danh sách cố định (*"There is no definitive ElevenLabs Audio Tags list"*): được tự chế vô hạn bằng ngôn ngữ tự nhiên trong ngoặc vuông `[...]`, ví dụ `[out of breath after running up the stairs]`, `[nervous, trying to sound confident]`.
- English Audio Tags only

### Giọng kể Ngôi thứ 3 (Fern / Atrium / Blackfiles)
- Hạng 1 (`Seff Echo - Cinematic Storyteller` — ID: `ZaZosYpkIGmSqOwAlfnk`):** Giọng dẫn chính ưu tiên số 1 (lai `Blackfiles × Atrium`). Phân khúc `PVC` (`professional` người thật thu phòng thu, `~2.5k` lượt dùng cực ít đụng hàng), giọng nam Mỹ trẻ `en-US`, `rate=1`, `notice_period=730` ngày, tắt kiểm duyệt ngầm (`live_moderation_enabled=null`), nhịp gốc chuẩn ngay trên `eleven_v4`.
- Hạng 2 (`Jake – Deep, Smooth, Dramatic` — ID: `ev2kMR9ZJZZsemuogS5u`):
- Hạng 3 (`True - Crime & Horror Narrator` — ID: `tZssYepgGaQmegsMEXjK`):

## SFX
Freesound API v2, CC0 1.0
Mixkit Free Sound Effects
Sonniss GDC Game Audio Archive
...
## Image
Dùng `codex` CLI để tạo ảnh nếu cần

# Inspired:
- Fern: https://www.youtube.com/@fern-tv
- Atrium: https://www.youtube.com/@AtriumExplores
- Primal Space: https://www.youtube.com/@primalspace