---
layout: post
title: "ecs-cli 예제"
date: 2024-01-10 08:38:00 +0900
categories: AWS
---

ecs 에서 자주 사용하는 커맨드라인 명령어 예제 모음

{% highlight ruby %}

ecs-cli configure profile \
    --access-key access-key \
    --secret-key secret-key \
    --profile-name ecs-profile
	
ecs-cli configure \
    --cluster nginx-cluster \
    --default-launch-type EC2 \
    --config-name nginx-cluster-config \
    --region ap-northeast-2
	
ecs-cli up \
    --capability-iam \
	--vpc vpc-080baea4c8eec132c \
	--subnets subnet-029e26888336e4c4e,subnet-0b7d27a4f990408ca \
	--security-group sg-04600e4f02571bdfe \
    --size 1 \
    --instance-type t2.micro \
    --cluster-config nginx-cluster-config \
    --ecs-profile ecs-profile
	
ecs-cli compose up \
    --create-log-groups \
    --cluster-config nginx-cluster-config \
    --ecs-profile ecs-profile
	
ecs-cli compose service up \
    --cluster-config nginx-cluster-config \
    --ecs-profile ecs-profile
	
	
ecs-cli ps \
    --cluster-config nginx-cluster-config \
    --ecs-profile ecs-profile
	
ecs-cli compose down \
    --cluster-config nginx-cluster-config \
    --ecs-profile ecs-profile
	
ecs-cli down \
    --force \
    --cluster-config nginx-cluster-config \
    --ecs-profile ecs-profile
	
ecs-cli compose service rm \
    --cluster-config hello-cluster-config \
    --ecs-profile ecs-profile
	
{% endhighlight %}
