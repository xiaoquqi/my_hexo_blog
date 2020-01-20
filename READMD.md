# 常用命令

## 建立文章草稿

```
hexo new draft <title>
```

## 本机预览草稿

```
hexo S --draft
```

## 将草稿发布为正式文章

```
hexo P <filename>
```

其中 <filename> 为不包含 md 后缀的文章名称。它的原理只是将文章从 source/_drafts 移动到 source/_posts 而已。
