關於串接 news api 資料的操作描述

使用 async/await 搭配 fetch 函數來獲取 API 資料：

**1. 定義 API Key 和 URL**

    在 methods 中建立一個函數，定義 API Key 和 API 的 URL。

**2. 發送 API 請求**

    使用 JavaScript 的 fetch 函數，傳入 API URL，並處理回傳的 response。

**3. 解析 API 響應**

    獲取的 response 是此 API 回傳的資料，使用 response.json() 將其轉換為可操作的 JSON 格式。

**4. 處理數據**

    宣告一個 array 來儲存 API 回傳的資料。通過 map 方法，將每一筆資料的 description 和 url 提取出來，並組成多個 object，然後存入 array 中，如此即可對此 array 進行處理。
