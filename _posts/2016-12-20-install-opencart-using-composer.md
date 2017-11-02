---
layout: post
title:  "컴포저를 이용한 opencart 설치"
date:   2016-12-20 15:48:00 +0900
categories: opencart
---

opencart2.0 부터 컴포저를 지원하기 시작했습니다. ftp를 이용해 업로드 할 수도 있지만, 컴포저를 이용해서 설치하는 방법을 알아보기로 합니다.
웹서버는 아파치를 기준으로 합니다. composer가 이미 설치되어 있는 것을 가정하고 시작합니다.

DOCUMENT_ROOT 가 /var/www/html/ 일 때

{% highlight ruby %}
composer create-project opencart/opencart /var/www

cd /var/www

mv html html_old

mv upload html

cd html

mv config-dist.php config.php

mv ./admin/config-dist.php ./admin/config.php
{% endhighlight %}

사이트 접속 후 설치화면을 따라 하시면 됩니다. 설치후에는 install 디렉토리를 삭제합니다.