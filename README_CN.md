# 城市地图海报生成器

为世界任何城市生成精美、极简风格的地图海报。

<img src="posters/singapore_neon_cyberpunk_20260118_153328.png" width="250">
<img src="posters/dubai_midnight_blue_20260118_140807.png" width="250">

## 示例

| 国家      | 城市           | 主题           | 海报 |
|:------------:|:--------------:|:---------------:|:------:|
| 美国        | 旧金山        | sunset          | <img src="posters/san_francisco_sunset_20260118_144726.png" width="250"> |
| 西班牙      | 巴塞罗那      | warm_beige      | <img src="posters/barcelona_warm_beige_20260118_140048.png" width="250"> |
| 意大利      | 威尼斯         | blueprint       | <img src="posters/venice_blueprint_20260118_140505.png" width="250"> |
| 日本        | 东京          | japanese_ink    | <img src="posters/tokyo_japanese_ink_20260118_142446.png" width="250"> |
| 印度        | 孟买         | contrast_zones  | <img src="posters/mumbai_contrast_zones_20260118_145843.png" width="250"> |
| 摩洛哥      | 马拉喀什      | terracotta      | <img src="posters/marrakech_terracotta_20260118_143253.png" width="250"> |
| 新加坡      | 新加坡      | neon_cyberpunk  | <img src="posters/singapore_neon_cyberpunk_20260118_153328.png" width="250"> |
| 澳大利亚    | 墨尔本      | forest          | <img src="posters/melbourne_forest_20260118_153446.png" width="250"> |
| 阿联酋        | 迪拜          | midnight_blue   | <img src="posters/dubai_midnight_blue_20260118_140807.png" width="250"> |
| 美国        | 西雅图        | emerald         | <img src="posters/seattle_emerald_20260124_162244.png" width="250"> |

## 安装

### 使用 uv（推荐）

确保已安装 [uv](https://docs.astral.sh/uv/)。在脚本前加 `uv run` 会自动创建和管理虚拟环境。

```bash
# 首次运行会自动安装依赖
uv run ./create_map_poster.py --city "Paris" --country "France"

# 或先显式同步依赖（使用锁定版本）
uv sync --locked
uv run ./create_map_poster.py --city "Paris" --country "France"
```

### 使用 pip + venv

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## 使用方法

### 生成海报

**模式 1：城市 + 国家**
```bash
uv run ./create_map_poster.py --city <城市> --country <国家> [选项]
```

**模式 2：坐标（无需城市名）**
```bash
uv run ./create_map_poster.py --latitude <纬度> --longitude <经度> [选项]
```

或使用（pip + venv）：
```bash
python create_map_poster.py --city <城市> --country <国家> [选项]
# 或
python create_map_poster.py --latitude <纬度> --longitude <经度> [选项]
```

### 必需参数

选择一种模式：

**选项 A：城市 + 国家**
| 参数 | 简写 | 说明 |
|--------|-------|-------------|
| `--city` | `-c` | 城市名称（用于地理编码） |
| `--country` | `-C` | 国家名称（用于地理编码） |

**选项 B：坐标**
| 参数 | 简写 | 说明 |
|--------|-------|-------------|
| `--latitude` | `-lat` | 中心点纬度 |
| `--longitude` | `-long` | 中心点经度 |

### 可选参数

| 参数 | 简写 | 说明 | 默认值 |
|--------|-------|-------------|---------|
| `--latitude` | `-lat` | 中心点纬度（与 --longitude 一起使用，或作为城市的替代） | |
| `--longitude` | `-long` | 中心点经度（与 --latitude 一起使用，或作为城市的替代） | |
| `--location-label` | `-l` | 自定义位置标签（使用坐标时，或覆盖城市名） | |
| `--country-label` | | 覆盖海报上显示的国家文字 | |
| `--theme` | `-t` | 主题名称 | terracotta |
| `--distance` | `-d` | 地图半径（米） | 18000 |
| `--list-themes` | | 列出所有可用主题 | |
| `--all-themes` | | 为所有可用主题生成海报 | |
| `--width` | `-W` | 图片宽度（英寸） | 12（最大：20） |
| `--height` | `-H` | 图片高度（英寸） | 16（最大：20） |

### 多语言支持 - i18n

使用 Google Fonts 的自定义字体以您的语言显示城市和国家名称：

| 参数 | 简写 | 说明 |
|--------|-------|-------------|
| `--display-city` | `-dc` | 自定义城市显示名称（如："東京"） |
| `--display-country` | `-dC` | 自定义国家显示名称（如："日本"） |
| `--font-family` | | Google 字体系列名称（如："Noto Sans JP"） |

**示例：**

```bash
# 日语
python create_map_poster.py -c "Tokyo" -C "Japan" -dc "東京" -dC "日本" --font-family "Noto Sans JP"

# 韩语
python create_map_poster.py -c "Seoul" -C "South Korea" -dc "서울" -dC "대한민국" --font-family "Noto Sans KR"

# 阿拉伯语
python create_map_poster.py -c "Dubai" -C "UAE" -dc "دبي" -dC "الإمارات" --font-family "Cairo"
```

**注意**：字体会自动从 Google Fonts 下载并缓存在 `fonts/cache/` 中。

### 分辨率指南（300 DPI）

使用 `-W` 和 `-H` 的这些值来达到特定分辨率：

| 目标 | 分辨率（像素） | 英寸（-W / -H） |
|--------|-----------------|------------------|
| **Instagram 帖子** | 1080 x 1080 | 3.6 x 3.6 |
| **手机壁纸** | 1080 x 1920 | 3.6 x 6.4 |
| **HD 壁纸** | 1920 x 1080 | 6.4 x 3.6 |
| **4K 壁纸** | 3840 x 2160 | 12.8 x 7.2 |
| **A4 打印** | 2480 x 3508 | 8.3 x 11.7 |

### 示例

#### 基础示例
```bash
# 使用默认主题的简单用法
python create_map_poster.py -c "Paris" -C "France"

# 自定义主题和距离
python create_map_poster.py -c "New York" -C "USA" -t noir -d 12000
```

#### 多语言示例（非拉丁字母）

以母语显示城市名称：

```bash
# 日语
python create_map_poster.py -c "Tokyo" -C "Japan" -dc "東京" -dC "日本" --font-family "Noto Sans JP" -t japanese_ink

# 韩语
python create_map_poster.py -c "Seoul" -C "South Korea" -dc "서울" -dC "대한민국" --font-family "Noto Sans KR" -t midnight_blue

# 泰语
python create_map_poster.py -c "Bangkok" -C "Thailand" -dc "กรุงเทพมหานคร" -dC "ประเทศไทย" --font-family "Noto Sans Thai" -t sunset

# 阿拉伯语
python create_map_poster.py -c "Dubai" -C "UAE" -dc "دبي" -dC "الإمارات" --font-family "Cairo" -t terracotta

# 中文（简体）
python create_map_poster.py -c "Beijing" -C "China" -dc "北京" -dC "中国" --font-family "Noto Sans SC"

# 高棉语
python create_map_poster.py -c "Phnom Penh" -C "Cambodia" -dc "ភ្នំពេញ" -dC "កម្ពុជា" --font-family "Noto Sans Khmer"
```

#### 高级示例
```bash
# 标志性网格图案
python create_map_poster.py -c "New York" -C "USA" -t noir -d 12000           # 曼哈顿网格
python create_map_poster.py -c "Barcelona" -C "Spain" -t warm_beige -d 8000   # 扩展区

# 水岸和运河
python create_map_poster.py -c "Venice" -C "Italy" -t blueprint -d 4000       # 运河网络
python create_map_poster.py -c "Amsterdam" -C "Netherlands" -t ocean -d 6000  # 同心运河
python create_map_poster.py -c "Dubai" -C "UAE" -t midnight_blue -d 15000     # 棕榈树和海岸线

# 辐射状图案
python create_map_poster.py -c "Paris" -C "France" -t pastel_dream -d 10000   # 奥斯曼大道
python create_map_poster.py -c "Moscow" -C "Russia" -t noir -d 12000          # 环路

# 有机老城市
python create_map_poster.py -c "Tokyo" -C "Japan" -t japanese_ink -d 15000    # 密集有机街道
python create_map_poster.py -c "Marrakech" -C "Morocco" -t terracotta -d 5000 # 麦地那迷宫
python create_map_poster.py -c "Rome" -C "Italy" -t warm_beige -d 8000        # 古老布局

# 沿海城市
python create_map_poster.py -c "San Francisco" -C "USA" -t sunset -d 10000    # 半岛网格
python create_map_poster.py -c "Sydney" -C "Australia" -t ocean -d 12000      # 港口城市
python create_map_poster.py -c "Mumbai" -C "India" -t contrast_zones -d 18000 # 沿海半岛

# 河流城市
python create_map_poster.py -c "London" -C "UK" -t noir -d 15000              # 泰晤士河曲线
python create_map_poster.py -c "Budapest" -C "Hungary" -t copper_patina -d 8000  # 多瑙河分岔
```

#### 基于坐标的示例

使用精确坐标生成地图，无需城市/国家名称：

```bash
# 在特定坐标生成地图（无文字标签）
python create_map_poster.py --latitude 48.8566 --longitude 2.3522 -t noir -d 8000

# 使用自定义位置标签（标签将显示在海报上）
python create_map_poster.py -lat 40.7128 -long -74.0060 -l "New York City" -t neon_cyberpunk

# 特定社区不使用完整城市名
python create_map_poster.py --latitude 35.6762 --longitude 139.6503 -l "Shinjuku" -t japanese_ink -d 8000

# 带有自定义名称的远程位置
python create_map_poster.py -lat 21.3069 -long -157.8583 -l "North Shore, Oahu" -t ocean -d 10000
```

**注意：** 使用坐标（`--latitude` + `--longitude`）而不使用城市/国家时，文字标签会自动隐藏以呈现干净的极简外观。如果您想要文字，请添加 `--location-label`。

#### 其他示例
```bash
# 使用城市名覆盖中心坐标
python create_map_poster.py --city "New York" --country "USA" -lat 40.776676 -long -73.971321 -t noir

# 列出可用主题
python create_map_poster.py --list-themes

# 为所有主题生成海报
python create_map_poster.py -c "Tokyo" -C "Japan" --all-themes
```

### 距离指南

| 距离 | 最适合 |
|----------|----------|
| 4000-6000米 | 小型/密集城市（威尼斯、阿姆斯特丹中心） |
| 8000-12000米 | 中型城市，聚焦市中心（巴黎、巴塞罗那） |
| 15000-20000米 | 大都市，全景城市视图（东京、孟买） |

## 主题

`themes/` 目录中提供 17 个主题：

| 主题 | 风格 |
|-------|-------|
| `gradient_roads` | 平滑渐变着色 |
| `contrast_zones` | 高对比度城市密度 |
| `noir` | 纯黑背景，白路 |
| `midnight_blue` | 海军蓝背景配金色道路 |
| `blueprint` | 建筑蓝图美学 |
| `neon_cyberpunk` | 深色配电粉/青色 |
| `warm_beige` | 复古褐色调 |
| `pastel_dream` | 柔和淡调 |
| `japanese_ink` | 极简水墨风格 |
| `emerald` | 郁郁葱葱的深绿美学 |
| `forest` | 深绿和鼠尾草绿 |
| `ocean` | 适合沿海城市的蓝青色调 |
| `terracotta` | 地中海温暖色调 |
| `sunset` | 温暖橙色和粉色 |
| `autumn` | 季节性焦橙和红色 |
| `copper_patina` | 氧化铜美学 |
| `monochrome_blue` | 单一蓝色系 |

## 输出

海报保存到 `posters/` 目录，格式为：
```
{城市}_{主题}_{YYYYMMDD_HHMMSS}.png
```

## 添加自定义主题

在 `themes/` 目录中创建 JSON 文件：

```json
{
  "name": "My Theme",
  "description": "主题描述",
  "bg": "#FFFFFF",
  "text": "#000000",
  "gradient_color": "#FFFFFF",
  "water": "#C0C0C0",
  "parks": "#F0F0F0",
  "road_motorway": "#0A0A0A",
  "road_primary": "#1A1A1A",
  "road_secondary": "#2A2A2A",
  "road_tertiary": "#3A3A3A",
  "road_residential": "#4A4A4A",
  "road_default": "#3A3A3A"
}
```

## 项目结构

```
map_poster/
├── create_map_poster.py    # 主脚本
├── font_management.py      # 字体加载和 Google Fonts 集成
├── themes/                 # 主题 JSON 文件
├── fonts/                  # 字体文件
│   ├── Roboto-*.ttf        # 默认 Roboto 字体
│   └── cache/              # 下载的 Google Fonts（自动生成）
├── posters/                # 生成的海报
└── README.md
```

## 黑客指南

贡献者快速参考，用于扩展或修改脚本。

### 架构概览

```
┌─────────────────┐     ┌──────────────┐     ┌─────────────────┐
│   CLI 解析器    │────▶│  地理编码   │────▶│  数据获取       │
│   (argparse)    │     │  (Nominatim) │     │    (OSMnx)      │
└─────────────────┘     └──────────────┘     └─────────────────┘
                                                     │
                        ┌──────────────┐             ▼
                        │    输出      │◀────┌─────────────────┐
                        │  (matplotlib)│     │   渲染         │
                        └──────────────┘     │  (matplotlib)   │
                                             └─────────────────┘
```

### 关键函数

| 函数 | 目的 | 在...时修改 |
|----------|---------|----------------|
| `get_coordinates()` | 通过 Nominatim 将城市转换为纬度/经度 | 切换地理编码提供商 |
| `create_poster()` | 主渲染管道 | 添加新地图层 |
| `get_edge_colors_by_type()` | 根据 OSM 公路标签设置道路颜色 | 更改道路样式 |
| `get_edge_widths_by_type()` | 根据重要性设置道路宽度 | 调整线条粗细 |
| `create_gradient_fade()` | 顶部/底部淡出效果 | 修改渐变叠加 |
| `load_theme()` | JSON 主题 → 字典 | 添加新主题属性 |
| `is_latin_script()` | 检测排版脚本 | 支持新脚本 |
| `load_fonts()` | 加载自定义/默认字体 | 更改字体加载逻辑 |

### 渲染层级（z 顺序）

```
z=11  文字标签（城市、国家、坐标）
z=10  渐变淡出（顶部和底部）
z=3   道路（通过 ox.plot_graph）
z=2   公园（绿色多边形）
z=1   水域（蓝色多边形）
z=0   背景颜色
```

### OSM 公路类型 → 道路层级

```python
# 在 get_edge_colors_by_type() 和 get_edge_widths_by_type() 中
motorway, motorway_link     → 最粗（1.2），最深色
trunk, primary              → 粗（1.0）
secondary                   → 中（0.8）
tertiary                    → 细（0.6）
residential, living_street  → 最细（0.4），最浅色
```

### 排版和脚本检测

脚本会自动检测文本脚本以应用适当的排版：

- **拉丁字母**（英语、法语、西班牙语等）：应用字母间距以获得优雅的 "P  A  R  I  S" 效果
- **非拉丁字母**（日语、阿拉伯语、泰语、韩语等）：自然间距 "東京"（字符间无间隙）

脚本检测使用 Unicode 范围（拉丁字母为 U+0000-U+024F）。如果超过 80% 的字母是拉丁字母，则应用间距。

### 添加新功能

**新地图层（如铁路）：**
```python
# 在 create_poster() 中，获取公园后：
try:
    railways = ox.features_from_point(point, tags={'railway': 'rail'}, dist=dist)
except:
    railways = None

# 然后在道路前绘制：
if railways is not None and not railways.empty:
    railways.plot(ax=ax, color=THEME['railway'], linewidth=0.5, zorder=2.5)
```

**新主题属性：**
1. 添加到主题 JSON：`"railway": "#FF0000"`
2. 在代码中使用：`THEME['railway']`
3. 在 `load_theme()` 默认字典中添加回退值

### 排版定位

所有文本使用 `transform=ax.transAxes`（0-1 归一化坐标）：
```
y=0.14  城市名称（拉丁字母的间距字母）
y=0.125 装饰线
y=0.10  国家名称
y=0.07  坐标
y=0.02  属性（右下角）
```

### 有用的 OSMnx 模式

```python
# 获取所有建筑
buildings = ox.features_from_point(point, tags={'building': True}, dist=dist)

# 获取特定设施
cafes = ox.features_from_point(point, tags={'amenity': 'cafe'}, dist=dist)

# 不同的网络类型
G = ox.graph_from_point(point, dist=dist, network_type='drive')  # 仅道路
G = ox.graph_from_point(point, dist=dist, network_type='bike')   # 自行车道
G = ox.graph_from_point(point, dist=dist, network_type='walk')   # 人行道
```

### 性能提示

- 大的 `dist` 值（>20 公里）= 下载慢 + 内存占用大
- 在本地缓存坐标以避免 Nominatim 速率限制
- 使用 `network_type='drive'` 而非 `'all'` 以加快渲染
- 将 `dpi` 从 300 降低到 150 以进行快速预览
