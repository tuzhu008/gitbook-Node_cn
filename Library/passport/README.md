[![passport banner](http://cdn.auth0.com/img/passport-banner-github.png)](http://passportjs.org)

# Passport

[![Build](https://travis-ci.org/jaredhanson/passport.svg?branch=master)](https://travis-ci.org/jaredhanson/passport)
[![Coverage](https://coveralls.io/repos/jaredhanson/passport/badge.svg?branch=master)](https://coveralls.io/r/jaredhanson/passport)
[![Dependencies](https://david-dm.org/jaredhanson/passport.svg)](https://david-dm.org/jaredhanson/passport)
[![Tips](https://img.shields.io/gratipay/jaredhanson.svg)](https://gratipay.com/jaredhanson/)


Passport 是适用于 [Node.js](http://nodejs.org/) 身份验证中间件，与 [Express](http://expressjs.com/) 相兼容。

Passport 的唯一目的是验证请求，它通过一系列被称为 _策略（strategies）_ 的可扩展插件进行验证。
Passport 不会安装路由或假定任何特定的数据库模式，这可以最大限度地提高灵活性，并允许开发人员进行应用程序级别的决策。
API 非常简单：您提供 Passport 请求进行身份验证，Passport 提供钩子来控制身份验证成功或失败时发生的情况。

## 赞助


Passport 是由 [Rollbar](https://cs.berry.sh/c/f049ac4d-0d95-4f3e-9582-4fa1ab791591
) 荣耀赞助的。他们为开发人员提供实时的错误监控、警报和分析。您可以在 [https://rollbar.com](https://cs.berry.sh/c/f049ac4d-0d95-4f3e-9582-4fa1ab791591
)上免费试用 Rollbar。

## 安装

```
$ npm install passport
```

## 用法

#### 策略

Passport 使用策略的概念来认证请求。策略的范围可以从验证用户名和密码凭证，使用 [OAuth](http://oauth.net/) 进行委托身份验证（例如通过 Facebook](http://www.facebook.com/) 或 [Twitter](http://twitter.com/) ）或使用 [OpenID](http://openid.net/) 的联合身份验证。

在对请求进行身份验证之前，必须配置应用程序使用的策略（或策略s）。

```javascript
passport.use(new LocalStrategy(
  function(username, password, done) {
    User.findOne({ username: username }, function (err, user) {
      if (err) { return done(err); }
      if (!user) { return done(null, false); }
      if (!user.verifyPassword(password)) { return done(null, false); }
      return done(null, user);
    });
  }
));
```

这里有 300+ 的策略。找到你想要的: [passportjs.org](http://passportjs.org)

#### 会话

Passport 将保持持续登录会话。为了使持久性会话正常工作，经过身份验证的用户必须序列化到会话，并在进行后续请求时进行反序列化。

Passport 不会对您的用户记录存储方式施加任何限制。相反，你提供给 Passport 的函数需要实现必要的序列化和反序列化逻辑。在一个典型的应用程序中，这将像序列化用户 ID 一样简单，并在反序列化时通过 ID 查找用户。

```javascript
passport.serializeUser(function(user, done) {
  done(null, user.id);
});

passport.deserializeUser(function(id, done) {
  User.findById(id, function (err, user) {
    done(err, user);
  });
});
```

#### 中间件

要在 [Express](http://expressjs.com/) 或基于 [Connect](http://senchalabs.github.com/connect/) 的应用程序中使用 Passport，请使用所需的 `passport.initialize()` 中间件对其进行配置。 如果您的应用程序使用持久登录会话（建议但不是必需的），则还必须使用 `passport.session()` 中间件。

```javascript
var app = express();
app.use(require('serve-static')(__dirname + '/../../public'));
app.use(require('cookie-parser')());
app.use(require('body-parser').urlencoded({ extended: true }));
app.use(require('express-session')({ secret: 'keyboard cat', resave: true, saveUninitialized: true }));
app.use(passport.initialize());
app.use(passport.session());
```

#### 验证请求

Passport 提供一个 `authenticate()` 函数，它被用作路由中间件来验证请求。

```javascript
app.post('/login',
  passport.authenticate('local', { failureRedirect: '/login' }),
  function(req, res) {
    res.redirect('/');
  });
```

## 策略

Passport 拥有一整套**超过 300 种**认证策略，包括社交网络、企业集成、API 服务等等。


## 搜索所有策略

在 [passportjs.org](http://passportjs.org) 可以进行 **策略搜索**。

下表列出了常用的策略:

|策略                                                       | 协议                 |开发者                                       |
|---------------------------------------------------------------|--------------------------|------------------------------------------------|
|[Local](https://github.com/jaredhanson/passport-local)         | HTML form                |[Jared Hanson](https://github.com/jaredhanson)  |
|[OpenID](https://github.com/jaredhanson/passport-openid)       | OpenID                   |[Jared Hanson](https://github.com/jaredhanson)  |
|[BrowserID](https://github.com/jaredhanson/passport-browserid) | BrowserID                |[Jared Hanson](https://github.com/jaredhanson)  |
|[Facebook](https://github.com/jaredhanson/passport-facebook)   | OAuth 2.0                |[Jared Hanson](https://github.com/jaredhanson)  |
|[Google](https://github.com/jaredhanson/passport-google)       | OpenID                   |[Jared Hanson](https://github.com/jaredhanson)  |
|[Google](https://github.com/jaredhanson/passport-google-oauth) | OAuth / OAuth 2.0        |[Jared Hanson](https://github.com/jaredhanson)  |
|[Twitter](https://github.com/jaredhanson/passport-twitter)     | OAuth                    |[Jared Hanson](https://github.com/jaredhanson)  |
|[Azure Active Directory](https://github.com/AzureAD/passport-azure-ad)     | OAuth 2.0 / OpenID / SAML  |[Azure](https://github.com/azuread)  |

## 示例

- 对于一个完整的工作示例，请参考使用 [passport-local](https://github.com/jaredhanson/passport-local) 的[示例](https://github.com/passport/express-4.x-local-example)。
- **本地策略**: 参考下面的教程，通过 LocalStrategy (`passport-local`) 设置用户身份验证:
    - Mongo
      - Express v3x - [教程](http://mherman.org/blog/2016/09/25/node-passport-and-postgres/#.V-govpMrJE5) / [工作示例](https://github.com/mjhea0/passport-local-knex)
      - Express v4x - [教程](http://mherman.org/blog/2015/01/31/local-authentication-with-passport-and-express-4/) / [工作示例](https://github.com/mjhea0/passport-local-express4)
    - Postgres
      - [教程](http://mherman.org/blog/2015/01/31/local-authentication-with-passport-and-express-4/) / [工作示例](https://github.com/mjhea0/passport-local-express4)
- **社交身份验证**: 请参阅下面的教程，以建立各种社交身份验证策略:
    - Express v3x - [教程](http://mherman.org/blog/2013/11/10/social-authentication-with-passport-dot-js/) / [工作示例](https://github.com/mjhea0/passport-examples)
    - Express v4x - [教程](http://mherman.org/blog/2015/09/26/social-authentication-in-node-dot-js-with-passport) / [工作示例](https://github.com/mjhea0/passport-social-auth)

## 相关模块

- [Locomotive](https://github.com/jaredhanson/locomotive) — 强大的 MVC web 框架
- [OAuthorize](https://github.com/jaredhanson/oauthorize) —OAuth 服务提供者工具包
- [OAuth2orize](https://github.com/jaredhanson/oauth2orize) — OAuth 2.0 授权服务器工具箱
- [connect-ensure-login](https://github.com/jaredhanson/connect-ensure-login)  — 确保登录会话的中间件



[wiki](https://github.com/jaredhanson/passport/wiki)  上的 [modules](https://github.com/jaredhanson/passport/wiki/Modules) 页面列出了其他有用的模块，这些模块可以构建或集成到 Passport 上。

## 测试

```
$ npm install
$ make test
```

## 关于作者

  - [Jared Hanson](http://github.com/jaredhanson)

## 支持

这个项目得到了 ![](http://passportjs.org/images/supported_logo.svg) [Auth0](https://auth0.com) 的支持。

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2011-2015 Jared Hanson <[http://jaredhanson.net/](http://jaredhanson.net/)>
