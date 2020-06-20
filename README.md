# 쿠버네티스에서 Jira 활용한 CI/CD 파이프라인 구축하기
> Jira를 쿠버네티스 클러스터에 올리고, Gitlab, Jenkins를 연동해서 DevOps toolchain을 구성합니다. 

[Developer Works Blog](https://developer.ibm.com/kr/cloud/devops/2020/06/19/jira-cicd-1/)

최근 IT 서비스 관리(ITSM, Information Technology Service Management)와 개발 및 운영 서비스를 통합 관리하는 DevOps 툴체인이 주요 트렌드로 자리잡고 있습니다. 최근 기업들은 Openshift, Kuberenetes와 같은 컨테이너 오케스트레이션 플랫폼으로 애플리케이션의 배포, 확장, 유지보수를 모두 할 수 있도록 환경 구축을 하고 서비스 관리를 위해 JIRA를 적극적으로 활용하고 있습니다. 

## Overview

이 코드 패턴은 컨테이너를 활용한 클라우드 네이티브 패키징 기술을 통해 ITSM 서비스와 DevOps 개발 도구들을 연동해서 활용하는 전체 로드맵을 제공합니다. 

Jira Software는 애자일 방법론을 적용한 프로젝트를 원활하게 진행하기 위한 서비스 관리 프로그램입니다. Jira Software, Gitlab, Jenkins를 연동해서 전체적인 DevOps 툴체인 진행 과정의 큰 그림을 소개합니다. 

## Flow

![](./image/jira_cicd_flow.png)

### Features
1. Gitlab에 소스코드 수정 Commit/Merge 하기 
2. Gitlab Webhook으로 Jenkins 자동빌드 설정하기
3. JIRA Issue에 Gitlab Commit/Merge 정보 업데이트하기
4. JIRA Issue에 Jenkins 빌드 결과 업데이트하기
5. JIRA Webhook으로 Jenkins 자동빌드 설정하기

## Included Components
- Kubernetes Clusters
- IBM Cloud Kubernetes Cluster
- Jira Software
- MySQL
- Gitlab
- Jenkins

## Technologies
- 클라우드
- 컨테이너 오케스트레이션

## Related Blogs
1. [쿠버네티스에 Jira 설치하기](blog/JIRA_CICD_(1).md)
2. [Jira 초기 설정하기](blog/JIRA_CICD_(2).md)
3. [Gitlab, Jenkins Webhook 연동하기](blog/JIRA_CICD_(3).md)
4. [Jira에서 Gitlab, Jenkins CI/CD 운영하기](blog/JIRA_CICD_(4).md)

