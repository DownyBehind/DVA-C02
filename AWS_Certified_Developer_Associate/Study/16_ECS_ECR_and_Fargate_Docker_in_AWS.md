# ECS, ECR & Fargate - Docker in AWS

## Amazon ECS - Rolling Updates

When updating from v1 to v2, we can control how many tasks can be started and stopped, and in which order
-> 업데이트가 필요할 때, 기존 버전으로 운영되는 ECS 중에서 최소 사용량만 빼고 나머지 종료 후, 종료된 수 만큼 업데이트 처리함

ECS Rolling Update - Min 50%, Max 100%

Starting Number of tasks : 4

Stop 2 tasks and update 2 tasks from v1 to v2

and Stop another 2 tasks(v1) and update these 2 tasks from v1 to v2

finally all tasks are v2

ECS Rolling Update - Min 100%, Max 150%

Starting Number of tasks : 4

Add 2 v2 Tasks

and Stop 2 tasks(v1) and update these 2 tasks from v1 to v2

and Stop another 2 tasks(v1) and update these 2 tasks from v1 to v2

finally all tasks are v2

## Amazon ECS Task Definitions - Deep Dive

## Amazon ECS Task Definitions - Hands On

## Amazon ECS - Task Placements

## Amazon ECR - Hands On
