---
layout: post
title: "AWS codecommit GRC 사용법"
date: 2022-05-18 10:48:00 +0900
categories: AWS
---

WSL에서 AWS codecommit에서 사용하는 GRC(git-remote-codecommit) 설정 방법을 공유합니다.(UBUNTU 20.04 LTS 기준)
codecommit에 레파지토리를 이미 생성한 것을 가정을 합니다.
그리고, IAM 에서 AWSCodeCommitFullAccess 또는 AWSCodeCommitPowerUser 권한을 가진 사용자를 생성한 것을 가정합니다.

{% highlight ruby %}
sudo apt update

//우분투 20에는 python3 이 이미 설치되어 있어서 pip만 설치했습니다.
sudo apt install python3-pip

sudo apt install awscli

aws configure
// 아래서 사용자 생성할 때 만들어진 키를 입력합니다.(복사하고 마우스 우클릭하면 됩니다.)
AWS Access Key ID [None]: Type your IAM user AWS access key ID here, and then press Enter
AWS Secret Access Key [None]: Type your IAM user AWS secret access key here, and then press Enter
Default region name [None]: Type a supported region for CodeCommit here, and then press Enter // 리전은 서울이면 ap-northeast-2
Default output format [None]: Type json here, and then press Enter// json 이라고 입력합니다.

pip install git-remote-codecommit

WARNING: The script git-remote-codecommit is installed in '/home/enosh/.local/bin' which is not on PATH.
Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
// 위와 같은 경고가 나오면 PATH 를 추가해줍니다.

PATH=$PATH:/home/enosh/.local/bin

{% endhighlight %}
