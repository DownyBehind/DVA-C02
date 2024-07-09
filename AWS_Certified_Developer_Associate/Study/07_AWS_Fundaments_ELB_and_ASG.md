# AWS ELB and ASG

## Auto Scaling Groups - Instance Refresh

Goal : Update launch template and then re-creating all EC2 instances.

we can use the native feature of instance Refresh.

you can set minimum healthy percentage like 60%
-> 얼마나 instance를 끄고 재시작할 수 있는지 ASG에게 알려준다.

and then Instance Refresh could change the old one to the new one.
