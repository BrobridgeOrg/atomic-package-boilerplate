# Config 設定說明文件

## 概述
此文件說明如何設定 Atomic Package 的設定結構。每個 package 可以包含多個設定頁面，用於設定不同類型的參數。

---

## 一、Config 列表結構

在 manifest 中定義多個設定項目：

```json
{
    "configs": [
        { "name": "config1" },
        { "name": "config2" }
    ]
}
```

---

## 二、Config 設定項目

每個設定項目包含以下欄位：

| 欄位 | 說明 |
|------|------|
| `name` | 設定項目的名稱 |
| `desc` | 設定項目的用途說明 |
| `config_server_path` | 其他服務取得此設定資料的 API 路徑 |
| `schema` | 可設定的欄位定義（詳見下方說明） |

**範例：**
```json
{
    "name": "database_config",
    "desc": "資料庫連線設定",
    "config_server_path": "/api/config/database",
    "schema": {
        // 欄位定義
    }
}
```

---

## 三、Schema 欄位定義

### 3.1 什麼是 Schema？
Schema 定義了前端設定頁面的表單欄位，系統會根據 schema 自動生成對應的 UI 元件，讓使用者輸入並儲存設定。

### 3.2 Schema 欄位結構

每個欄位包含以下屬性：

```json
"schema": {
    "欄位名稱": {
        "desc": "欄位說明文字",
        "dataType": "資料型態",
        "uiType": "UI 元件類型",
        "required": true/false,
        "rules": [
            // 驗證規則
        ]
    }
}
```

### 3.3 支援的資料型態 (dataType)

| dataType | 說明 |
|----------|------|
| `string` | 字串 |
| `integer` | 整數 |
| `boolean` | 布林值 (true/false) |
| `enum` | 列舉（從選項中選擇） |
| `array` | 陣列 |
| `object` | 物件 |

### 3.4 支援的 UI 元件 (uiType)

| uiType | 說明 | 適用 dataType |
|--------|------|---------------|
| `input` | 文字輸入框 | string |
| `password` | 密碼輸入框 | string |
| `number` | 數字輸入框 | integer |
| `select` | 下拉選單（單選） | enum |
| `multiselect` | 下拉選單（多選） | array |
| `checkbox` | 勾選框 | boolean |
| `radio` | 單選按鈕 | boolean, enum |

### 3.5 支援的驗證規則 (rules)

| rule | 說明 | 範例 |
|------|------|------|
| `min` | 最小值 | `{"type": "min", "value": 1}` |
| `max` | 最大值 | `{"type": "max", "value": 100}` |
| `minLength` | 最小長度 | `{"type": "minLength", "value": 6}` |
| `maxLength` | 最大長度 | `{"type": "maxLength", "value": 50}` |
| `regex` | 正規表達式驗證 | `{"type": "regex", "value": "^[a-zA-Z0-9]+$"}` |

---

rule會有三

## 四、schema單個欄位範例

### 範例 1：密碼輸入框（加密）
```json
"password": {
    "desc": "資料庫密碼",
    "dataType": "string",
    "uiType": "password",
    "required": true,
    "rules": [
        {
            "type": "minLength",
            "value": 8,
            "err_msg": "密碼長度至少需要 8 個字元"
        }
    ]
}
```

### 範例 2：下拉選單（單選）
```json
"type": {
    "desc": "資料庫類型",
    "dataType": "enum",
    "uiType": "select",
    "required": true,
    "options": [
        { "label": "Oracle", "value": "oracle" },
        { "label": "Informix", "value": "informix" },
        { "label": "MS SQL", "value": "mssql" },
        { "label": "MySQL", "value": "mysql" },
        { "label": "PostgreSQL", "value": "postgresql" }
    ]
}
```

### 範例 3：勾選框
```json
"encrypted": {
    "desc": "密碼是否已加密？",
    "dataType": "boolean",
    "uiType": "checkbox",
    "default": false
}
```

### 範例 4：單選按鈕
```json
"encrypted": {
    "desc": "密碼是否已加密？",
    "dataType": "boolean",
    "uiType": "radio",
    "default": false,
    "options": [
        { "label": "是", "value": true },
        { "label": "否", "value": false }
    ]
}
```

### 範例 5：數字輸入框（帶範圍限制）
```json
"port": {
    "desc": "資料庫連接埠",
    "dataType": "integer",
    "uiType": "number",
    "required": true,
    "default": 5432,
    "rules": [
        {
            "type": "min",
            "value": 1,
            "err_msg": "連接埠號碼必須大於 1"
        },
        {
            "type": "max",
            "value": 65535,
            "err_msg": "連接埠號碼不能超過 65535"
        }
    ]
}
```

---

## 參考資料
完整的設定範例請參考 [manifest.json](manifest.json)