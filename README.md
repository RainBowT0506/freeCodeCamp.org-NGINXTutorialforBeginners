Github：[freeCodeCamp.org-NGINXTutorialforBeginners](https://github.com/RainBowT0506/freeCodeCamp.org-NGINXTutorialforBeginners)

# What is NGINX

## NGINX 簡介

- NGINX 是一個開源的網頁伺服器軟體，常用於反向代理、負載平衡和快取。
- 對後端開發者來說，了解 NGINX 是非常重要的。

## NGINX 的運作方式

- 當你訪問 Airbnb.ca 時，瀏覽器會收到大量的內容，如圖片和文本，這些內容是通過網路請求從伺服器獲取的。
- 可以通過檢查瀏覽器的網路標籤來查看這些請求。
![CleanShot 2024-07-29 at 20.11.29](https://hackmd.io/_uploads/rJP-vbrKA.png)

## NGINX 的角色
![CleanShot 2024-07-29 at 20.11.57](https://hackmd.io/_uploads/HyjMw-BFA.png)

- 瀏覽器向伺服器發送請求，伺服器回應並提供網頁內容。
- 在此過程中，NGINX 充當反向代理，瀏覽器的請求先到達 NGINX，再由 NGINX 轉發給 Airbnb 伺服器，最後再由 NGINX 將回應傳回瀏覽器。
![CleanShot 2024-07-29 at 20.12.41](https://hackmd.io/_uploads/SkaBD-HY0.png)

- 這種結構稱為反向代理（Reverse Proxy）。

## 使用 NGINX 的好處

### 負載平衡
![CleanShot 2024-07-29 at 20.13.36](https://hackmd.io/_uploads/SJkYPWHK0.png)

- 當網站流量很大時，NGINX 可以將請求分配給多個伺服器，以減少單一伺服器的負載。
- NGINX 作為負載平衡器，能夠提高應用程式的擴展性和效率。

### 加密
![CleanShot 2024-07-29 at 20.14.20](https://hackmd.io/_uploads/r1uiv-HFC.png)

- 如果網站使用 HTTPS，表示伺服器加密和解密數據。
- NGINX 可以集中處理這些加密和解密過程，避免每個伺服器都需要單獨設置。
![CleanShot 2024-07-29 at 20.14.41](https://hackmd.io/_uploads/r1epwbSK0.png)

# NGINX Installation

## 安裝步驟

1. 打開終端機，執行 `brew install nginx`（需要先安裝 Homebrew）。
2. 安裝完成後，檢查 `cd /usr/local/etc/nginx` 目錄下的文件和資料夾。
* 可以使用 which nginx 命令來查看 Nginx 的安裝路徑。
```
which nginx
/opt/homebrew/bin/nginx
```
* Nginx 配置文件通常位於 /opt/homebrew/etc/nginx。
3. 你可以使用 ls 命令來列出目錄中的文件，確保存在 nginx.conf 配置文件。
```
fastcgi.conf		mime.types		servers
fastcgi.conf.default	mime.types.default	uwsgi_params
fastcgi_params		nginx.conf		uwsgi_params.default
fastcgi_params.default	nginx.conf.default	win-utf
koi-utf			scgi_params
koi-win			scgi_params.default
```

疑問：[為什麼安裝路徑 /opt/homebrew/bin/nginx 卻是使用 cd /opt/homebrew/etc/nginx？](https://hackmd.io/tqmS-QWjRfaY_rn9ilxIoQ#%E7%96%91%E5%95%8F)
## 配置 NGINX
- 使用 code . 命令後，VS Code 打開當前目錄
```
code .
zsh: command not found: code
```
- 設定 code 命令行工具
    * 打開 Visual Studio Code。
    * 按 Cmd+Shift+P 打開命令面板。
    * 輸入 `Shell Command: Install 'code' command in PATH`，並選擇該命令。
- 使用 VS Code 打開 NGINX 配置文件 `nginx.conf`。
- 這個文件是用來配置 NGINX 反向代理的核心文件。

## 啟動 NGINX

- 在終端機中執行 `nginx` 命令來啟動 NGINX。
- 打開瀏覽器並訪問 `localhost:8080`，你會看到 NGINX 已經啟動並在提供網頁內容。
![CleanShot 2024-07-29 at 20.30.53](https://hackmd.io/_uploads/HyJ5j-SFR.png)
![CleanShot 2024-07-29 at 20.32.06](https://hackmd.io/_uploads/rkrJhbrK0.png)

# NGINX Terminology
## 簡介
- 安裝並運行 NGINX
- 開始返回應用程式所需的文件和文件夾及圖像

## nginx.conf 文件
- 主要包含兩個部分：指令 (directives) 和上下文 (context)

## 指令 (Directives)
- 以鍵值對形式出現
- 例如：`worker_processes 1;` 和 `include mime.types;`

## 上下文 (Context)
- 以大括號包圍的代碼塊
- 例如：`events` 和 `http` 上下文
- 在上下文中包含特定的指令

## HTTP 上下文
- 定義 HTTP 服務器
- 包含配置服務器的指令

# Serving Static Content
## 步驟
1. 創建目錄並在 VS Code 中打開
2. 創建 `index.html` 文件，寫入簡單的 HTML 內容
3. 配置 NGINX 以服務該文件
3. 使用 `ngix -s reload` 重新加載 Server
![CleanShot 2024-07-30 at 10.41.33](https://hackmd.io/_uploads/ryj1X0rY0.png)
## 配置 NGINX
- 在 `nginx.conf` 文件中添加 HTTP 和 events 上下文
- 定義 server 上下文，並添加相關指令
  - `listen` 指令設定端口
  - `root` 指令設定文件路徑
- 重載 NGINX 配置使更改生效

# Mime Types
## 簡介
- 添加 CSS 文件，並在 HTML 中引用
- 遇到樣式未應用的問題，需配置 mime types
![CleanShot 2024-07-30 at 11.46.06](https://hackmd.io/_uploads/SkpzfJ8K0.png)

## 解決方案
- 檢查文件的 content type
- 配置 HTTP 上下文中的 mime types
  - 為不同的文件類型設置對應的 mime types

## 使用 NGINX 默認 mime types
- 使用 include 指令引入默認的 mime types 配置
- 重載 NGINX 配置使更改生效

# Location Context
## 簡介
- 介紹 location block 或 location context 的重要性
- 允許我們指定特定的端點和頁面

## 設置範例
1. 創建一個 fruits 目錄並在其中放置一個 index.html 文件
2. 配置 NGINX 以服務這個文件

## 配置 NGINX
- 在 server 上下文中使用 location 指令
  - `location /fruits` 設定路徑
  - 指定 root 目錄以服務文件
```
http {

    include mime.types;

    server {
        listen 8080;
        root /Users/userName/Desktop/mysite;

        location /fruits {
            root /Users/userName/Desktop/mysite;
        }
    }
}

events {}

```
- 重新加載 NGINX 配置
* http://localhost:8080/fruits/
## Alias 使用
- 當需要服務不同路徑但不希望附加原始路徑時使用 alias
```
http {

    include mime.types;

    server {
        location /carbs {
            alias /Users/userName/Desktop/mysite/fruits;
        }
    }
}

events {}
```
- 範例：`location /carbs` 使用 alias 指向 fruits 目錄
- 重新加載 NGINX 配置
* http://localhost:8080/carbs/
## 處理不同文件名
- 創建 vegetables 目錄並放置 veggies.html 文件
- 使用 try_files 指令指定不同的文件名
  - 順序嘗試指定的文件，若不存在則返回 404
```
2024/07/30 14:25:31 [error] 6622#0: *39 directory index of "/Users/userName/Desktop/mysite/vegetables/" is forbidden, client: 127.0.0.1, server: , request: "GET /vegetables/ HTTP/1.1", host: "localhost:8080"
```

```
http {

    include mime.types;

    server {
        location /vegetables{
            root /Users/rainbowt/Desktop/mysite;
            try_files /vegetables/veggies.html /index.html =404;
        }
    }
}

events {}

```
## 正則表達式匹配
- 在 location 中使用正則表達式
  - 例如：匹配 `/count/數字` 路徑
  - 使用 `try_files` 指定匹配的文件或返回 404
```
http {

    include mime.types;

    server {
        listen 8080;
        root /Users/rainbowt/Desktop/mysite;

        location ~* /count/[0-9] {
            root /Users/rainbowt/Desktop/mysite;
            try_files /index.html =404;
        }
    }
}

events {}
```
## 總結
- 使用 location 和 alias 指令靈活配置不同路徑和文件服務
- 使用 try_files 指令處理不同的文件名和返回狀態

# Rewires and Redirect

## 介紹

* 本次討論的主題是 nginx 中的重定向（redirect）和重寫（rewrite）。
* 透過範例說明這些概念的使用方式。

## 重新載入設定並測試重定向

* 設定 nginx 時可以使用 location 區塊來處理不同的 URL 路徑。
* 在範例中，當訪問 `/count/5` 或 `/count/2` 時，會被重定向到其他頁面，這是透過正規表達式來完成的。

## 重定向（Redirect）

* 重定向是一個簡單的概念，首先在 nginx 設定檔中新增一個 location 區塊。
* 例如，訪問 `/crops` 時，想要重定向到 `/fruits`，可以使用以下設定：
  ```nginx
  location /crops {
      return 307 /fruits;
  }
  ```
* 重新載入 nginx 設定後，訪問 `/crops` 會自動重定向到 `/fruits`，並在瀏覽器的 URL 欄位中顯示 `/fruits`。

## 重寫（Rewrite）

* 重寫與重定向不同，它不會改變瀏覽器的 URL，只會在伺服器端改變路徑處理。
* 範例中，訪問 `/number/3` 時，希望 URL 保持不變但實際處理的路徑變為 `/count/3`：
  ```nginx
  rewrite ^/number/(\w+)$ /count/$1;
  ```
* 這樣設定後，訪問 `/number/3` 時，URL 保持不變，但伺服器實際會處理 `/count/3` 的內容。

## 總結

* 重定向（redirect）用於將用戶導向另一個 URL，並在瀏覽器顯示新的 URL。
* 重寫（rewrite）則是改變伺服器處理的路徑，但保持瀏覽器顯示的 URL 不變。
* 理解和靈活運用這些功能對於 nginx 的配置和使用非常重要。


# NGINX as a Load Balancer

## 介紹

* 當應用程式開始有大量使用者時，我們需要擴展應用程式。
* 最佳的擴展方式是建立多個伺服器。
* 問題在於用戶該如何選擇伺服器進行請求，這是 NGINX 所解決的問題。
* NGINX 位於用戶與伺服器之間，負責將請求轉發至特定伺服器。

## 負載平衡（Load Balancer）的概念

* 常見的算法是輪循算法（Round Robin），將請求依次分配給不同的伺服器。
* 需要配置多個伺服器，最佳方式是使用 Docker 建立隔離的伺服器容器。

## 建立 Docker 容器

1. **建立伺服器應用程式**
    * 建立新目錄並在其中創建 `index.js`。
    * 使用 Express 建立簡單的 Node.js 應用程式：
      ```javascript
      const express = require('express');
      const app = express();

      app.get('/', (req, res) => {
          res.send('I am an endpoint');
      });

      app.listen(7777, () => {
          console.log('Listening on port 7777');
      });
      ```
    * 初始化 Node 應用程式並安裝 Express：
      ```bash
      npm init -y
      npm install express
      ```

2. **建立 Dockerfile**

* 建立 Dockerfile，內容如下：
Nodejs Docker WebApp（失效）：https://nodejs.org/docs/guides/nodejs-docker-webapp/
![CleanShot 2024-07-30 at 15.02.51](https://hackmd.io/_uploads/By27gMUKR.png)
```
FROM node:16

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source
COPY . .

EXPOSE 8080
CMD ["node", "server.js"]
```
3. **建立 Docker 映像**
    * 在伺服器目錄中執行命令建立映像：
      ```bash
      docker build -t myserver
      ```

4. **運行 Docker 容器**
    * 運行多個容器，映射到不同的本機端口：
      ```bash
      docker run -d -p 1111:7777 myserver
      docker run -d -p 2222:7777 myserver
      docker run -d -p 3333:7777 myserver
      docker run -d -p 4444:7777 myserver
      ```

## 配置 NGINX 負載平衡

1. **修改 NGINX 設定檔**
    * 打開並編輯 NGINX 設定檔：
      ```nginx
      upstream backendservers {
          server 127.0.0.1:1111;
          server 127.0.0.1:2222;
          server 127.0.0.1:3333;
          server 127.0.0.1:4444;
      }

      server {
          listen 8080;

          location / {
              proxy_pass http://backendservers;
          }
      }
      ```

2. **重新載入 NGINX 設定**
    * 執行命令重新載入 NGINX 設定：
      ```bash
      sudo nginx -s reload
      ```

3. **測試負載平衡**
    * 訪問 `localhost:8080`，應用程式將在多個伺服器之間進行輪循。

## 總結

* NGINX 作為負載平衡器，能有效分配請求至多個伺服器。
* 使用 Docker 建立多個伺服器容器，有助於快速擴展應用程式。
* 輪循算法是實現負載平衡的常用方法之一。

# 指令
## 測試 Nginx 配置
在重新加載 Nginx 配置之前，先測試配置文件是否有誤
```
sudo nginx -t
```

output:
```
nginx: the configuration file /opt/homebrew/etc/nginx/nginx.conf syntax is ok
nginx: configuration file /opt/homebrew/etc/nginx/nginx.conf test is successful
```
## 重新加載 Nginx 配置
重新加載 Nginx 配置以應用更改
```
sudo nginx -s reload
```

## 查看 Homebrew 安裝的 Nginx 錯誤日誌
```
sudo tail -f /opt/homebrew/var/log/nginx/error.log
```

## 清除錯誤日誌文件
```
sudo truncate -s 0 /opt/homebrew/var/log/nginx/error.log
```

## Hard reload
Cmd + Shift + R

# 疑問
## NGINX Installation
Q：
為什麼安裝路徑 /opt/homebrew/bin/nginx
卻是使用 cd /opt/homebrew/etc/nginx

A：
這是因為不同的安裝路徑分別有不同的用途：

1. **執行檔路徑**：
   - `/opt/homebrew/bin/nginx` 是 Nginx 的執行檔路徑。這裡存放的是 Nginx 的可執行文件，也就是你啟動 Nginx 服務時所使用的程式。

2. **配置檔案路徑**：
   - `/opt/homebrew/etc/nginx` 是 Nginx 的配置檔案所在路徑。這裡存放的是 Nginx 的配置文件，如 `nginx.conf`，以及其他相關的設定文件。這些文件控制 Nginx 的運行方式和行為。

總結來說，執行檔和配置檔案通常會分開存放在不同的目錄中：

- **執行檔**：`/opt/homebrew/bin/`
- **配置檔案**：`/opt/homebrew/etc/`

這樣的設置有助於清晰地管理應用程式的各個部分，並且遵循了 Unix 系統中的標準慣例。如果你需要啟動、停止或重啟 Nginx 服務，你會使用執行檔，而如果你需要修改 Nginx 的行為，你會編輯配置檔案。
## Nginx 命令
```
nginx % nginx -s reload
nginx: [alert] kill(25599, 1) failed (3: No such process)
```

### nginx -s reload 沒反應
nginx -s reload 沒反應，Content-Type:
text/plain 沒有改成 text/css
可以開無痕或新 user 網頁來做三角驗證。
使用清除快取解決問題。

## 403 Forbidden
查看 Nginx 錯誤日誌
```
sudo tail -f /opt/homebrew/var/log/nginx/error.log

2024/07/30 11:06:22 [notice] 4047#0: signal process started
2024/07/30 11:06:36 [error] 4048#0: *19 "/Users/userName/Desktop/mysite/index.html" is forbidden (13: Permission denied), client: 127.0.0.1, server: , request: "GET / HTTP/1.1", host: "localhost:8080"
```

我重開機後正常，我懷疑沒有重新加載 .zshrc 文件 


# 關鍵字
- **NGINX**：一個開源的網頁伺服器軟體，用於反向代理、負載均衡和緩存。
- **反向代理（Reverse Proxy）**：NGINX作為中間伺服器，接收客戶端的請求，然後將請求轉發給後端伺服器，接收後端伺服器的響應後再傳回給客戶端。
- **負載均衡（Load Balancing）**：當有多個後端伺服器時，NGINX將請求分配給不同的伺服器以均衡負載，提升效能和可靠性。
- **HTTP/HTTPS**：HTTP是網頁數據傳輸的協議，HTTPS是其安全版本，通過加密來保護數據傳輸安全。
- **AWS（Amazon Web Services）**：提供雲計算服務的平臺，許多公司使用其來託管伺服器。
- **伺服器瓶頸（Server Bottleneck）**：當伺服器無法處理所有傳入請求時會出現的效能問題，通常導致延遲增加。
- **加密和解密（Encryption and Decryption）**：保護數據傳輸安全的過程，加密將數據轉換為不可讀的形式，解密將其轉換回原始形式。
- **Homebrew**：Mac上的包管理器，用於安裝和管理軟體包。
- **配置文件（Configuration File）**：如nginx.conf，用於設置NGINX的各種功能和參數。
- **本地伺服器（localhost）**：指向本機的伺服器，用於測試和開發。
- **網絡請求（Network Request）**：客戶端向伺服器發送的請求，用於獲取網頁內容。
- **網絡標籤（Network Tab）**：瀏覽器開發者工具中的一個標籤，用於檢查網絡請求和響應。
- **瀏覽器（Browser）**：用於訪問網頁的應用程序，如Chrome、Firefox等。
- **內容（Content）**：網頁上的文本、圖片、視頻等資源。
- **映像（Image）**：網頁上的圖片資源。
- **檢查（Inspect）**：使用瀏覽器開發者工具查看和調試網頁。
- **HTTP狀態碼（HTTP Status Code）**：伺服器返回的響應碼，用於表示請求的結果。
- **雲伺服器（Cloud Server）**：託管在雲計算平臺上的伺服器，如AWS上的伺服器。
- **請求處理（Request Handling）**：伺服器接收和處理客戶端請求的過程。
- **用戶端（Client）**：發送請求並接收響應的設備或應用程序，如用戶的電腦或手機。 
- **指令（Directive）**：NGINX配置文件中的鍵值對，如`worker_processes 1;`表示工作進程數量為1。
- **上下文（Context）**：定義配置範圍的代碼塊，用大括號包圍，如`events`上下文和`http`上下文。
- **HTTP上下文（HTTP Context）**：定義HTTP伺服器配置的上下文，其中包含許多指令。
- **事件上下文（Events Context）**：管理NGINX事件處理的上下文。
- **伺服器上下文（Server Context）**：在HTTP上下文內部，用於定義單個伺服器配置的上下文。
- **靜態內容（Static Content）**：指不需要動態生成的文件，如HTML、CSS和圖片文件。
- **端口（Port）**：網絡伺服器監聽請求的通訊端口，如`listen 8080;`表示監聽8080端口。
- **根目錄（Root Directive）**：指定伺服器要提供的文件所在的根目錄，如`root /path/to/site;`。
- **配置重載（Configuration Reload）**：重新加載NGINX配置文件的命令，如`nginx -s reload`。
- **MIME類型（Mime Types）**：定義不同文件類型的標識方法，如`text/css`表示CSS文件。
- **文檔類型（DOCTYPE）**：HTML文件的文檔類型宣告，如`<!DOCTYPE html>`。
- **字符集（Charset）**：指定HTML文件的字符編碼，如`<meta charset="UTF-8">`。
- **標題（Head）**：HTML文件的頭部區域，用於包含元數據和鏈接外部資源。
- **超文本標記語言（HTML）**：用於構建網頁結構的標記語言。
- **連結（Link）**：HTML標籤，用於連接外部CSS文件，如`<link rel="stylesheet" href="styles.css">`。
- **背景顏色（Background Color）**：CSS屬性，用於設置元素的背景顏色。
- **顏色（Color）**：CSS屬性，用於設置元素的文本顏色。
- **硬重載（Hard Reload）**：強制重新加載網頁並清除緩存的操作，通常使用命令`Command+Shift+R`。
- **緩存（Caching）**：在客戶端或伺服器端保存已加載的資源，以提高後續請求的加載速度。 
- **位置上下文（Location Context）**：NGINX配置中的一個重要概念，用於指定特定的端點或頁面，以服務不同類型的HTML元素。
- **目錄（Directory）**：在網站中，用於組織和管理不同類型的內容。例如，`fruits`目錄包含水果相關的HTML文件。
- **無序列表（UL）**：HTML標籤，用於創建無序列表。
- **列表項（LI）**：HTML標籤，用於創建列表中的單個項目。
- **位置塊（Location Block）**：用於在NGINX配置文件中定義特定路徑的配置。例如，`location /fruits`定義了當訪問`/fruits`時的行為。
- **根目錄（Root）**：指示伺服器從哪個目錄服務文件。例如，`root /path/to/site`。
- **別名（Alias）**：在NGINX配置中，用於指定一個路徑別名，與`root`不同，它不會將請求的路徑附加到別名路徑的末尾。
- **重載（Reload）**：重新加載NGINX配置文件以應用更改。
- **403 Forbidden**：HTTP狀態碼，表示伺服器拒絕提供請求的資源。
- **404 Not Found**：HTTP狀態碼，表示伺服器無法找到請求的資源。
- **嘗試文件（Try Files）**：NGINX指令，用於指定當請求的文件不存在時要嘗試的其他文件。例如，`try_files /path/to/file /index.html =404`。
- **正則表達式（Regular Expression）**：用於在NGINX位置上下文中匹配特定的URL模式。
- **Tilde符號（~）**：在NGINX配置中，用於指示正則表達式匹配。
- **星號（*）**：在正則表達式中，用於匹配零個或多個字符。
- **重定向（Redirect）**：將一個URL重定向到另一個URL。例如，將所有`/count/`路徑重定向到根目錄。
- **靜態內容（Static Content）**：指不需要動態生成的文件，如HTML、CSS和圖片文件。
- **標題（Header）**：HTTP響應的一部分，用於提供有關響應的元數據。
- **內容類型（Content Type）**：HTTP標頭，用於指示資源的媒體類型。例如，`text/html`表示HTML文件。
- **樣式表（Stylesheet）**：CSS文件，用於定義網頁的樣式和佈局。
- **鏈接標籤（Link Tag）**：HTML標籤，用於在HTML文件中引入外部CSS文件。 
- **重定向（Redirect）**：將一個URL重定向到另一個URL，使用HTTP狀態碼如307來進行跳轉。例如，當訪問`/crops`時，重定向到`/fruits`。
- **重寫（Rewrite）**：改變請求的URL路徑，但保持瀏覽器中的URL不變。例如，將`/number/{number}`重寫為`/count/{number}`，但URL仍然顯示為`/number/{number}`。
- **307重定向（307 Redirect）**：HTTP狀態碼，表示臨時重定向，請求方法和主體在重定向後保持不變。
- **變量（Variable）**：在重寫規則中使用的佔位符，如`$1`表示匹配的第一個分組。
- **正則表達式（Regular Expression）**：用於匹配URL模式的語法，例如`\w+`表示匹配一個或多個字母或數字。
- **位置塊（Location Block）**：在NGINX配置中定義特定路徑的配置。例如，`location /crops`定義了當訪問`/crops`時的行為。
- **返回指令（Return Directive）**：在NGINX配置中用於立即返回特定狀態碼和URL的指令。例如，`return 307 /fruits;`表示返回307重定向到`/fruits`。
- **重寫指令（Rewrite Directive）**：在NGINX配置中用於改變請求URL的指令。例如，`rewrite ^/number/(\w+)$ /count/$1;`表示將`/number/{number}`重寫為`/count/{number}`。
- **NGINX重載（NGINX Reload）**：重新加載NGINX配置文件以應用更改，通常使用命令`nginx -s reload`。
- **URL模式（URL Pattern）**：用於匹配特定URL結構的模式，例如`/number/{number}`。
- **動態端點（Dynamic Endpoint）**：具有可變部分的URL端點，例如`/number/{number}`中的`{number}`部分。
- **靜態端點（Static Endpoint）**：固定不變的URL端點，例如`/crops`或`/fruits`。
- **HTML元素（HTML Elements）**：網頁中的基本組成部分，如標籤和文本。
- **內容轉發（Content Forwarding）**：將請求轉發到不同的路徑，但保持原始URL不變。
- **伺服器上下文（Server Context）**：在NGINX配置文件中的一個部分，用於定義伺服器相關的配置。
- **根目錄（Root Directive）**：指示伺服器從哪個目錄服務文件，例如`root /path/to/site;`。
- **別名（Alias）**：在NGINX配置中，用於指定一個路徑別名，與`root`不同，它不會將請求的路徑附加到別名路徑的末尾。
- **返回指令（Return Directive）**：在NGINX配置中用於立即返回特定狀態碼和URL的指令。例如，`return 307 /fruits;`表示返回307重定向到`/fruits`。
- **重寫指令（Rewrite Directive）**：在NGINX配置中用於改變請求URL的指令，例如`rewrite ^/number/(\w+)$ /count/$1;`表示將`/number/{number}`重寫為`/count/{number}`。
- **負載均衡（Load Balancing）**：NGINX的高級功能，用於將請求分配給多個伺服器以均衡負載，提高效能和可靠性。 
- **負載均衡（Load Balancing）**：將請求分配給多個伺服器以均衡負載，提高效能和可靠性。
- **Docker**：一個用於創建和管理容器化應用程序的工具，容器是隔離的執行環境。
- **Docker容器（Docker Container）**：輕量級、可移植的軟體包，包含應用程序及其所有依賴。
- **Docker映像（Docker Image）**：用於創建容器的靜態快照，包含運行應用程序所需的所有內容。
- **Dockerfile**：一個文本文件，包含構建Docker映像的指令。
- **端口映射（Port Mapping）**：將主機的端口映射到容器內部的端口，以便外部訪問容器中的應用程序。
- **round robin算法**：一種將請求依次分配給每個伺服器的負載均衡算法。
- **上游伺服器（Upstream Server）**：NGINX配置中的一組伺服器，用於負載均衡。
- **反向代理（Reverse Proxy）**：NGINX作為中間伺服器，接收客戶端的請求並將其轉發給後端伺服器，然後將響應返回給客戶端。
- **代理轉發（Proxy Pass）**：NGINX指令，用於將請求轉發給上游伺服器。
- **指令（Directive）**：NGINX配置文件中的鍵值對，用於設置各種功能。
- **上下文（Context）**：定義配置範圍的代碼塊，用大括號包圍。
- **HTTP上下文（HTTP Context）**：定義HTTP伺服器配置的上下文。
- **伺服器上下文（Server Context）**：定義單個伺服器配置的上下文。
- **位置塊（Location Block）**：定義特定路徑的配置。
- **npm**：Node.js的包管理器，用於安裝和管理JavaScript庫和工具。
- **Express**：Node.js的Web應用框架，用於構建伺服器端應用程序。
- **GET請求（GET Request）**：一種HTTP請求方法，用於從伺服器獲取數據。
- **控制台日誌（Console Log）**：在控制台中輸出消息，用於調試和信息顯示。
- **npm腳本（npm Script）**：在package.json文件中定義的命令，可通過`npm run`運行。 
