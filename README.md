# typecho-links



更新历史

增加CSS样式links 
详细见http://www.ncnynl.com
@author nightcat at 2016-6-5

* version 1.1.0 at 2013-12-08
* 修改支持Typecho 0.9
*
* version 1.0.4 at 2010-06-30
* 修正数据表的前缀问题
* 在Pattern里加上所有的数据表字段
*
* version 1.0.3 at 2010-06-20
* 修改图片链接的支持方式。
* 增加链接分类功能
* 增加自定义字段，以便用户自定义扩展
* 增加多种链接输出方式。
* 增加较详细的帮助文档
* 增加在自定义页面引用标签，方便友情链接页面的引用
*
* version 1.0.2 at 2010-05-16
* 增加SQLite支持
*
* version 1.0.1 at 2009-12-27
* 增加显示链接描述
* 增加首页链接数量限制功能
* 增加图片链接功能

* version 1.0.0 at 2009-12-12
* 实现友情链接的基本功能
* 包括: 添加 删除 修改 排序



功能描述
本版本的友情链接可以支持以下的功能：
1、方便地在侧边栏添加友情链接。
2、支持两种输出方式。一种为函数输出方式，主要用于侧边栏的友情链接，或者模板开发者设计的友情链接模板等。另一种方式为HTML标签式输出，主要方便用户建立自己的友情链接页面。
3、支持文字链接、图片链接、图文混合链接等。内设这三种默认的输出方式，支持自定议设定输出规则。
4、支持链接分类，方便管理。
5、支持增加自定义字段，方便用户做一些个性扩展。

使用帮助
插件的安装：
解压至插件目录后，激活即可。
如果已经安装旧版本的本插件，需要禁用后重新激活。

友情链接插件主要有两种调用方式。
第一种为函数调用法。函数的原型为：
output($pattern=NULL, $links_num=0, $sort=NULL)

其中，$pattern是输出规则。输出规则是Links插件的一种特殊语法。使用输出规则，可以定制出属于自己的链接输出方式。例如：
<li><a href="{url}" title="{title}" target="_blank">{name}</a></li>

这就是一个输出规则的例子。经过插件解析后，{url}将会被替换成链接地址，{title}将会被替换链连描述，{name}将会被替换成链接名称。
Links插件目前支持的输出规则有：
{lid}链接在数据表中存放的ID<br />
{url}将会被替换成链接地址<br />
{sort}链接的分类名称<br />
{title}{description}将会被替换链连描述，两者效果一样<br />
{name}将会被替换成链接名称<br />
{image}将会被替换成链接图片<br />
{user}自定义字段


插件自带三种输出规则：显示文字、显示图片及图文混排。
当$pattern值为NULL或SHOW_TEXT时，则规则为显示文字。
<li><a href="{url}" title="{title}" target="_blank">{name}</a></li>\n

当$pattern值为SHOW_IMG时，则规则为显示图片。
<li><a href="{url}" title="{title}" target="_blank"><img src="{image}" alt="{name}" /></a></li>\n

当$pattern值为SHOW_MIX时，则规则为显示图片和文字
<li><a href="{url}" title="{title}" target="_blank"><img src="{image}" alt="{name}" /><span>{name}</span></a></li>\n


$links_num是用于控制链接输出的条数的。当$links_num为缺省值0时，表示不进行限制，输出满足条件的所有链接。

$sort用于指定输出的链接类别，以实现链接的分类输出。缺省值NULL表示输出所有类别的链接。

第二种输出为HTML标签调用法。可以在文章或页面中加入HTML标签来实现链接的调用。
其调用原型为：
<links $links_num $sort>$pattern</links>

$links_num $sort $pattern的功能及缺省值与第一种一样。不过，为了$links_num和$sort缺省值的识别，建议$sort采用的命名方式为：以字母开头，仅包括字母和数字。

使用向导：在侧边栏添加友情链接

在0.8默认主题上，已经集成了本插件的调用接口。因此，不需要任何的修改即可直接使用。如果主题没有本插件接口，可按照以下方式进行调用。
最简单的调用方式为：
<?php Links_Plugin::output(); ?>

此时，会列出所有的链接。
如果想调用的为图片链接，则调用方式为：
<?php Links_Plugin::output("SHOW_IMG"); ?>

如果是图文的混合链接，则调用方式为：
<?php Links_Plugin::output("SHOW_MIX"); ?>


如果想限制侧边栏的链接数量，比如说为10个，则可调用：
<?php Links_Plugin::output("SHOW_TEXT", 10); ?>

图片链接依此类推。

如果想列出某个类别的链接，则可调用：
<?php Links_Plugin::output("SHOW_TEXT", 0, "testsort"); ?>


使用向导：建立独立的友情链接页面
建立独立的友情页面，可以直接用类似建立侧边栏的方式，在模板设计阶段，就设计好链接模板。也可以在后台的页面创建进行链接引用。

最简单的引用方式为：
<links></links>

如果想调用的为图片链接，则调用方式为：
<links>SHOW_IMG</links>

如果是图文的混合链接，则调用方式为：
<links>SHOW_MIX</links>


如果想限制侧边栏的链接数量，比如说为10个，则可调用：
<links 10>SHOW_TEXT</links>

图片链接依此类推。
如果想列出某个类别的链接，则可调用：
<links 0 testsort></links>

也可以用
<links testsort></links>

不过，后者要求分类必须以字母开头。

最后要注意的是：分类名只能包含字母及数字！
