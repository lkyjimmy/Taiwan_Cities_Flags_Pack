# ETS2 台灣縣市旗幟配件模組 — 開發者技術說明文件 (Developer README)

## 1. 模組概覽與目錄結構

本模組為《歐洲卡車模擬 2》（Euro Truck Simulator 2）的台灣 22 縣市車窗旗幟配件包，同時支援官方卡車與官方客車（Coaches DLC）。模組採用標準的 SCS 封裝結構（根目錄為 `Taiwan_Cities_Flags_Pack/`）：

```text
Taiwan_Cities_Flags_Pack/
├── versions.sii                        # 遊戲版本相容性清單
└── universal/                          # 通用版本資源目錄
    ├── manifest.sii                    # 模組基本資訊與描述設定
    ├── mod_description.txt             # 模組商店/管理員顯示文字
    ├── mod_icon.jpg                    # 模組縮圖 (JPG 格式)
    ├── Taiwan_Window_Flags_Pack.scs    # 封裝檔案/備份
    ├── Taiwan_Window_Flags_Pack.sh     # 打包腳本 (Shell Script)
    ├── def/vehicle/                    # 車輛配件定義檔 (.sii)
    ├── img/                            # 原始向量與圖片素材 (.svg, .jpg)
    ├── material/ui/accessory/flag/     # 改裝介面 UI 圖示 (.dds, .mat, .tobj)
    └── vehicle/truck/upgrade/flag/     # 3D 旗幟模型貼圖 (.dds, .mat, .tobj)
```

---

## 2. 二進位檔案與圖片資源規格

模組內的圖片資源分為 **3D 實體貼圖** 與 **改裝選單 UI 圖示** 兩大類，皆包含 `.dds`（DirectDraw Surface 紋理檔）、`.tobj`（SCS 紋理物件二進位索引檔）與 `.mat`（材質定義檔）。

### A. 旗幟代號對照表（台灣 22 縣市樣式）

為避免與其他旗幟模組（如 `Un-CCP_Flags_Collection_Pack`）產生 ID 衝突，本模組直接採用各縣市三位英文代碼作為配件定義檔（`{代號}_l.sii` / `{代號}_r.sii`）與材質檔名稱，3D 實體貼圖與原始素材則統一加上 `tw` 前綴：

| 縣市名稱 | 內部代號 (ID) | 3D 實體貼圖路徑 (`vehicle/truck/upgrade/flag/`) | UI 選單圖示路徑 (`material/ui/accessory/flag/`) |
| :--- | :--- | :--- | :--- |
| **臺北市** | `tpe` | `twtpe.dds` / `twtpe.tobj` / `tpe.mat` | `flag_twtpe.dds` / `flag_tpe.tobj` / `.mat` |
| **新北市** | `nwt` | `twnwt.dds` / `twnwt.tobj` / `nwt.mat` | `flag_twnwt.dds` / `flag_nwt.tobj` / `.mat` |
| **桃園市** | `tao` | `twtao.dds` / `twtao.tobj` / `tao.mat` | `flag_twtao.dds` / `flag_tao.tobj` / `.mat` |
| **臺中市** | `txg` | `twtxg.dds` / `twtxg.tobj` / `txg.mat` | `flag_twtxg.dds` / `flag_txg.tobj` / `.mat` |
| **臺南市** | `tnn` | `twtnn.dds` / `twtnn.tobj` / `tnn.mat` | `flag_twtnn.dds` / `flag_tnn.tobj` / `.mat` |
| **高雄市** | `khh` | `twkhh.dds` / `twkhh.tobj` / `khh.mat` | `flag_twkhh.dds` / `flag_khh.tobj` / `.mat` |
| **基隆市** | `kee` | `twkee.dds` / `twkee.tobj` / `kee.mat` | `flag_twkee.dds` / `flag_kee.tobj` / `.mat` |
| **新竹市** | `hsz` | `twhsz.dds` / `twhsz.tobj` / `hsz.mat` | `flag_twhsz.dds` / `flag_hsz.tobj` / `.mat` |
| **嘉義市** | `cyi` | `twcyi.dds` / `twcyi.tobj` / `cyi.mat` | `flag_twcyi.dds` / `flag_cyi.tobj` / `.mat` |
| **新竹縣** | `hsq` | `twhsq.dds` / `twhsq.tobj` / `hsq.mat` | `flag_twhsq.dds` / `flag_hsq.tobj` / `.mat` |
| **苗栗縣** | `mia` | `twmia.dds` / `twmia.tobj` / `mia.mat` | `flag_twmia.dds` / `flag_mia.tobj` / `.mat` |
| **彰化縣** | `cha` | `twcha.dds` / `twcha.tobj` / `cha.mat` | `flag_twcha.dds` / `flag_cha.tobj` / `.mat` |
| **南投縣** | `nan` | `twnan.dds` / `twnan.tobj` / `nan.mat` | `flag_twnan.dds` / `flag_nan.tobj` / `.mat` |
| **雲林縣** | `yun` | `twyun.dds` / `twyun.tobj` / `yun.mat` | `flag_twyun.dds` / `flag_yun.tobj` / `.mat` |
| **嘉義縣** | `cyq` | `twcyq.dds` / `twcyq.tobj` / `cyq.mat` | `flag_twcyq.dds` / `flag_cyq.tobj` / `.mat` |
| **屏東縣** | `pif` | `twpif.dds` / `twpif.tobj` / `pif.mat` | `flag_twpif.dds` / `flag_pif.tobj` / `.mat` |
| **宜蘭縣** | `ila` | `twila.dds` / `twila.tobj` / `ila.mat` | `flag_twila.dds` / `flag_ila.tobj` / `.mat` |
| **花蓮縣** | `hua` | `twhua.dds` / `twhua.tobj` / `hua.mat` | `flag_twhua.dds` / `flag_hua.tobj` / `.mat` |
| **臺東縣** | `ttt` | `twttt.dds` / `twttt.tobj` / `ttt.mat` | `flag_twttt.dds` / `flag_ttt.tobj` / `.mat` |
| **澎湖縣** | `pen` | `twpen.dds` / `twpen.tobj` / `pen.mat` | `flag_twpen.dds` / `flag_pen.tobj` / `.mat` |
| **金門縣** | `kin` | `twkin.dds` / `twkin.tobj` / `kin.mat` | `flag_twkin.dds` / `flag_kin.tobj` / `.mat` |
| **連江縣** | `lie` | `twlie.dds` / `twlie.tobj` / `lie.mat` | `flag_twlie.dds` / `flag_lie.tobj` / `.mat` |

### B. 圖片格式與尺寸規範（供再開發替換用）

以下為 SCS 引擎的標準開發規範與檔案特徵說明：

* **3D 旗幟實體貼圖 (`tw*.dds`)**：採用 DXT5 (BC3) 壓縮格式（支援 Alpha 透明通道），標準 2 的次方比例（建議 `512x256` 或 `1024x512` 像素，視長寬比而定），需包含 Mipmaps。
* **UI 配件圖示 (`flag_tw*.dds`)**：採用無壓縮 A8R8G8B8 或 DXT5 格式，SCS 改裝介面標準尺寸為 `256x64` 像素（不含 Mipmaps）。
* **原始向量/圖片源檔 (`universal/img/`)**：保留全台灣 22 縣市旗幟的原始向量檔（`.svg`，其中臺中市為 `twtxg.jpg`），方便後續匯出高解析度貼圖。
* **模組預覽圖 (`mod_icon.jpg`)**：標準 JPEG 格式，SCS 官方規定尺寸必須為 `276x162` 像素。
* **二進位索引檔 (`*.tobj`)**：包含對應 `.dds` 檔案的相對路徑字串與紋理定址模式（如 `clamp_to_edge`）。若第三方開發者修改檔名，必須使用 TOBJ 編輯器同步修改內部路徑指針，否則遊戲將顯示紫紅色遺失貼圖。

---

## 3. 支援車輛清單（Def 定義檔架構）

本模組在 `universal/def/vehicle/` 下為每款車輛分別建立了左側（`accessory/flag_l/{代號}_l.sii`）與右側（`accessory/flag_r/{代號}_r.sii`）的配件掛載定義（共 26 款卡車 + 3 款客車）：

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

## 4. 二次開發與擴充指南

1. **替換旗幟圖案**：直接覆蓋 `vehicle/truck/upgrade/flag/`（如 `twtpe.dds`）與 `material/ui/accessory/flag/`（如 `flag_twtpe.dds`）下對應代號的 `.dds` 檔案即可，無需更動 `.mat`、`.tobj` 或 `.sii` 結構。
2. **新增支援車型（如模組卡車或客車）**：
   * 直接編輯 `universal/Taiwan_Window_Flags_Pack.sh` 中的 `all_trucks` 或 `all_buses` 陣列，填入目標車輛的內部代號並重新執行腳本即可自動生成所有 `.sii` 定義檔。
3. **封裝打包**：目錄內附有 `Taiwan_Window_Flags_Pack.sh` 腳本，開發者在 Linux/macOS 環境或 Windows Git Bash / WSL 下可直接執行該腳本進行自動化補齊材質與打包（採用 `zip -0` 無壓縮 Store 模式封裝為 `Taiwan_Window_Flags_Pack.scs` 以確保遊戲讀取效能）。
