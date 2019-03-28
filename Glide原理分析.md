## Glide原理分析

### 1. 问题

- Glide是如何加载图片资源的
- Glide的缓存策略是如何实现的
- Glide的优势与弊端

### 2. Glide图片是如何加载图片资源的

首先看看是如何使用Glide的

```
Glide.with(context)
  .asBitmap()
  .load(url)
  .into(imageView);
```



