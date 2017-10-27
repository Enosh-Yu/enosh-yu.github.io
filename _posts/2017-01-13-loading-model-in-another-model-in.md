---
layout: post
title:  "[Codeigniter] model에서 다른 model 불러오기"
date:   2017-01-13 13:43:00 +0900
categories: Codeigniter
---
코드이그나이터를 사용하다보면 아주 가끔(?) 모델에서 다른 모델에 있는 함수를 호출하고 싶을 때가 있습니다.
이럴 경우에 어떻게 사용하는지 알아보기로 합니다. 코드이그나이터 2.2.X 를 기준으로 했습니다.

먼저 호출하려고 하는 모델입니다.

{% highlight ruby %}
class M1_model extends CI_Model
{
  function __contruct()
  {
    parent::__contruct();
  }

  function f1()
  {
    echo 'f1() called';
  }
}
{% endhighlight %}

M2_model에서 M1_model을 사용하고 싶을 때 아래와 같이 사용합니다.

{% highlight ruby %}
class M2_model extends CI_Model
{
  var $ci = null;
  function __contruct()
  {
    parent::__contruct();
    $this->ci =& get_instance();
    $this->ci->load->model('M1_model');
  }

  function f2()
  {
    echo 'f2() called';
    $this->ci->M1_model->f1();
  }
}
{% endhighlight %}

아래 링크를 참고했습니다. 아래 처럼했는데, 2.2.x에서는 안 되는 것 같아서 위와 같이 하니까 되더군요.

[참고](http://codeignitertricks.blogspot.kr/2009/10/loading-model-in-another-model-in.html)