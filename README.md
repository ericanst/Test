`npx create-react-app my-app`

*** 安装antd，注意按需加载 ***

`npm install antd --save`
`npm install babel-plugin-import --save-dev`

`yarn eject`

*** 若出错，可删除git隐藏文件，重试 ***


 "plugins": [
      [
        "import",
        {
          "libraryName": "antd",
          "style": "css"
        }
      ]
    ]



[问题解决](https://github.com/facebook/create-react-app/issues/12070)

`npm i less less-loader --save`
 
[安装less less-loader,注意less-loader版本过高](https://blog.csdn.net/wang_jun8072/article/details/106160036)

`yarn remove less-loader`
`yarn add less-loader@5.0.0`

*** 或 ***

`npm uninstall less-loader `
`npm cache clear -f `
`npm install less-loader@5.0.0`


*** 修改webpack ***



const lessRegex= /\.less$/;
const lessModuleRegex=/\.module\.less$/;

getStyleLoaders函数加 lessOptions
{
        loader: require.resolve('less-loader'),
        options: lessOptions,
      },



{
              test: lessRegex,
              exclude: lessModuleRegex,
              use: getStyleLoaders(
                  {
                    importLoaders: 3,
                    sourceMap: isEnvProduction
                    ? shouldUseSourceMap
                    : isEnvDevelopment,
                  },
                  'less-loader'
              ),
              sideEffects: true,
            },
            {
              test: lessModuleRegex,
              use: getStyleLoaders(
                  {
                    importLoaders: 3,
                    sourceMap: isEnvProduction
                    ? shouldUseSourceMap
                    : isEnvDevelopment,
                    modules: {
                      getLocalIdent: getCSSModuleLocalIdent,
                    },
                  },
                  'less-loader'
              ),
            },

*** 定制主题 ***
[参考](https://blog.csdn.net/sophieLV1993/article/details/104565192?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-104565192-blog-90672774.pc_relevant_downloadblacklistv1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-104565192-blog-90672774.pc_relevant_downloadblacklistv1&utm_relevant_index=2)


{
              test: /\.less$/,
              use: [{
                loader: 'style-loader',
              }, {
                loader: 'css-loader', // translates CSS into CommonJS
              }, {
                loader: 'less-loader', // compiles Less to CSS
                options: {
                  modifyVars: {
                    'primary-color': '#4E2CA3',
                  },
                  javascriptEnabled: true,
                },
              }]
            },


     "plugins": [
      [
        "import",
        {
          "libraryName": "antd",
          "libraryDirectory": "es",
          "style": true
        }
      ]
    ]
