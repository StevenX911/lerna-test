# lerna实践

- lerna
- yarn


#### 参考文章

- https://juejin.cn/post/6844903918279852046
- https://juejin.cn/post/6844903911095025678
- https://juejin.cn/post/6844903749232623629


#### FAQ：lerna 发布错误
* lerna http fetch PUT 404 https://registry.npmjs.org/@mo-demo%2fcli-shared-utils
    - 配置：`package.json > publishConfig > registry > https://registry.npmjs.org/`
* lerna ERR! E402 You must sign up for private packages
    - 配置：`package.json > publishConfig > access > public`
* lerna ERR! E404 Scope not found
    - 设置npm-scope: https://segmentfault.com/a/1190000017234785