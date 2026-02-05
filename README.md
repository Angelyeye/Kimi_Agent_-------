# 🧧 春节模拟器 (Spring Festival Simulator)

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-brightgreen)](https://yourusername.github.io/spring-festival-simulator/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

> 🎮 一款生存模拟 + 叙事选择的Web小游戏，体验春节回家的酸甜苦辣！

## 📖 游戏简介

《春节模拟器》是一款以春节为背景的生存模拟游戏。玩家需要在9天的春节假期中，通过早/中/晚三个时间段的决策，影响角色的六大属性，最终走向不同的结局。

### ✨ 游戏特色

- 🎭 **10个独特角色**：从体制内霸总到脆皮大学生，每个角色都有独特的故事线
- 🎯 **六大属性系统**：存款、体重、面子、心情、健康、运气
- 📚 **100+事件**：专属事件 + 常规事件，每个事件都有多个选项
- 🔗 **蝴蝶效应**：你的选择会影响后续剧情发展
- 🏆 **50+结局**：成功、失败、特殊、隐藏结局等你解锁
- 📱 **跨平台**：支持PC和移动端，随时随地体验春节

## 🚀 快速开始

### 在线游玩

访问 [GitHub Pages 在线版](https://yourusername.github.io/spring-festival-simulator/) 即可开始游戏！

### 本地运行

```bash
# 克隆仓库
git clone https://github.com/yourusername/spring-festival-simulator.git

# 进入目录
cd spring-festival-simulator

# 用浏览器打开 index.html
open src/index.html
```

## 🎮 游戏玩法

1. **选择角色**：10个角色各有不同的初始属性和故事线
2. **做出选择**：每个时段都会触发事件，选择你的应对方式
3. **管理属性**：平衡六大属性，避免任何一项过低
4. **触发结局**：9天后根据你的属性触发不同结局

### 角色列表

| 角色 | 身份 | 特点 |
|------|------|------|
| 郝仕途 | 厅局风·编制内霸总 | 面子高，体制内话术 |
| 花贝贝 | 都市隶人·回村Vivian | 精致穷，Vivian变翠花 |
| 范统 | 脆皮大学生·特种兵 | 德华带娃，清澈又愚蠢 |
| 顾嘉 | 全职儿女·家务雇佣兵 | 新型啃老，家务全包 |
| 任兴 | 发疯学者·职场整顿版 | 拒绝精神内耗，直接发疯 |
| 郝有乾 | 隐形富豪·土味房东 | 人字拖POLO衫，腰上挂钥匙 |
| 毕成龙 | 鸡娃战神·绝望家长 | 春节也要鸡娃，红包回收站 |
| 甄洋气 | 海归凡尔赛·假装名流 | 中英夹杂，Gap Year掩饰失业 |
| 胡三万 | 川渝雀圣·熬夜修仙党 | 三缺一绝对不行，血战到底 |
| 吴仁爱 | 大龄剩斗士·相亲遇难 | 滞销库存，相亲KPI |

## 📁 项目结构

```
spring-festival-simulator/
├── src/                    # 源代码
│   ├── index.html          # 主页面
│   ├── styles.css          # 样式文件
│   ├── game.js             # 游戏逻辑
│   └── assets/             # 图片资源
├── data/                   # 游戏数据
│   ├── characters.json     # 角色数据
│   ├── character_events.json # 角色专属事件
│   ├── common_events.json  # 常规事件
│   └── endings.json        # 结局数据
├── docs/                   # 文档
└── README.md               # 本文件
```

## 🛠️ 技术栈

- **前端**：HTML5 + CSS3 + JavaScript (ES6+)
- **存储**：LocalStorage 本地存档
- **部署**：GitHub Pages

## 📝 开发文档

- [系统架构文档](docs/系统架构文档.md)
- [UI设计文档](docs/UI设计文档.md)
- [策划规范文档](docs/策划规范文档.md)

## 🤝 贡献指南

欢迎提交Issue和Pull Request！

1. Fork 本仓库
2. 创建你的特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交你的修改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 打开一个 Pull Request

## 📄 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

## 🙏 致谢

- 感谢所有参与开发的策划、程序、测试人员
- 感谢所有提供灵感的网络热梗创作者
- 感谢每一个体验游戏的玩家

---

🧧 **新年快乐，大吉大利！** 🧧
