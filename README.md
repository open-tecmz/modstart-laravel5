<p align="center">
  <a href="https://modstart.com">
    <img src="https://ms-assets.modstart.com/data/image/2021/09/08/23652_1f1j_9825.png" alt="ModStart" width="360" />
  </a>
</p>
<p align="center">
  基于 Laravel 5.1 的轻量模块化建站框架
</p>

<p align="center">
  <a href="https://modstart.com" target="_blank">
    <img alt="Framework ModStart" src="https://img.shields.io/badge/Framework-ModStart-blue">
  </a>
  <a href="https://laravel.com" target="_blank">
    <img alt="Laravel 5.1" src="https://img.shields.io/badge/Laravel-5.1-red">
  </a>
  <a href="https://www.php.net" target="_blank">
    <img alt="PHP 5.6 / 7.0" src="https://img.shields.io/badge/PHP-5.6%20%2F%207.0-red">
  </a>
  <a href="https://www.mysql.com" target="_blank">
    <img alt="MySQL 5.x" src="https://img.shields.io/badge/MySQL-5.x-orange">
  </a>
  <a href="https://vuejs.org" target="_blank">
    <img alt="Vue / Element UI" src="https://img.shields.io/badge/JS-Vue%20%2F%20ElementUI-green">
  </a>
</p>

# 轻量模块化建站框架

## 🔥 功能一览

- 欢迎首页：`Welcome` 模块提供介绍型首页，介绍 ModStart 能力并提供后台 / 文档 / 模块市场入口
- 导航管理：`Nav` 模块支持头部、底部、底部次导航等多位置导航配置
- 站点设置：`Site` 模块统一配置网站名称、Logo、关键词、描述、备案信息与主题
- 后台管理：`AdminManager` 提供基于 RBAC 的权限管理，多管理员多角色，手机 / 平板 / PC 均可管理
- 模块市场：`ModuleStore` 支持模块安装、卸载、升级
- 基础能力：ModStart 基础库提供文件上传、分片上传与数据存储；`Vendor` 模块提供验证码、事件、Provider 等通用能力

## 💡 系统简介

本项目是一个基于 **Laravel 5.1** 的轻量模块化建站框架，运行于 **PHP 5.6 / 7.0**，底座为 **ModStart 6.0.0** 基础库。

`config/module.php` 默认只注册 6 个基础模块（`Vendor`、`AdminManager`、`ModuleStore`、`Site`、`Nav`、`Welcome`），后台菜单和路由更少。

未启用 `Member` 时，`app/Web/routes.php` 与 `app/Api/routes.php` 不会挂载会员页面路由和会员鉴权中间件；安装并启用 `Member` 后自动生效。

`module/` 下的每个模块通过 `config.json` 的 `env` 字段声明兼容环境，本仓库按 `laravel5` 运行。

- [ModStart 官方网站](https://modstart.com)
- [模块市场](https://modstart.com/store)
- [开发文档](https://modstart.com/doc)

**技术栈**

- [Laravel 5.1](https://laravel.com/)
- [ModStart 基础库](https://modstart.com/doc)
- [Vue](https://vuejs.org/)
- [Element UI](https://element.eleme.io/)
- [jQuery](http://jquery.com)

## 💥 系统特性

- 全模块化开发，积木式搭建系统，可灵活组合
- 简洁优雅、灵活可扩展，可实现大型复杂系统
- 后台 RBAC 权限管理，多管理员多角色管理
- 丰富的数据表格、数据表单、数据详情功能
- 丰富的模块市场，后台一键快速安装

## 🎁 模块市场

丰富的模块市场，后台一键安装模块应用

![模块市场](https://ms-assets.modstart.com/data/image/2022/01/12/21242_me7h_4616.jpg)

## 🌐 开发文档

[https://modstart.com/doc](https://modstart.com/doc)

## 🔧 系统安装

### 环境要求

| 项目 | 要求 |
|---|---|
| PHP | `5.6` / `7.0` |
| MySQL | `>= 5.0`，建议 `5.6` / `5.7`；MySQL 8.0 默认认证插件与老版本 PHP 驱动不兼容，需额外处理 |
| PHP 扩展 | `fileinfo`、`pdo_mysql`、`mbstring`、`openssl`、`curl`、`gd`、`zip`、`exif`、`bcmath`、`tokenizer`、`iconv` |
| 禁用函数 | 确保 `proc_open`、`proc_get_status`、`putenv` 未被 `disable_functions` 禁用 |
| PHP 5.6 配置 | 需设置 `always_populate_raw_post_data=-1` |
| Web 服务器 | `Nginx` / `Apache`，需支持 Rewrite，站点根目录指向 `public/` |
| Composer | PHP 5.6 / 7.0 环境使用 Composer 2.2 LTS（Composer 2.3+ 需要 PHP 7.2.5+） |

### 安装向导

站点根目录必须指向项目的 `public/` 目录；如果实际访问地址是 `http://your-domain/public/install.php`，说明根目录配置有误，安装器也会给出提示。

```
Nginx:  root /path/to/modstart-laravel5/public;
Apache: DocumentRoot "/path/to/modstart-laravel5/public"
```

部署代码并完成 `composer install` 后，浏览器访问：

```
http://your-domain/install.php
```

向导页面在 `public/install.php`，逻辑在 `module/Vendor/Installer/install.php`，接口为
`module/Vendor/Web/routes.php` 中的 `install/ping`、`install/prepare`、`install/execute`。

向导依次为：安装协议（存在 `license_url.txt` 时）→ 环境检查 → 配置安装。

1. **安装协议**：阅读并同意《软件安装许可协议》；
2. **环境检查**：PHP 版本、扩展、目录可写、`always_populate_raw_post_data=-1`（PHP 5.6）、Rewrite 规则（`/install/ping` 返回 `ok` 才算通过）与 `.env` 可写性；
3. **配置安装**：填写 MySQL 连接与后台管理员账号 → `/install/prepare` 校验数据库连接并按 `env.example` 生成 `.env` → `/install/execute` 执行 `migrate`、创建管理员、按依赖顺序安装已注册模块（默认即 6 个基础模块），最后写入 `storage/install.lock`；如 `public/data_demo/data.php` 存在，向导还会提供「初始化安装演示数据」选项。

注意：

- 需要重装时，先删除 `storage/install.lock`，清空目标数据库中的表，再删除 `.env`（或删除其中所有 `DB_HOST` / `DB_*` 行，确保文件里不再出现 `DB_HOST` 字样）；`prepare` 对仍含 `DB_HOST` 的 `.env` 会返回「请先清空.env文件」；
- 向导从 `env.example` 生成 `.env`，其中的 `APP_KEY`、`ENCRYPT_KEY` 由安装器随机生成；
- 安装完成后建议删除 `public/install.php`（保留也可，向导会提示「系统无需重复安装」）。

### 目录结构

```
app/                              项目应用层（Admin / Web / Api / Console / Exceptions / Providers）
bootstrap/app.php                 Laravel 5.1 应用骨架：绑定 HTTP / Console Kernel 与异常处理器
config/app.php                    注册 ModStart ServiceProvider 等全局 Provider
config/module.php                 系统模块注册表
database/migrations/              ModStart 核心表迁移
module/                           可安装模块（后台按需安装）
vendor/modstart/modstart-laravel5 Laravel 5.1 适配层（composer.json 直接依赖，dev-master）
vendor/modstart/modstart          ModStart 6.0.0 基础库（由适配层引入）
public/asset                      基础库静态资源（vendor:publish 发布）
public/vendor                     模块静态资源（模块安装时发布）
resources/views/theme/            前台默认主题
```

### 升级指南

参照 [https://modstart.com/doc/install/upgrade.html](https://modstart.com/doc/install/upgrade.html)

升级代码后执行：

```bash
php artisan migrate
php artisan modstart:module-install-all
php artisan cache:clear
```

如静态资源有变化，再执行 `make PublishAsset`（该目标会重新发布 `public/asset`、`public/vendor`，并再次执行上述 `migrate` / `module-install-all`）。

## 🔨 开发速看

以下以一个简单的「新闻管理」模块为例，快速了解 ModStart 模块开发的大致流程。

### 模块目录

```
module/News/
├── Admin/
│   ├── Controller/NewsController.php
│   └── routes.php
├── Core/ModuleServiceProvider.php
├── Migrate/
├── config.json
└── README.md
```

### 模块声明 `config.json`

```json
{
  "name": "News",
  "title": "新闻管理",
  "version": "1.0.0",
  "author": "官方",
  "env": ["laravel5"],
  "types": ["PC", "Mobile"],
  "require": ["Vendor:>=3.0.0"],
  "modstartVersion": ">=6.0.0",
  "description": "新闻管理示例模块"
}
```

### 数据表迁移 `Migrate/2026_11_13_000000_news_create.php`

```php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class NewsCreate extends Migration
{
    public function up()
    {
        if (!\ModStart\Core\Dao\ModelManageUtil::hasTable('news')) {
            Schema::create('news', function (Blueprint $table) {
                $table->increments('id');
                $table->timestamps();
                $table->string('title', 200)->nullable()->comment('标题');
                $table->string('cover', 200)->nullable()->comment('封面');
                $table->text('content')->nullable()->comment('内容');
            });
        }
    }

    public function down()
    {
        //
    }
}
```

### 控制器 `Admin/Controller/NewsController.php`

```php
namespace Module\News\Admin\Controller;

use Illuminate\Routing\Controller;
use ModStart\Admin\Concern\HasAdminQuickCRUD;
use ModStart\Admin\Layout\AdminCRUDBuilder;
use ModStart\Grid\GridFilter;
use ModStart\Support\Concern\HasFields;

class NewsController extends Controller
{
    use HasAdminQuickCRUD;

    protected function crud(AdminCRUDBuilder $builder)
    {
        $builder
            ->init('news')
            ->field(function ($builder) {
                /** @var HasFields $builder */
                $builder->id('id', 'ID');
                $builder->text('title', '标题');
                $builder->image('cover', '封面');
                $builder->richHtml('content', '内容');
                $builder->display('created_at', '创建时间');
                $builder->display('updated_at', '更新时间');
            })
            ->gridFilter(function (GridFilter $filter) {
                $filter->eq('id', 'ID');
                $filter->like('title', '标题');
            })
            ->title('新闻管理');
    }
}
```

### 路由 `Admin/routes.php`

```php
/* @var \Illuminate\Routing\Router $router */
$router->match(['get', 'post'], 'news', 'NewsController@index');
$router->match(['get', 'post'], 'news/add', 'NewsController@add');
$router->match(['get', 'post'], 'news/edit', 'NewsController@edit');
$router->match(['post'], 'news/delete', 'NewsController@delete');
$router->match(['get'], 'news/show', 'NewsController@show');
```

### 后台菜单 `Core/ModuleServiceProvider.php`

```php
namespace Module\News\Core;

use Illuminate\Events\Dispatcher;
use Illuminate\Support\ServiceProvider;
use ModStart\Admin\Config\AdminMenu;

class ModuleServiceProvider extends ServiceProvider
{
    public function boot(Dispatcher $events)
    {
        AdminMenu::register(function () {
            return [
                [
                    'title' => '新闻管理',
                    'icon' => 'description',
                    'sort' => 200,
                    'url' => '\Module\News\Admin\Controller\NewsController@index',
                ]
            ];
        });
    }

    public function register()
    {
    }
}
```

### 安装并启用模块

```bash
php artisan modstart:module-install News
```

新安装的模块默认 `enable => false`，在后台「模块管理」里启用即可；如需固定为系统模块，在
`config/module.php` 的 `system` 段注册：

```php
'News' => [
    'enable' => true,
],
```

这样一个简单的新闻增删改查模块就开发完成了。

## 📋 常见问题

- 安装向导提示「系统无需重复安装」：删除 `storage/install.lock`、清空目标数据库中的表，并删除 `.env` 后重试（`prepare` 不接受仍含 `DB_HOST` 的 `.env`）
- 后台菜单 / 页面 500 且刚装过模块：执行 `php artisan cache:clear` 清理模块缓存
- 页面样式或脚本不生效：执行 `make PublishAsset` 重新发布静态资源
- 安装、部署等问题：[https://modstart.com/doc/install/qa.html](https://modstart.com/doc/install/qa.html)

如有其他问题推荐使用官方讨论交流群或在线讨论

- [https://modstart.com/forum](https://modstart.com/forum)

## ⭐️ 贡献代码

本项目的应用层与模块代码在以下仓库维护：

- `GitHub` [https://github.com/open-tecmz/modstart-laravel5](https://github.com/open-tecmz/modstart-laravel5)
- `Gitee` [https://gitee.com/open-tecmz/modstart-laravel5](https://gitee.com/open-tecmz/modstart-laravel5)

## ✉️ 使用交流

> 添加好友请备注 ModStart

<table width="100%">
    <thead>
        <tr>
            <th width="50%">微信交流群</th>
            <th>QQ交流群</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <img style="width:100%;"
                     src="https://open.tecmz.com/code_dynamic/wx" />
            </td>
            <td>
                <img style="width:100%;"
                     src="https://open.tecmz.com/code_dynamic/qq" />
            </td>
        </tr>
    </tbody>
</table>
