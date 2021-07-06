## yeoman的基本使用

- 环境的搭建

  ~~~ 
  全局下载安装yo命令
  npm i -g yo
  初始化项目
  npm init -y
  下载依赖
  npm i --save yeoman-generator
  切记package-json的name一定要以generator开头
  新建目录
  generator-name
  	generators/app
  		index.js
  ~~~

  

- 运行文件

  index.js

  ~~~
  var Generator = require('yeoman-generator');
  
  module.exports = class extends Generator {
    method1() {
      this.log('method 1 just ran');
    }
    method2() {
      this.log('method 2 just ran');
    }
  };
  ~~~

  在文件的根目录运行npm link命令

  ~~~
  npm link
  ~~~

  接着运行yo name(你的文件名)

  ~~~ 
  yo generator-name
  ~~~

  

- 命令行交互

  根据用户的输入进行交互

  index.js

  ~~~
  var Generator = require('yeoman-generator');
  
  module.exports = class extends Generator {
  // 注意这里需要使用async
   async method1() {
        const answers = await this.prompt([
          {
            type: "input",
            name: "name",
            message: "Your project name",
            default: this.appname // Default to current folder name
          },
          {
            type: "input",
            name: "title",
            message: "Would you like to enable the title feature?",
            default: '我是一个标题'
          }
        ]);
        
        this.log("app name", answers.name);
        this.log("app title", answers.title);
      }
  };
  ~~~

  

## babel的使用

- 安装babel

  全局安装Babel和Babel-cli，这样我们就可以全局的使用balel命令了

  ~~~
  npm i -g @babel/core @babel/cli
  ~~~

  

- babel的编译

  ~~~
  // 直接编译
  babel [name]
  // 将编译的文件存到指定的位置
  babel [name] > ../path
  ~~~

  

- 编译配置

  .babel.json文件设置

  ~~~
  {
  	// 谁知常用的Babel配置
  	"presets": ["@babel/preset-env"],
  	"plugins": [...]
  }
  ~~~

  

##  测试工具mocha的使用

- mocha的安装

  ~~~
  npm i -g mocha
  // 也可以局部安装
  npm i -D mocha
  ~~~

- 使用mocha

  我们简单的创建一个文件mkdir mochaTest

  然后再文件中输入：

  ~~~
  var assert = require('assert');
  
  it('should return -1 when the value is not present', function() {
  	// 判断输出结果是否位-1
        assert.equal([1,2,3].indexOf(4), -1);
   });
   
   // 断言
   describe('User', function() {
   	// 里面的内容会变成一个集合
   })
  ~~~

- mocha使用ES6模块语法

  mocha中默认是不不支持ES6模块化的，要想使用我必须借用我们Babel来实现

  ~~~
  // 下载依赖
  npm i -D @babel/core @babel/register @babel/preset-env
  ~~~

  配置值.babelrc文件

  ~~~
  {
      "presets": ["@babel/preset-env"]
  }
  ~~~

  在执行mocha [name]报错，我需要用register插件

  ~~~
  mocha --require @babel/register
  // 这个时候提示我们undefind未找到mocha
  // 这时候我们要是
  ./node_modules/.bin/mocha --require @babel/register
  ~~~

  

## nyc的使用

- 安装nyc

  ~~~
  npm i -D nyc
  ~~~

- 使用nyc

  ~~~
  npm run nyc mocha
  ~~~

  