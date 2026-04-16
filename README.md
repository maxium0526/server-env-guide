# Docker 環境使用說明

每位學生在服務器上都會有一個Docker container環境（下稱環境），每個環境像是一台linux系統一樣，每個環境之間是互相獨立的，都有獨立的port口、儲存空間、帳戶和密碼，因此，學生無法存取到其他人的環境。

在管理員部署好屬於你的環境後，會給予你以下資訊以作連接：

- `服務器的IP`
- `環境的SSH 端口`
- `環境的SSH 帳號`
- `環境的SSH 初始密碼`
- `環境的node-server 端口`
- `環境的jupyter 端口`

## 與服務器建立連線

請聯繫服務器管理員。

## 連接到環境

環境可以使用SSH連接，像連線到Linux系統一樣。每個環境都有獨立的SSH port。連線資料如下：

- IP and port: `服務器的IP`:`環境的SSH 端口`
- username: `環境的SSH 帳號`
- password: `環境的SSH 初始密碼`

**請第一次連接到環境後立即更改密碼，如下說明**。

## 更改SSH 密碼

通過 SSH 連接到環境後，可以使用指令 `env-change-ssh-passwd` 更改SSH密碼。新密碼將在重啟環境後生效。

## 重啟環境

通過 SSH 連接到環境後，可以使用指令 `env-restart` 重啟環境。重啟環境會導致所講運行中的代碼中斷並無法復原！

## 環境變更

學生可以在環境內自行安裝實驗需要使用的軟件（禁止挖礦、網絡相關軟件），但其將會在重設環境後消失。

## 重設環境

若環境因各種原因（e.g., 錯誤安裝軟件）出現損壞，可向管理員提出重設環境。重設環境會導致所有資料消失！（以下兩個位置除外）

## 資料儲存

環境內有兩個資料夾提供資料儲存，這兩個資料夾內的資料不會因重設環境而消失，而在其他資料夾的資料將在重設後消失。

### `/datasets`

`/datasets`資料夾掛載到服務器的SSD上以提供高速資料讀取。然而SSD空間有限，請只把數據集等需要高速讀取等資料放在這裡，避免將實驗數據等放在這裡。

### `/workspace`

`/workspace`資料夾掛載到服務器的HDD上提供大量儲存空間，請將實驗數據等放在這裡。

## 環境配置

預設的配置跟據環境的版本有所不同。

### v4.0b1-2501

- Ubuntu 24.04
- CUDA 12.8.0
- Pytorch 2.6
- Jupyter 4.5.2
- Code-server

### v2.4

- Ubuntu 20.04
- CUDA 12.0
- Pytorch 11.3
- Other python libraries: pytorch_lightning, torchmetrics, tensorboard
- Jupyter
- Code-server

## Jupyter 與 code-server

環境有內建Jupyter 與 code-server (網頁版VS Code)，學生可以在瀏覽器進入 Jupyter 或 code-server 來使用環境。連線方式如下：

- Jupyter 在瀏覽器輸入 "服務器的IP":"環境的jupyter 端口"
- code-server 在瀏覽器輸入 "服務器的IP":"環境的node-server 端口"

Jupyter 和 code-server 都受密碼保護，在第一次使用前，請在SSH中使用`env-change-jupyter-passwd`和`env-change-code-server-passwd` 指令更改密碼，新密碼將在重啟環境後生效。

## 其它

### 環境指令

- `env-restart`: 重啟環境
- `env-change-ssh-passwd`: 更改SSH密碼
- `env-change-jupyter-passwd`: 更改Jupyter密碼
- `env-change-code-server-passwd`: 更改 Code-server密碼
- `env-info`: 關於環境

### 疑難排解

#### 1. 找不到GPU，nvidia-smi顯示未知錯誤，或無法使用GPU訓練

這是因為未知原因導致環境與GPU間的連接失效，一般通過`env-restart`指令重啟環境即可解決。
