---
layout: post
title:  "extends와 overwrite 지시어를 사용해서 템플릿 확장하기"
date:   2018-06-26 13:48:00 +0900
categories: Blade
---

블레이드를 사용하다보면 ``@extends``를 주로 하나만 사용하지만, 가끔은 여러 개를 사용하고 싶을 때가 있습니다.
이럴 때는 ``@overwrite``라는 지사자를 사용하면 됩니다.

아래 예제를 통해서 확인해 보도록 합니다.

master.blade.php
{% highlight ruby %}
<!doctype html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>제목</title>
</head>
<body>
    @yield('content')
</body>
</html>
{% endhighlight %}

index.blade.php
{% highlight ruby %}
@extends('master')
@section('content')
<div class="content">
    <header>overwrite 예제</header>
    <div class="row">@include('template1')</div>
    <div class="row">@include('template2')</div>
    <div class="row">@include('template3')</div>
</div>
@stop
{% endhighlight %}

panel.blade.php
{% highlight ruby %}
<div class="panel panel-primary">
    <div class="panel-heading">
        @yield('heading')
    </div>
    <div class="panel-body">
        @yield('body')
    </div>
</div>
{% endhighlight %}

template1.blade.php
{% highlight ruby %}
@extends('panel')
@section('heading')
<h4 class="panel-title">template1</h4>
@overwrite

@section('body')
<div class="sub-content">
    template1 content
</div>
@overwrite
{% endhighlight %}

template2.blade.php
{% highlight ruby %}
@extends('panel')
@section('heading')
<h4 class="panel-title">template2</h4>
@overwrite

@section('body')
<div class="sub-content">
    template12 content
</div>
@overwrite
{% endhighlight %}

template3.blade.php
{% highlight ruby %}
@extends('panel')
@section('heading')
<h4 class="panel-title">template3</h4>
@overwrite

@section('body')
<div class="sub-content">
    template2 content
</div>
@overwrite
{% endhighlight %}

만일 위에서 ``@overwrite`` 대신에 ``@stop``을 사용하면 ``@include``한 것이 모두 첫번째로 ``@include``한 template1과 똑같이 나오게 됩니다.
같은 페이지 안에서 똑같은 형태의 위젯이 있는데, 형태는 비슷하고 내용이 조금씩 다른 것이 있다면 아주 유용하게 사용할 수 있을 것 같습니다.

참고사이트 : https://laravel.io/forum/08-26-2015-multiple-subviews-extending-a-master-template-only-works-once