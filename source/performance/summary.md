## 加载图片，浏览器要不断计算宽高
！！！
srcset sizes

## FOUC（无样式内容闪烁）
CSS文件的@import就是造成这个问题的罪魁祸首

IE会先加载完DOM结构，再加载导入的外部css。解决：在它之后加上<link>或<script>


## 前端性能优化有哪些
