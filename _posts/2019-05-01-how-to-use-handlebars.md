---
layout: post
title:  "Handlebars 사용법"
date:   2019-05-01 06:48:00 +0900
categories: Express, Handlebars, Template
---

nodejs 에서 많이 사용하는 템플릿 중에 handlebars 라는 것이 있습니다. express generator 에 pug와 ejs처럼 옵션으로 들어가 있습니다. (```express --hbs``` 로 프로젝트 생성) 하지만, 국내에서는 많이 사용을 하지 않는 것 같습니다.
mustache 문법을 사용하고 레이아웃을 지원합니다. 

pug는 사용하기는 편한 점이 있지만 html 기본 문법을 사용하지 않아서 디자이너와 협업이 불편하고 기존 html 마크업을 그대로 사용하기가 어렵다는 단점이 있습니다.

ejs는 html 마크업을 그대로 사용할 수 있지만 레이아웃을 지원하지 않아서 약간 불편한 점이 있습니다.

handlebars 는 레이아웃을 사용하고 html 마크업을 사용할 수 있어서 사용법만 약간 익히면 중복 작업을 많이 줄일 수 있습니다.

handlebars 는 백엔드, 프론트엔드 둘 다 사용이 가능한데, 여기에서는 백엔트, 특별히 express 에서 사용하는 방법을 알아보겠습니다.

설치
===
>(nodejs, npm, express generator 는 설치되어 있는 것을 가정합니다.)

express generator를 사용하여 아래와 같이 생성합니다.
{% highlight ruby %}
express --view=hbs myapp
{% endhighlight %}
또는
{% highlight ruby %}
express --hbs myapp
{% endhighlight %}
views 디렉토리에 error.hbs, index.hbs, layout.hbs 파일이 자동으로 생성이 됩니다.
디폴트 layout을 변경하려면 아래와 같이 추가합니다.
{% highlight ruby %}
#app.js
app.set('view options', { layout: 'layouts/main' });
{% endhighlight %}

handlebars는 기본 layout 기능만 제공합니다.
다른 템플릿엔진처럼 확장해서 사용하려면 helper를 등록해서 사용하면 됩니다.
hbs github 에 예제가 나와 있어서 그대로 사용합니다.

{% highlight ruby %}
#app.js
var hbs  = require('hbs');
var blocks = {};

hbs.registerHelper('extend', function(name, context) {
    var block = blocks[name];
    if (!block) {
        block = blocks[name] = [];
    }

    block.push(context.fn(this)); // for older versions of handlebars, use block.push(context(this));
});

hbs.registerHelper('block', function(name) {
    var val = (blocks[name] || []).join('\n');

    // clear the block
    blocks[name] = [];
    return val;
});
{% endhighlight %}

layout 파일에 아래와 같이 정의합니다.

```
<!doctype html>
<html>
<head>
  <title>{ {title} }</title>

  <link rel='stylesheet' href='/css/style.css'>

  { { {block "stylesheets"} } }
</head>
<body>
  body: { { {body} } }

  <hr/>
  post body
  <hr/>
  { { {block "scripts"} } }
</body>
</html>
```

layout 적용된 view 파일에는 아래와 같이 사용합니다.

```
{ {#extend "stylesheets"} }
<link rel="stylesheet" href="/css/index.css"/>
{ {/extend} }

let the magic begin

{ {#extend "scripts"} }
<script>
  document.write('foo bar!');
</script>
{ {/extend} }
```
(중괄호가 한 칸씩 띄어쓰는 걸로 되어 있는데, 붙여써야 합니다. 마크다운에서 붙여쓰니까 특수문자로 인식이 되어 나오지게 않네요-,-;;)