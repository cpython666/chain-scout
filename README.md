# Web3-Monitor-Go

[![Go Version](https://img.shields.io/badge/Go-1.21-blue.svg)](https://golang.org/) [![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## 项目概述
Web3-Monitor-Go 是一个使用 Go 语言构建的 Web3 领域信息监控系统，支持定时爬取新闻和监控区块链仓位变化。项目使用 MongoDB 作为数据库，支持任务重启和持久化状态。通过 cron 调度器管理多个并发任务，适用于实时监控 DeFi、NFT 或加密货币相关事件。项目结构模块化，便于扩展和维护。


Web3-Monitor-Go 是一个开源的 Web3 信息监控项目，使用 Go 语言实现。主要功能包括：
- **定时爬虫任务**：采集 Web3 相关新闻（如从 CoinDesk、Twitter 等源）。
- **仓位监控**：实时监控区块链钱包或合约仓位变化（支持 Ethereum 等 EVM 链）。
- **数据库支持**：使用 MongoDB 存储采集数据和任务状态，支持任务重启（程序崩溃或重启时从数据库恢复）。
<!-- - **可扩展性**：模块化设计，便于添加新任务或集成通知（如 Telegram 警报）。 -->

项目适用于 DeFi 爱好者、交易员或开发者，用于自动化监控加密市场动态。

## 特性
- **定时调度**：基于 cron 表达式，支持灵活的任务间隔（如每 5 分钟检查仓位）。
- **并发处理**：使用 Go goroutines 高效运行多个爬虫任务。
- **持久化**：任务状态存储在 MongoDB，确保重启后无缝恢复。
- **配置灵活**：通过 YAML 文件管理数据库连接、API 密钥和任务参数。
- **日志记录**：结构化日志，便于调试和监控。

## 安装与运行
### 前提条件
- Go 1.21 或更高版本。
- MongoDB 服务器（本地或云端，如 MongoDB Atlas）。
<!-- - 可选：Infura/Alchemy API 密钥（用于区块链交互）。 -->

### 步骤
1. 克隆仓库：
   ```
   git clone git@github.com:cpython666/web3-monitor-go.git
   cd web3-monitor-go
   ```

2. 安装依赖：
   ```
   go mod tidy
   ```

3. 配置 `configs/config.yaml`：
   示例：
   ```yaml
   mongodb:
     uri: "mongodb://localhost:27017"
     database: "web3_monitor"
   tasks:
     news_crawler:
       cron: "0 */1 * * *"  # 每小时运行
     position_monitor:
       cron: "*/5 * * * *"  # 每5分钟运行
       wallets: ["0xYourWalletAddress"]
   ethereum:
     <!-- rpc_url: "https://mainnet.infura.io/v3/YOUR_API_KEY" -->
   ```

4. 运行项目：
   ```
   go run cmd/monitor/main.go
   ```

5. 测试：访问 MongoDB 检查数据插入，或查看控制台日志。

## 项目目录结构
```
web3-monitor-go/
├── cmd/
│   └── monitor/
│       └── main.go
├── internal/
│   ├── config/
│   ├── crawler/
│   ├── db/
│   ├── scheduler/
│   └── utils/
├── configs/
│   └── config.yaml
├── scripts/
├── docs/
├── go.mod
├── go.sum
├── README.md
└── .gitignore
```

详细说明见 `docs/architecture.md`。

## 依赖包
- `go.mongodb.org/mongo-driver/mongo`：MongoDB 操作。
- `github.com/robfig/cron/v3`：定时任务。
- `github.com/gocolly/colly`：Web 爬虫。
- `github.com/ethereum/go-ethereum`：区块链交互。
- `github.com/spf13/viper`：配置管理。
- `github.com/sirupsen/logrus`：日志记录。
- `github.com/go-resty/resty/v2`：HTTP 客户端。

## 贡献
欢迎 PR！请遵循 Go 编码规范，并添加单元测试。

## 许可证
MIT License. 详见 [LICENSE](LICENSE) 文件。

## 联系
如有问题，请开 Issue 或联系 [your.email@example.com](mailto:your.email@example.com)。