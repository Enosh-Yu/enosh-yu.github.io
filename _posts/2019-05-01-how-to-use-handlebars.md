---
layout: post
title:  "Handlebars 사용법"
date:   2019-05-01 06:48:00 +0900
categories: Express, Handlebars, Template
---

nodejs 에서 많이 사용하는 템플릿 중에 handlebars 라는 것이 있습니다. express generator 에 pug와 ejs처럼 옵션으로 들어가 있습니다. (```express --hbs``` 로 프로젝트 생성) 하지만, 국내에서는 많이 사용을 하지 않는 것 같습니다.
mastache 문법을 사용하고 레이아웃을 지원합니다. 

pug는 사용하기는 편한 점이 있지만 html 기본 문법을 사용하지 않아서 디자이너와 협업이 불편하고 기존 html 마크업을 그대로 사용하기가 어렵다는 단점이 있습니다.

ejs는 html 마크업을 그대로 사용할 수 있지만 레이아웃을 지원하지 않아서 약간 불편한 점이 있습니다.

handlebars 는 레이아웃을 사용하고 html 마크업을 사용할 수 있어서 사용법만 약간 익히면 중복 작업을 많이 줄일 수 있습니다.

handlebars 는 백엔드, 프론트엔드 둘 다 사용이 가능한데, 여기에서는 백엔트, 특별히 express 에서 사용하는 방법을 알아보겠습니다.

#설치
(nodejs, npm, express generator 는 설치되어 있는 것을 가정합니다.)
express generator를 사용하여 아래와 같이 생성합니다.
{% highlight ruby %}
express --view=hbs myapp
{% endhighlight %}
레이아웃을 편하게 사용하기 위해서 express-handlebars를 설치합니다.
{% highlight ruby %}
cd myapp
npm i express-handlebars
{% endhighlight %}
