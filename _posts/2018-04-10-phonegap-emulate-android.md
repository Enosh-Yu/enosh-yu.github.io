---
layout: post
title:  "폰갭에서 안드로이드 에뮬레이터 실행하기"
date:   2018-04-10 12:48:00 +0900
categories: developer, phonegap, android
---

폰갭 cli 명령중에서 ```phonegap emulate``` 라는 것이 있는데, 이것이 작동을 하지 않는 경우가 있는데요.
그럴 경우에는 아래와 같이 하면 실행이 됩니다. (그전에 안드로이드 sdk는 설치되어 있어야 하고, 적어도 한개의 AVD는 있어야 합니다.)

{% highlight ruby %}
my_phonegap_projectfolder/platform/android/cordova/run --emulator
{% endhighlight %}