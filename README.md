# SpringBucks 咖啡店服務員微服務 ⚡

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.5-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Spring Cloud](https://img.shields.io/badge/Spring%20Cloud-2024.0.2-blue.svg)](https://spring.io/projects/spring-cloud)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 專案介紹

本專案實作一個咖啡店服務員微服務，負責處理咖啡產品管理與訂單處理的核心業務邏輯。此服務作為 SpringBucks 咖啡店系統的一部分，展示如何使用 Spring Cloud 與 Eureka 建構微服務架構。

**核心功能：**
- **咖啡產品管理**：新增、查詢、批量匯入咖啡產品資訊
- **訂單處理**：建立與管理咖啡訂單，支援多種咖啡組合
- **服務註冊**：自動向 Eureka 服務註冊中心註冊服務實例
- **健康監控**：整合 Actuator 提供完整的服務健康檢查與監控指標
- **金額處理**：使用 Joda Money 進行精確的貨幣計算

> 💡 **為什麼選擇此微服務架構？**
> - 業務邏輯清晰分離，便於維護與擴展
> - 支援服務自動發現，提升系統可用性
> - 完整的監控與健康檢查機制
> - 採用領域驅動設計（DDD）原則

### 🎯 專案特色

- **微服務架構**：完整的服務註冊與發現機制
- **RESTful API**：提供標準化的 HTTP API 介面
- **資料持久化**：使用 JPA 與 H2 資料庫實現資料存取
- **快取機制**：整合 Spring Cache 提升查詢效能
- **監控整合**：支援 Prometheus 指標收集與健康檢查
- **金額精度**：使用專業的貨幣處理庫確保計算精確性

## 技術棧

### 核心框架
- **Spring Boot 3.4.5** - 主框架，提供自動配置與生產就緒功能
- **Spring Cloud 2024.0.2** - 微服務框架，提供服務註冊與發現等功能
- **Spring Data JPA** - 資料持久層框架，簡化資料庫操作
- **Spring Web MVC** - Web 層框架，提供 RESTful API 支援

### 微服務相關
- **Netflix Eureka Client** - 服務註冊與發現客戶端
- **Spring Cloud Discovery** - 服務發現抽象層
- **Spring Boot Actuator** - 應用監控與管理端點

### 資料處理與工具
- **Joda Money 2.0.2** - 專業的貨幣處理庫，支援精確計算
- **Jackson Hibernate6** - JSON 序列化與 Hibernate 整合
- **Apache Commons Lang3 3.17.0** - 常用工具類庫
- **H2 Database** - 記憶體資料庫（開發環境使用）

### 開發工具與輔助
- **Lombok** - 簡化 Java 程式碼撰寫
- **Micrometer Prometheus** - 指標收集與監控
- **Maven** - 專案建構與依賴管理工具

## 專案結構

```
eureka-waiter-service/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── tw/fengqing/spring/springbucks/waiter/
│   │   │       ├── WaiterServiceApplication.java        # 主啟動類
│   │   │       ├── controller/                          # Web 控制器層
│   │   │       │   ├── CoffeeController.java           # 咖啡產品 API
│   │   │       │   ├── CoffeeOrderController.java      # 訂單管理 API
│   │   │       │   ├── PerformanceInteceptor.java      # 效能監控攔截器
│   │   │       │   └── request/                        # 請求物件
│   │   │       ├── model/                              # 領域模型層
│   │   │       │   ├── Coffee.java                    # 咖啡產品實體
│   │   │       │   ├── CoffeeOrder.java              # 訂單實體
│   │   │       │   ├── MoneyConverter.java           # 金額轉換器
│   │   │       │   └── OrderState.java               # 訂單狀態枚舉
│   │   │       ├── repository/                        # 資料存取層
│   │   │       │   ├── CoffeeRepository.java         # 咖啡產品倉儲
│   │   │       │   └── CoffeeOrderRepository.java    # 訂單倉儲
│   │   │       ├── service/                           # 業務邏輯層
│   │   │       │   ├── CoffeeService.java            # 咖啡產品服務
│   │   │       │   └── CoffeeOrderService.java       # 訂單服務
│   │   │       └── support/                           # 輔助工具類
│   │   │           ├── CoffeeIndicator.java          # 健康檢查指標
│   │   │           ├── MoneyDeserializer.java        # 金額反序列化
│   │   │           ├── MoneySerializer.java          # 金額序列化
│   │   │           └── MoneyFormatter.java           # 金額格式化
│   │   └── resources/
│   │       ├── application.properties                 # 應用配置檔案
│   │       ├── schema.sql                            # 資料庫結構定義
│   │       ├── data.sql                              # 初始資料
│   │       └── coffee.txt                            # 咖啡產品範例檔案
│   └── test/                                          # 測試程式碼
├── target/                                            # 編譯輸出目錄
├── pom.xml                                           # Maven 專案配置
├── LICENSE                                           # 授權檔案
└── README.md                                         # 專案說明文件
```

## 快速開始

### 前置需求
- Java 21 或更高版本
- Maven 3.6+ 或 Gradle 7.0+
- 執行中的 Eureka Server（建議先啟動 eureka-server 專案）
- 網路連線（用於下載依賴套件）

### 安裝與執行

1. **克隆此倉庫：**
```bash
git clone <repository-url>
```

2. **進入專案目錄：**
```bash
cd eureka-waiter-service
```

3. **編譯專案：**
```bash
mvn clean compile
```

4. **執行應用程式：**
```bash
# 方法一：使用 Maven 執行
mvn spring-boot:run

# 方法二：打包後執行
mvn clean package
java -jar target/waiter-service-0.0.1-SNAPSHOT.jar
```

5. **驗證服務啟動：**
```bash
# 檢查服務健康狀態
curl http://localhost:{random-port}/actuator/health

# 查看所有咖啡產品
curl http://localhost:{random-port}/coffee/
```

## API 端點說明

### 咖啡產品管理 API

#### 查詢所有咖啡產品
```http
GET /coffee/
```

#### 依 ID 查詢咖啡產品
```http
GET /coffee/{id}
```

#### 依名稱查詢咖啡產品
```http
GET /coffee/?name={coffeeName}
```

#### 新增咖啡產品（表單格式）
```http
POST /coffee/
Content-Type: application/x-www-form-urlencoded

name=Americano&price=TWD 125.0
```

#### 新增咖啡產品（JSON 格式）
```http
POST /coffee/
Content-Type: application/json

{
  "name": "Latte",
  "price": 150.0
}
```

#### 批量新增咖啡產品
```http
POST /coffee/
Content-Type: multipart/form-data

[上傳 coffee.txt 檔案]
```

### 訂單管理 API

#### 查詢訂單
```http
GET /order/{orderId}
```

#### 建立新訂單
```http
POST /order/
Content-Type: application/json

{
  "customer": "張先生",
  "items": ["espresso", "latte"]
}
```

### 監控端點

#### 健康檢查
```http
GET /actuator/health
```

#### 應用資訊
```http
GET /actuator/info
```

#### Prometheus 指標
```http
GET /actuator/prometheus
```

## 進階說明

### 環境變數
```properties
# Eureka Server 位址（可選，預設為 http://localhost:8761/eureka/）
EUREKA_CLIENT_SERVICE_URL_DEFAULTZONE=http://eureka-server:8761/eureka/

# 服務實例偏好設定（可選）
EUREKA_INSTANCE_PREFER_IP_ADDRESS=true

# 日誌等級（可選）
LOGGING_LEVEL_ROOT=INFO
```

### 設定檔說明
```properties
# application.properties 主要設定

# 應用程式名稱 - 用於 Eureka 服務註冊（重要：此名稱會顯示在 Eureka 管理介面中）
spring.application.name=waiter-service

# JPA 資料庫設定
spring.jpa.hibernate.ddl-auto=none          # 使用 schema.sql 建立資料表
spring.jpa.properties.hibernate.show_sql=true    # 顯示 SQL 語句（開發環境）
spring.jpa.properties.hibernate.format_sql=true  # 格式化 SQL 輸出

# Actuator 監控端點設定
management.endpoints.web.exposure.include=*      # 暴露所有監控端點
management.endpoint.health.show-details=always  # 顯示詳細健康檢查資訊
management.info.env.enabled=true                # 啟用 info 端點環境變數顯示

# 應用資訊設定
info.app.author=DigitalSonic
info.app.encoding=@project.build.sourceEncoding@

# 服務埠設定（重要：使用隨機埠避免衝突）
server.port=0    # 系統自動分配可用埠號
```

### 資料庫初始化
系統啟動時會自動執行以下檔案：
1. `schema.sql` - 建立資料表結構
2. `data.sql` - 插入初始咖啡產品資料

**預設咖啡產品：**
- Espresso (100.00 TWD)
- Latte (125.00 TWD)
- Cappuccino (125.00 TWD)
- Mocha (150.00 TWD)
- Macchiato (150.00 TWD)

### 金額處理機制
本專案使用 Joda Money 庫處理金額計算：

```java
// 金額在資料庫中以分為單位儲存（避免浮點數精度問題）
@Convert(converter = MoneyConverter.class)
private Money price;

// 建立金額物件
Money price = Money.of(CurrencyUnit.of("TWD"), new BigDecimal("125.00"));
```

### 服務註冊與發現
```java
// 啟用服務發現客戶端功能
@EnableDiscoveryClient
public class WaiterServiceApplication {
    // 應用程式會自動向 Eureka Server 註冊
    // 服務名稱：waiter-service
    // 實例 ID：IP:waiter-service:隨機埠號
}
```

## 參考資源

- [Spring Cloud Netflix 官方文件](https://cloud.spring.io/spring-cloud-netflix/reference/html/)
- [Spring Boot Actuator 官方文件](https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html)
- [Joda Money 官方文件](https://www.joda.org/joda-money/)
- [Spring Data JPA 官方文件](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/)
- [H2 Database 官方文件](https://www.h2database.com/html/main.html)

## 注意事項與最佳實踐

### ⚠️ 重要提醒

| 項目 | 說明 | 建議做法 |
|------|------|----------|
| 服務啟動順序 | 必須先啟動 Eureka Server | 確保 eureka-server 先行啟動 |
| 埠號衝突 | 使用隨機埠避免衝突 | 維持 `server.port=0` 設定 |
| 金額精度 | 避免浮點數計算誤差 | 使用 Joda Money 處理所有金額 |
| 服務註冊 | 應用名稱必須唯一 | 確保 `spring.application.name` 的唯一性 |
| 監控安全 | Actuator 端點可能暴露敏感資訊 | 生產環境請限制端點存取權限 |

### 🔒 最佳實踐指南

- **服務健康檢查**：實作自定義健康指標（如 `CoffeeIndicator`），監控業務邏輯狀態
- **效能監控**：使用攔截器（`PerformanceInteceptor`）追蹤請求處理時間
- **資料驗證**：在所有 API 端點使用 `@Valid` 註解確保資料完整性
- **異常處理**：實作全域異常處理器，提供一致的錯誤回應格式
- **快取策略**：在查詢頻繁的服務方法上使用 `@Cacheable` 提升效能
- **日誌記錄**：使用 SLF4J 與 Logback 記錄關鍵業務操作
- **測試覆蓋**：撰寫單元測試與整合測試確保程式碼品質

### 📊 監控與觀測

#### 自定義健康檢查
```java
@Component
public class CoffeeIndicator implements HealthIndicator {
    // 檢查咖啡產品庫存狀態
    // 當咖啡產品數量 > 0 時回報 UP
    // 當咖啡產品數量 = 0 時回報 DOWN
}
```

#### 業務指標監控
```java
@Service
public class CoffeeOrderService implements MeterBinder {
    // 整合 Micrometer 監控訂單建立數量
    // 指標名稱：order.count
}
```

### 🔧 開發環境設定

#### IDE 設定建議
- 安裝 Lombok 外掛程式
- 啟用 annotation processing
- 設定 Java 21 作為專案 SDK

#### 本地測試環境
```bash
# 1. 啟動 Eureka Server（8761 埠）
cd ../eureka-server && mvn spring-boot:run

# 2. 啟動 Waiter Service（隨機埠）
mvn spring-boot:run

# 3. 檢查服務註冊狀態
curl http://localhost:8761
```

## 授權說明

本專案採用 MIT 授權條款，詳見 LICENSE 檔案。

## 關於我們

我們主要專注在敏捷專案管理、物聯網（IoT）應用開發和領域驅動設計（DDD）。喜歡把先進技術和實務經驗結合，打造好用又靈活的軟體解決方案。

## 聯繫我們

- **FB 粉絲頁**：[風清雲談 | Facebook](https://www.facebook.com/profile.php?id=61576838896062)
- **LinkedIn**：[linkedin.com/in/chu-kuo-lung](https://www.linkedin.com/in/chu-kuo-lung)
- **YouTube 頻道**：[雲談風清 - YouTube](https://www.youtube.com/channel/UCXDqLTdCMiCJ1j8xGRfwEig)
- **風清雲談 部落格**：[風清雲談](https://blog.fengqing.tw/)
- **電子郵件**：[fengqing.tw@gmail.com](mailto:fengqing.tw@gmail.com)

---

**📅 最後更新：2024年12月**  
**👨‍💻 維護者：風清雲談團隊**
