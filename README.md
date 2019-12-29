这是一个用于测试vue项目跨域的简单项目，很纯净，只有跨域访问的功能。使用方式如下：

1、clone本项目到本地，使用vscode编辑器打开项目，编辑器无所谓；
2、在开发环境中进行调试：打开conf->index.js 文件，在proxyTable: {}中添加代码
    '/api': {
        target: 'https://www.runoob.com',//请求域名
        //secure: false, // 如果是https接口，需要配置这个参数
        changeOrigin: true,//如果是跨域访问，需要配置这个参数
        pathRewrite: {
          '^/api': ''
        }
      }
或者将注释打开；
在src/components/HelloWorld 这个vue文件中，有对跨域设置的使用；
之后直接在终端中执行命令 npm run dev，即可在测试地址首页看到得到的json打印在网页上；
3、在生产环境的使用：
第一步，需要将刚才的代码段注释，然后执行指令： npm run build,得到静态文件夹dist；
第二部，在发布的操作系统中安装Nginx服务器，然后将项目发布上去，比如新建路径/usr/local/webapps，将dist文件夹放到该路径，然后将Nginx的默认server的root指向到该路径“/usr/local/webapps/dist/”
第三步，在默认server中增加代码段
location /api/ {
  proxy_pass https://www.runoob.com/;
 }
这里的"/api/"是根据前端vue项目中设定的标识而定的。
在Nginx遇到/api/字符串后自动会将/api/替换成https://www.runoob.com/
启动Nginx服务器，进行测试，即可得到开发环境一致的效果

这是本人的一个测试，顺便在这里测试项目的上传，还有很多坑要走，一定要坚持下去！
# happy

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
