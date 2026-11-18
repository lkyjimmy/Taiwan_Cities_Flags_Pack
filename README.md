# ETS2 旗幟配件模組 — 開發者技術說明文件 (Taiwan Cities Window Flags Pack)

## 1. 模組概覽與源碼目錄結構

本模組（**Taiwan Cities Window Flags Pack**，製作：**通番救國政治部 / PDSNCF / Political Department of Saving the Nation by Colluding with Foreigners**）為《歐洲卡車模擬 2》（Euro Truck Simulator 2）的台灣 22 縣市車窗旗幟配件包，同時支援官方卡車與官方客車（Coaches DLC）。源碼根目錄為 `Taiwan_Cities_Flags_Pack/`：

```text
Taiwan_Cities_Flags_Pack/
├── LICENSE                             # 授權條款文件
├── README.md                           # 開發者技術說明文件 (Markdown)
├── README.txt                          # 純文字版說明文件
├── mod_icon.jpg                        # 模組縮圖 (276x162 JPG 格式)
├── Taiwan_Window_Flags_Pack.sh         # 全自動檢查、補齊材質與雙軌打包腳本
├── img/                                # 原始向量與高解析度縣市旗幟素材 (.svg / .jpg)
├── material/ui/accessory/flag/         # 改裝介面 UI 圖示 (flag_tw*.dds, .mat, .tobj)
└── vehicle/truck/upgrade/flag/         # 3D 旗幟模型貼圖 (tw*.dds, *.mat, tw*.tobj)
```

*(註：執行 `.sh` 打包腳本後，會自動生成 `def/` 定義檔、本地測試用 `Taiwan_Window_Flags_Pack.scs`，以及可直接交由 SCS Workshop Uploader 上傳的 `Taiwan_Window_Flags_Pack_Workshop/` 目錄。)*

---

## 2. 二進位檔案與圖片資源規格

模組內的圖片資源分為 **3D 實體貼圖** 與 **改裝選單 UI 圖示** 兩大類，皆包含 `.dds`（DirectDraw Surface 紋理檔）、`.tobj`（SCS 紋理物件二進位索引檔）與 `.mat`（材質定義檔）。

### A. 台灣 22 縣市旗幟代號對照表（22 組獨立樣式）

本模組採用台灣各縣市標準英文代碼（`{代號}`）作為配件定義檔與單元 ID，並在 3D 與 UI 貼圖檔案加上 `tw` 前綴（`tw{代號}` / `flag_tw{代號}`）以避免與其他地區旗幟衝突：

| 縣市名稱 | 內部代號 (ID) | 配件定義檔 (`def/.../accessory/`) | 3D 實體貼圖 (`vehicle/truck/upgrade/flag/`) | UI 選單圖示 (`material/ui/accessory/flag/`) |
| :--- | :--- | :--- | :--- | :--- |
| 臺北市 | **`tpe`** | `tpe_l.sii` / `tpe_r.sii` | `twtpe.dds` / `twtpe.tobj` / `tpe.mat` | `flag_twtpe.dds` / `.tobj` / `.mat` |
| 新北市 | **`nwt`** | `nwt_l.sii` / `nwt_r.sii` | `twnwt.dds` / `twnwt.tobj` / `nwt.mat` | `flag_twnwt.dds` / `.tobj` / `.mat` |
| 桃園市 | **`tao`** | `tao_l.sii` / `tao_r.sii` | `twtao.dds` / `twtao.tobj` / `tao.mat` | `flag_twtao.dds` / `.tobj` / `.mat` |
| 臺中市 | **`txg`** | `txg_l.sii` / `txg_r.sii` | `twtxg.dds` / `twtxg.tobj` / `txg.mat` | `flag_twtxg.dds` / `.tobj` / `.mat` |
| 臺南市 | **`tnn`** | `tnn_l.sii` / `tnn_r.sii` | `twtnn.dds` / `twtnn.tobj` / `tnn.mat` | `flag_twtnn.dds` / `.tobj` / `.mat` |
| 高雄市 | **`khh`** | `khh_l.sii` / `khh_r.sii` | `twkhh.dds` / `twkhh.tobj` / `khh.mat` | `flag_twkhh.dds` / `.tobj` / `.mat` |
| 基隆市 | **`kee`** | `kee_l.sii` / `kee_r.sii` | `twkee.dds` / `twkee.tobj` / `kee.mat` | `flag_twkee.dds` / `.tobj` / `.mat` |
| 新竹市 | **`hsz`** | `hsz_l.sii` / `hsz_r.sii` | `twhsz.dds` / `twhsz.tobj` / `hsz.mat` | `flag_twhsz.dds` / `.tobj` / `.mat` |
| 嘉義市 | **`cyi`** | `cyi_l.sii` / `cyi_r.sii` | `twcyi.dds` / `twcyi.tobj` / `cyi.mat` | `flag_twcyi.dds` / `.tobj` / `.mat` |
| 新竹縣 | **`hsq`** | `hsq_l.sii` / `hsq_r.sii` | `twhsq.dds` / `twhsq.tobj` / `hsq.mat` | `flag_twhsq.dds` / `.tobj` / `.mat` |
| 苗栗縣 | **`mia`** | `mia_l.sii` / `mia_r.sii` | `twmia.dds` / `twmia.tobj` / `mia.mat` | `flag_twmia.dds` / `.tobj` / `.mat` |
| 彰化縣 | **`cha`** | `cha_l.sii` / `cha_r.sii` | `twcha.dds` / `twcha.tobj` / `cha.mat` | `flag_twcha.dds` / `.tobj` / `.mat` |
| 南投縣 | **`nan`** | `nan_l.sii` / `nan_r.sii` | `twnan.dds` / `twnan.tobj` / `nan.mat` | `flag_twnan.dds` / `.tobj` / `.mat` |
| 雲林縣 | **`yun`** | `yun_l.sii` / `yun_r.sii` | `twyun.dds` / `twyun.tobj` / `yun.mat` | `flag_twyun.dds` / `.tobj` / `.mat` |
| 嘉義縣 | **`cyq`** | `cyq_l.sii` / `cyq_r.sii` | `twcyq.dds` / `twcyq.tobj` / `cyq.mat` | `flag_twcyq.dds` / `.tobj` / `.mat` |
| 屏東縣 | **`pif`** | `pif_l.sii` / `pif_r.sii` | `twpif.dds` / `twpif.tobj` / `pif.mat` | `flag_twpif.dds` / `.tobj` / `.mat` |
| 宜蘭縣 | **`ila`** | `ila_l.sii` / `ila_r.sii` | `twila.dds` / `twila.tobj` / `ila.mat` | `flag_twila.dds` / `.tobj` / `.mat` |
| 花蓮縣 | **`hua`** | `hua_l.sii` / `hua_r.sii` | `twhua.dds` / `twhua.tobj` / `hua.mat` | `flag_twhua.dds` / `.tobj` / `.mat` |
| 臺東縣 | **`ttt`** | `ttt_l.sii` / `ttt_r.sii` | `twttt.dds` / `twttt.tobj` / `ttt.mat` | `flag_twttt.dds` / `.tobj` / `.mat` |
| 澎湖縣 | **`pen`** | `pen_l.sii` / `pen_r.sii` | `twpen.dds` / `twpen.tobj` / `pen.mat` | `flag_twpen.dds` / `.tobj` / `.mat` |
| 金門縣 | **`kin`** | `kin_l.sii` / `kin_r.sii` | `twkin.dds` / `twkin.tobj` / `kin.mat` | `flag_twkin.dds` / `.tobj` / `.mat` |
| 連江縣 | **`lie`** | `lie_l.sii` / `lie_r.sii` | `twlie.dds` / `twlie.tobj` / `lie.mat` | `flag_twlie.dds` / `.tobj` / `.mat` |

### B. 圖片格式與尺寸規範（供再開發替換用）

以下為 SCS 引擎的標準開發規範與檔案特徵說明：

* **3D 旗幟實體貼圖 (`*.dds`)**：採用 DXT5 (BC3) 壓縮格式（支援 Alpha 透明通道），標準 2 的次方比例（建議 `512x256` 或 `1024x512` 像素，視長寬比而定），需包含 Mipmaps。
* **UI 配件圖示 (`flag_*.dds`)**：採用無壓縮 A8R8G8B8 或 DXT5 格式，SCS 改裝介面標準尺寸為 `256x64` 像素（不含 Mipmaps）。
* **模組預覽圖 (`mod_icon.jpg`)**：標準 JPEG 格式，SCS 官方規定尺寸必須精準為 `276x162` 像素。
* **二進位索引檔 (`*.tobj`)**：包含對應 `.dds` 檔案的相對路徑字串與 SCS 官方標準 40-byte 二進位檔頭。透過自動化打包腳本執行時，系統會自動根據貼圖類型生成對應的 `.tobj` 與 `.mat` 檔案。

---

## 3. 支援車輛清單（Def 定義檔架構）

本模組透過自動化腳本在 `def/vehicle/` 下為每款車輛分別建立了左側（`accessory/flag_l/{代號}_l.sii`）與右側（`accessory/flag_r/{代號}_r.sii`）的配件掛載定義（共 26 款卡車 + 3 款客車）：

### 卡車系列 (`def/vehicle/truck/`)
* **DAF**：`daf.xf`、`daf.xf_euro6`、`daf.2021`、`daf.xd`
* **Iveco**：`iveco.stralis`、`iveco.hiway`、`iveco.sway`
* **MAN**：`man.tgx`、`man.tgx_euro6`、`man.tgx_2020`
* **Mercedes-Benz**：`mercedes.actros`、`mercedes.actros2014`、`mercedes.newactros`
* **Renault**：`renault.magnum`、`renault.premium`、`renault.t`、`renault.etech_t`
* **Scania**：`scania.r`、`scania.streamline`、`scania.r_2016`、`scania.s_2016`、`scania.25l`
* **Volvo**：`volvo.fh16`、`volvo.fh16_2012`、`volvo.fh_2021`、`volvo.fh_2024`

### 客車系列 (`def/vehicle/bus/`)
* **MAN**：`man.lions_24` (MAN Lion's Coach)
* **Scania**：`scania.touring_23` (Scania Touring)
* **Volvo**：`volvo.9700_23` (Volvo 9700 DD)

*(註：使用本模組需擁有並安裝官方「Euro Truck Simulator 2 - Window Flags」DLC；另目前版本暫不支援 DAF NGD、MAN TGX 新世代部分車型及 Volvo FH5 獨立架構)。*

---

## 4. 二次開發與自動化打包指南

1. **替換旗幟圖案**：直接覆蓋 `vehicle/truck/upgrade/flag/` 與 `material/ui/accessory/flag/` 下對應代號的 `.dds` 檔案即可。
2. **新增旗幟或支援車型**：直接編輯打包腳本中的 `flag_names`、`all_trucks` 或 `all_buses` 陣列，填入目標代號（注意 ETS2 引擎限制單一配件 ID 長度不得超過 12 個字元）。
3. **一鍵自動化生成與雙軌封裝**：
   * 在 Linux / macOS 終端機或 Windows Git Bash / WSL 環境中執行 `chmod +x *.sh && ./<腳本名稱>.sh`。
   * 腳本執行時會自動進行 **DDS 貼圖完整性檢查**、`mod_icon.jpg`（`276x162` JPEG）自動驗證與縮放修復、補齊所有 `.mat` 與官方標準二進位 `.tobj` 檔，並同步輸出本地測試用的 `.scs` 模組與 Steam Workshop 專用上傳目錄（內含 `versions.sii` 與 `universal/`）。
