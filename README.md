#nodejs express学习

### 0 环境设置
(本框架是使用webstorm自带的node express 4.x工程模板，带了handlebars和sass
)

>本地安装node模块

    git clone 本项目
    npm install

>程序启动方式：

    node ./bin/www
浏览localhst:3000，显示首页。 Hello World成功！

### 第1课 express基本功能和结构

端口监听：bin/www

    var server = http.createServer(app);

设置路由：/app.js

    app.use('/', routes);
    app.use('/users', users);

app.use是express使用中间件（middleware）的方式。本来app直接设置路由的方式：

    app.get('/about*',function(req,res){ // send content....
    })
    app.get('/about/contact',function(req,res){
                // send content....
    })
使用路由中间件后变成了（routes/index.js）
    router.get('/', function(req, res, next) {
      res.render('index', { title: 'Express' });
    });

通过express的路由中间件，每个功能模块可以自定义自己的路由并封装在独立的js文件里

express设置了渲染引擎为handlebars后，response返回时可以使用handlebars做服务器端模板

    res.render('index', { title: 'Express' });
    // 给模板实例化时传入变量参数
    if (app.get('env') === 'development') {
      app.use(function(err, req, res, next) {
        res.status(err.status || 500);
        res.render('error', {
          message: err.message,
          error: err
        });
      });
    }
对比不用模板的response：

    /* routes/users.js */
    router.get('/', function(req, res, next) {
      res.send('respond with a resource');
    });

express使用中间件static来处理静态文件：

    app.use(express.static(__dirname + '/public'));

TRY:尝试访问http://localhost:3000/users和http://localhost:3000/，找到相关的页面

###第2课 动手实现一个模块




