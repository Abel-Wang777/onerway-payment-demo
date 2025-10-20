# Onerway Payment Integration Demo (Java + Spark Framework)
# Onerway 支付集成演示项目（Java + Spark 框架）

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/onerway/onerway-payment-demo-java?quickstart=1)

**English** | [中文](#中文文档)

A demo project showcasing how to integrate the Onerway payment gateway using Java and the Spark Framework.

---

## 📋 Prerequisites
- Java 21 (required by pom.xml)
- Maven 3.9.6 or higher
- Git (for local development)

## 🚀 Quick Start

### Option 1: Run in GitHub Codespaces (Recommended)

1. [![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/onerway/onerway-payment-demo-java?quickstart=1)
2. Wait for the environment to initialize (~1 minute)
3. The devcontainer will automatically run `mvn clean install -DskipTests`
4. Configure your credentials (see Configuration section below)
5. Run: `mvn exec:java`
6. Open the forwarded port 8080 in your browser
7. Navigate to `/create-checkout-session` to test the payment flow

### Option 2: Run Locally

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd onerway-payment-demo
   ```

2. **Verify Java version**:
   ```bash
   java -version  # Should be Java 21
   ```

3. **Install dependencies**:
   ```bash
   mvn clean install -DskipTests
   ```

4. **Configure credentials** (see Configuration section below)

5. **Run the application**:
   ```bash
   mvn exec:java
   ```

6. **Test the integration**:
   - Open your browser to `http://localhost:8080/create-checkout-session`
   - You should be redirected to the Onerway payment page

## 📝 Configuration

Before running the application, you **must** update the following credentials in [`src/main/java/com/onerway/demo/ServerDemo.java`](src/main/java/com/onerway/demo/ServerDemo.java):

| Line | Variable | Description | Example |
|------|----------|-------------|---------|
| 31 | `MERCHANT_NO` | Your merchant number from Onerway | `"M123456789"` |
| 32 | `DEFAULT_APP_ID` | Your application ID from Onerway | `"APP_ABC123"` |
| 33 | `MERCHANT_SECRET` | Your merchant secret key (for signature generation) | `"your-secret-key"` |
| 34 | `DEFAULT_RETURN_URL` | URL where customers return after payment | `"https://yourdomain.com/payment/return"` |
| 35 | `DEFAULT_NOTIFY_URL` | Webhook URL for async payment notifications | `"https://yourdomain.com/payment/notify"` |

> **Note**: The application uses the Onerway sandbox environment by default: `https://sandbox-acq.onerway.com/txn/payment`

## 🏗️ Project Structure

```
onerway-payment-demo/
├── src/main/java/com/onerway/demo/
│   └── ServerDemo.java          # Main application with payment integration logic
├── pom.xml                       # Maven configuration
└── .devcontainer/                # GitHub Codespaces configuration
    └── devcontainer.json
```

## 🔑 Key Features

- **Payment Request Building**: Constructs payment requests with billing information and transaction details
- **Signature Generation**: Implements Onerway's SHA-256 signature algorithm for request authentication
- **API Communication**: Uses Java's HttpClient to communicate with Onerway's API
- **Automatic Redirect**: Extracts and redirects customers to the Onerway payment page

## 🛠️ Development

### Build Commands

- **Clean build**: `mvn clean install`
- **Run without tests**: `mvn clean install -DskipTests`
- **Run application**: `mvn exec:java`
- **Clean artifacts**: `mvn clean`

### Testing the Payment Flow

1. Start the server: `mvn exec:java`
2. Access: `http://localhost:8080/create-checkout-session`
3. The server will:
   - Generate a payment request with demo data
   - Sign the request using your merchant secret
   - Call the Onerway API
   - Redirect you to the payment page

## 📚 Additional Resources

- [Onerway Payment Gateway Documentation](https://docs.onerway.com/apis/en/)

## 🔒 Security Notes

- Never commit your `MERCHANT_SECRET` to version control
- Use environment variables or secure configuration management in production
- The current implementation uses hardcoded credentials for demo purposes only

---

# 中文文档

## 📋 前置要求
- Java 21（pom.xml 中要求）
- Maven 3.9.6 或更高版本
- Git（本地开发时需要）

## 🚀 快速开始

### 方式一：在 GitHub Codespaces 中运行（推荐）

1. [![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/onerway/onerway-payment-demo-java?quickstart=1)
2. 等待环境初始化（约 1 分钟）
3. devcontainer 会自动运行 `mvn clean install -DskipTests`
4. 配置你的凭证（参见下方配置章节）
5. 运行：`mvn exec:java`
6. 在浏览器中打开转发的 8080 端口
7. 访问 `/create-checkout-session` 测试支付流程

### 方式二：本地运行

1. **克隆仓库**：
   ```bash
   git clone <repository-url>
   cd onerway-payment-demo
   ```

2. **验证 Java 版本**：
   ```bash
   java -version  # 应该是 Java 21
   ```

3. **安装依赖**：
   ```bash
   mvn clean install -DskipTests
   ```

4. **配置凭证**（参见下方配置章节）

5. **运行应用**：
   ```bash
   mvn exec:java
   ```

6. **测试集成**：
   - 在浏览器中打开 `http://localhost:8080/create-checkout-session`
   - 你将被重定向到 Onerway 支付页面

## 📝 配置

在运行应用之前，你**必须**在 [`src/main/java/com/onerway/demo/ServerDemo.java`](src/main/java/com/onerway/demo/ServerDemo.java) 中更新以下凭证：

| 行号 | 变量 | 描述 | 示例 |
|------|------|------|------|
| 31 | `MERCHANT_NO` | 你从 Onerway 获取的商户号 | `"M123456789"` |
| 32 | `DEFAULT_APP_ID` | 你从 Onerway 获取的应用 ID | `"APP_ABC123"` |
| 33 | `MERCHANT_SECRET` | 你的商户密钥（用于签名生成） | `"your-secret-key"` |
| 34 | `DEFAULT_RETURN_URL` | 支付完成后客户返回的 URL | `"https://yourdomain.com/payment/return"` |
| 35 | `DEFAULT_NOTIFY_URL` | 接收异步支付通知的 Webhook URL | `"https://yourdomain.com/payment/notify"` |

> **注意**：应用默认使用 Onerway 沙箱环境：`https://sandbox-acq.onerway.com/txn/payment`

## 🏗️ 项目结构

```
onerway-payment-demo/
├── src/main/java/com/onerway/demo/
│   └── ServerDemo.java          # 包含支付集成逻辑的主应用程序
├── pom.xml                       # Maven 配置
└── .devcontainer/                # GitHub Codespaces 配置
    └── devcontainer.json
```

## 🔑 核心功能

- **支付请求构建**：构造包含账单信息和交易详情的支付请求
- **签名生成**：实现 Onerway 的 SHA-256 签名算法以进行请求认证
- **API 通信**：使用 Java 的 HttpClient 与 Onerway API 通信
- **自动重定向**：提取并重定向客户到 Onerway 支付页面

## 🛠️ 开发

### 构建命令

- **清理构建**：`mvn clean install`
- **跳过测试构建**：`mvn clean install -DskipTests`
- **运行应用**：`mvn exec:java`
- **清理构建产物**：`mvn clean`

### 测试支付流程

1. 启动服务器：`mvn exec:java`
2. 访问：`http://localhost:8080/create-checkout-session`
3. 服务器将：
   - 使用演示数据生成支付请求
   - 使用你的商户密钥对请求进行签名
   - 调用 Onerway API
   - 将你重定向到支付页面

## 📚 其他资源

- [Onerway 支付网关文档](https://docs.onerway.com/apis/zh/)

## 🔒 安全注意事项

- 永远不要将你的 `MERCHANT_SECRET` 提交到版本控制系统
- 在生产环境中使用环境变量或安全的配置管理
- 当前实现使用硬编码凭证仅用于演示目的
