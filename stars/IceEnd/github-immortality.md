---
project: github-immortality
stars: 40
description: |-
    Dynamically generate stats for your GitHub readme
url: https://github.com/IceEnd/github-immortality
---

# GitHub Immortality ⚔️

[简体中文](./docs/README-ZH.md) | English

> Your GitHub Journey, Visualized as a Cultivation Path

A beautiful GitHub stats card inspired by the cultivation system from "A Record of a Mortal's Journey to Immortality" (凡人修仙传). Transform your GitHub contributions into a mystical cultivation journey with traditional Chinese aesthetics.

## ✨ Features

- 🎨 **Exquisite Design**: Hand-crafted SVG with traditional Chinese ink painting aesthetics
- 🌊 **Dynamic Effects**: Smooth water ripple animations and gradient transitions
- 📊 **Comprehensive Stats**: Tracks commits, PRs, issues, reviews, stars, and followers
- 🏆 **13 Cultivation Realms**: From Qi Refinement (练气) to Dao Ancestor (道祖)
- 🎭 **Intelligent Coloring**: Each realm has its unique color scheme harmonized with the background
- ⚡ **High Performance**: Powered by Vercel Edge Functions with smart caching
- 🔧 **Customizable**: Support for various parameters and themes (coming soon)

## 📖 Demo

[![IceEnd's GitHub stats](https://github-immortality.vercel.app/api?username=iceend)](https://github.com/IceEnd)

## 🚀 Quick Start

Simply add your GitHub username to the URL to get your cultivation stats card:

```markdown
![GitHub Stats](https://github-immortality.vercel.app/api?username=YOUR_USERNAME)
```

Replace `YOUR_USERNAME` with your actual GitHub username.

## 🎯 Cultivation Realms

The card calculates your cultivation realm based on your GitHub activities:

| Realm | Chinese | Requirements |
|-------|---------|--------------|
| 13 | 道祖 (Dao Ancestor) | Top 1% - Legendary contributors |
| 12 | 大罗 (Daluo Golden Immortal) | Top 5% - Masters of the craft |
| 11 | 太乙 (Taiyi True Immortal) | Top 10% - Distinguished developers |
| 10 | 金仙 (Golden Immortal) | Top 15% - Expert contributors |
| 9 | 真仙 (True Immortal) | Top 20% - Advanced developers |
| 8 | 大乘 (Great Vehicle) | Top 30% - Skilled practitioners |
| 7 | 合体 (Body Integration) | Top 40% - Experienced coders |
| 6 | 炼虚 (Void Refinement) | Top 50% - Proficient developers |
| 5 | 化神 (Soul Transformation) | Top 60% - Competent contributors |
| 4 | 元婴 (Nascent Soul) | Top 70% - Growing developers |
| 3 | 金丹 (Golden Core) | Top 80% - Active contributors |
| 2 | 筑基 (Foundation Establishment) | Top 90% - Regular contributors |
| 1 | 练气 (Qi Refinement) | Starting your journey |

### Ranking Algorithm

The cultivation realm is calculated using a weighted formula:

- ⭐ **Stars**: 6x weight - Represents project impact and recognition
- 👥 **Followers**: 4x weight - Personal influence and community presence
- 🔀 **Pull Requests**: 3x weight - Substantial contributions to open source
- 👁️ **Code Reviews**: 2x weight - Code quality and mentorship
- 🐛 **Issues**: 2x weight - Problem-solving abilities
- 💻 **Commits**: 1x weight - Daily cultivation (anti-spam weighted)

## 📜 License

[MIT License](LICENSE) © Alchemy

---

<div align="center">
  <sub>May your cultivation path be prosperous! 🌟</sub>
</div>

