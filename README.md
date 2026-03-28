# Word-Cloud 词云生成器

基于 Python 的中文词云生成工具，可将聊天记录或任意中文文本转化为以指定图片轮廓为形状的词云图。

## 功能简介

- 使用 [jieba](https://github.com/fxsjy/jieba) 对中文文本进行分词
- 通过停用词表过滤无意义词汇
- 支持自定义用户词典（`mywords.txt`）
- 以任意图片作为词云轮廓蒙版
- 词云颜色自动从蒙版图片中提取，风格统一

## 项目结构

```
Word-Cloud/
├── WordCloud.py       # 主程序
├── mywords.txt        # 用户自定义词典
├── stopwords.txt      # 停用词表
├── chat_records.txt   # 待分析的文本（需自行提供）
├── picture1.jpg       # 词云蒙版图片（需自行提供）
└── simhei.ttf         # 中文字体文件（需自行提供）
```

## 依赖安装

```bash
pip install jieba pandas matplotlib wordcloud imageio
```

> 中文字体文件 `simhei.ttf` 可从系统字体目录复制，或从网络下载后放置于项目根目录。

## 使用方法

1. 将待分析的中文文本保存为 `chat_records.txt`，编码为 UTF-8。
2. 准备一张用于形状蒙版的图片，命名为 `picture1.jpg`，放入项目目录。
3. （可选）在 `mywords.txt` 中添加 jieba 未能正确识别的专有词汇。
4. 根据实际路径修改 `WordCloud.py` 中的文件路径。
5. 运行主程序：

```bash
python WordCloud.py
```

运行后将弹出词云图预览窗口。

## 参数说明

| 参数 | 说明 | 默认值 |
|---|---|---|
| `width` / `height` | 词云画布尺寸（像素） | 1080 × 1080 |
| `background_color` | 背景颜色 | `white` |
| `max_words` | 最多显示词数 | 1000 |
| `scale` | 渲染缩放比例，值越大图片越清晰 | 10 |
| 词长过滤 | 仅保留长度为 2 ~ 5 个汉字的词语 | — |

若需透明背景，可将 `WordCloud` 初始化替换为：

```python
wordcloud = WordCloud(background_color=None, mode='RGBA', mask=bimg, font_path='simhei.ttf')
```

## 示例效果

将聊天记录导入后，词云将按词频渲染，出现频率越高的词语字体越大，整体轮廓与蒙版图片保持一致。

