title: grunt基础用法
date: 2015-11-14
tags: Grunt
---

### grunt基础用法

#### 1. grunt是什么？

#### 2. 准备阶段
1. **开发环境**
	- window7 64bit
	- nodejs v0.12.7
2. **安装nodejs环境**。Grunt和Grunt插件是通过`npm`安装并管理的，所以首先需要安装`nodejs`环境。
3. **全局安装`grunt-cli`**。为了更方便在任何目录下使用Grunt命令，我们需要在全局中安装`grunt-cli`

	```shell
	npm install -g grunt-cli
	```
4.**全局安装`grunt-init`**。`grunt-init`是一个用于自动创建项目脚手架的工具（就是提供项目文件的模板），比如我们在使用Grunt时，需要新建一个`gruntfile.js`文件，利用`grunt-init`中的`grunt-init-gruntfile`模板就可以直接生成了，详情请见：[grunt-init-gruntfile](https://github.com/gruntjs/grunt-init-gruntfile)

	``` shell
	npm install -g grunt-init
	```

#### 2. grunt的使用

1. **grunt概述**
![grunt使用使用](http://img2.ph.126.net/1aQ7dPg3wJz_1o9CrGGwSQ==/6631204105142711267.png)
- grunt-cli：grunt命令行，在系统全局环境中使用grunt命令；
- grunt-init：生成一些grunt的模板，主要是gruntfile；
- grunt：grunt默认导入了五个插件依赖。
		- concat：js文件的合并；
		- uglify：js文件的扰乱；
		- qunit：js文件的单元测试；
		- jshint：检验js的代码是否合法与规范；
		- watch：监控js文件的变化，包括增删改等。
2. **gruntfile配置**
	文章最下面附有生成默认的gruntfile的代码，下面我们分析每个模块
	- **包装函数（wrapper function）**
		每一份 Gruntfile （和grunt插件）都遵循同样的格式，你所书写的Grunt代码必须放在此函数内：
	```javascript
		/*global module:false*/
		module.exports = function(grunt) {
		  // 包含各种插件配置、注册和执行
		};
	```
	- **配置grunt插件（grunt.initConfig对象）**
		- 读取`package.json`中的JSON元数据 ，编写注释标题（banner）

		```javascript
		pkg: grunt.file.readJSON('package.json')
		banner: '/*! <%= pkg.title || pkg.name %> - v<%= pkg.version %> - ' +
        '<%= grunt.template.today("yyyy-mm-dd") %>\n' +
        '<%= pkg.homepage ? "* " + pkg.homepage + "\\n" : "" %>' +
        '* Copyright (c) <%= grunt.template.today("yyyy") %> <%= pkg.author.name %>;' +
        ' Licensed <%= _.pluck(pkg.licenses, "type").join(", ") %> */\n',
        ```

		- **js文件合并（concat）**

		```javascript
		concat: {
	        options: {
	          banner: '<%= banner %>',
	          stripBanners: true
	        },
	        dist: {
		      //源文件，把要压缩的文件以数组形式存入src
	          src: ['lib/<%= pkg.name %>.js'],
	          //目标目录与文件
	          dest: 'dist/<%= pkg.name %>.js'
	        }
	      },
		```
		
		- **js文件扰乱（uglify）**

		```javascript
		uglify: {
	        options: {
	          banner: '<%= banner %>'
	        },
	        dist: {
		      //源文件，需要被扰乱的js文件
	          src: '<%= concat.dist.dest %>',
	          //生成的目标文件
	          dest: 'dist/<%= pkg.name %>.min.js'
	        }
	      },
		```
		
		- **js文件检验（jshint）**
			jshint具体option配置信息请参考[jshint中文doc](http://www.cnblogs.com/code/articles/4103070.html)
		```javascript
		jshint: {
			//jshint的校验配置
	        options: {
	          curly: true,
	          eqeqeq: true,
	          immed: true,
	          latedef: true,
	          newcap: true,
	          noarg: true,
	          sub: true,
	          undef: true,
	          unused: true,
	          boss: true,
	          eqnull: true,
	          browser: true,
	          globals: {}
	        },
	        //配置要校验的文件，任务gruntfile
	        gruntfile: {
	          src: 'Gruntfile.js'
	        },
	        //配置要校验的文件，任务lib_test
	        lib_test: {
	          src: ['lib/**/*.js', 'test/**/*.js']
	        }
	      },
		```

		- **js文件单元测试（quint）**

		```javascript
		 qunit: {
			/*需要测试的文件，
			*单元测试对新手来说成本较高（包括我），起初不推荐
			*/
	        files: ['test/**/*.html']
	      },
		```
		
		- **监控js文件变化（watch）**
		
		```javascript
		watch: {
			/*配置任务gruntfile，
			*files：指监控的文件，
			*tasks：指当监控的文件变化中进行的任务
			*/
	        gruntfile: {
	          files: '<%= jshint.gruntfile.src %>',
	          tasks: ['jshint:gruntfile']
	        },
	        /*配置任务lib_test，
			*files：指监控的文件，
			*tasks：指当监控的文件变化中进行的任务
			*/
	        lib_test: {
	          files: '<%= jshint.lib_test.src %>',
	          tasks: ['jshint:lib_test', 'qunit']
	        }
	      }
		```

#### 3. gruntfile初始文档

	```javascript
		/*global module:false*/
	  module.exports = function(grunt) {
	
	    // Project configuration.
	    grunt.initConfig({
	      // Metadata.
	      pkg: grunt.file.readJSON('package.json'),
	      banner: '/*! <%= pkg.title || pkg.name %> - v<%= pkg.version %> - ' +
	        '<%= grunt.template.today("yyyy-mm-dd") %>\n' +
	        '<%= pkg.homepage ? "* " + pkg.homepage + "\\n" : "" %>' +
	        '* Copyright (c) <%= grunt.template.today("yyyy") %> <%= pkg.author.name %>;' +
	        ' Licensed <%= _.pluck(pkg.licenses, "type").join(", ") %> */\n',
	      // Task configuration.
	      concat: {
	        options: {
	          banner: '<%= banner %>',
	          stripBanners: true
	        },
	        dist: {
	          src: ['lib/<%= pkg.name %>.js'],
	          dest: 'dist/<%= pkg.name %>.js'
	        }
	      },
	      uglify: {
	        options: {
	          banner: '<%= banner %>'
	        },
	        dist: {
	          src: '<%= concat.dist.dest %>',
	          dest: 'dist/<%= pkg.name %>.min.js'
	        }
	      },
	      jshint: {
	        options: {
	          curly: true,
	          eqeqeq: true,
	          immed: true,
	          latedef: true,
	          newcap: true,
	          noarg: true,
	          sub: true,
	          undef: true,
	          unused: true,
	          boss: true,
	          eqnull: true,
	          browser: true,
	          globals: {}
	        },
	        gruntfile: {
	          src: 'Gruntfile.js'
	        },
	        lib_test: {
	          src: ['lib/**/*.js', 'test/**/*.js']
	        }
	      },
	      qunit: {
	        files: ['test/**/*.html']
	      },
	      watch: {
	        gruntfile: {
	          files: '<%= jshint.gruntfile.src %>',
	          tasks: ['jshint:gruntfile']
	        },
	        lib_test: {
	          files: '<%= jshint.lib_test.src %>',
	          tasks: ['jshint:lib_test', 'qunit']
	        }
	      }
	    });
	
	    // These plugins provide necessary tasks.
	    grunt.loadNpmTasks('grunt-contrib-concat');
	    grunt.loadNpmTasks('grunt-contrib-uglify');
	    grunt.loadNpmTasks('grunt-contrib-qunit');
	    grunt.loadNpmTasks('grunt-contrib-jshint');
	    grunt.loadNpmTasks('grunt-contrib-watch');
	
	    // Default task.
	    grunt.registerTask('default', ['jshint', 'qunit', 'concat', 'uglify']);
	
	  };
	```