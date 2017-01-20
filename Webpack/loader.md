在引用 loader 的时候可以使用全名 json-loader，或者使用短名 json。这个命名规则和搜索优先级顺序在 webpack 的 resolveLoader.moduleTemplates api 中定义。

Default: ["\*-webpack-loader", "\*-web-loader", "\*-loader", "*"]