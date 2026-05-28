# Lime Recommendation Formulas for Tropical Acid Soils

## 小组成员
- 组长：屈文龙
- 组员：阿布都拉 韦佳妮 涂雨涵 侯坤均
  
---

## 项目信息
- **论文标题**：Estimating lime requirements for tropical soils: Model comparison and development
- **相关软件/包**：Positron
- **代码和数据链接**：本仓库包含复现石灰推荐公式的 R 代码及示例数据

---

## 复现目标与核心内容
本项目在 R 环境中完整实现了多种热带酸性土壤石灰需要量计算公式，核心目标包括：
1. 实现 Kamprath、Cochrane、NuMaSS 及巴西 V 法的石灰推荐逻辑
2. 生成与原始文献一致的铝饱和度下降曲线、预测值与实际值对比图
3. 提供单位转换（meq/100g ↔ 吨/公顷）及石灰材料等效性调整功能

---

## 项目结构说明
```
.
├── R/                    # 核心函数（limeRate, convert, CCE 等）
├── data/                 # 示例数据集（kamp, coch）
├── vignettes/            # 详细说明文档（Lime_recommendation_formulas.Rmd）
├── plot and figure/      # 复现的图表
├── README.md             # 项目说明
└── DESCRIPTION           # R 包元数据
```

---

## 环境配置与依赖安装

### 1. 创建 R 环境（推荐使用 renv 或 Conda）
```r
# 安装 limer 包（开发版本）
install.packages("devtools")
devtools::install_github("yourusername/limer")
```

### 2. 安装核心依赖
```r
install.packages(c("ggplot2", "viridis", "knitr", "rmarkdown"))
```

### 3. 关键环境配置（处理图形输出）
```r
# 若使用 RStudio，确保绘图设备支持 png/pdf
options(bitmapType = "cairo")
```


---

## 使用示例
```r
library(limer)

# 计算 Cochrane 公式推荐的石灰用量（meq/100g）
lr_meq <- limeRate(
  data.frame(exch_Al = 2.5, ECEC = 5.0),
  method = "co",
  TAS = 15
)

# 转换为吨/公顷（容重 1.2 g/cm³，深度 20 cm）
lr_tha <- convert(lr_meq, bd = 1.2, depth = 20) * 1000
print(lr_tha)
```

---

## 复现图表说明
| 图号 | 内容 | 对应文件 |
|------|------|----------|
| 图1 | 铝饱和度随石灰用量的变化（Kamprath) | `figure/plot1.png` |
| 图2 | Cochrane 公式预测 vs 实际石灰用量 | `figure/plot2.png` |
| 图3 | NuMaSS 公式的两种解释对比 | `figure/plot4.png` |
| 图4 | Cochrane 与 NuMass 预测精度对比 | `figure/plot3.png` |
| 图5 | 铝饱和度与石灰用量的简化关系 | `figure/plot5.png` |

---


