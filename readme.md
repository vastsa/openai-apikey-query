# 构建教程
```shell
# 安装依赖
pnpm install
# 构建
pnpm build
```
# 案例
http://open.isvs.me/

# 可能需要修改的
## -> OpenAI 接口地址
src->components->TheWelcome.vue->line 6

## 尾部超链接
src->App.vue-> line 19

# 原理
调用官方面板的查询历史用量接口，然后进行计算
