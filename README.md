<h1 align='center'>
   <samp> Pictify </samp>
</h1>
<p align = 'center'>
  <samp> 获取懂球帝评论区无水印图片 </samp>
</p>

前几天在懂球帝看一个帖子，评论区里面有一张图片，我想保存下来，但是它有水印。

于是用 Qx 抓包看了一下，发现它返回的有无水印的地址。

但是每次抓包下载图片不够直观，看到评论区也经常有求原图的朋友，随手写了个网站，方便大家保存喜欢的图片。

## 如何使用

1. 找到想要保存的图片帖子，点击分享，复制帖子链接。
2. 粘贴地址到输入框中，点击 `获取评论数据`，会跳转到新页面。
3. 复制新页面的数据，粘贴到文本框中，点击 `查看图片`，即可。点击图片可预览大图

注：如果获取的图片仍然有水印，是因为评论的源图就是有水印版本的图片

## TODO

- [x] 保存帖子评论区的图片
- [ ] 保存帖子中的图片
