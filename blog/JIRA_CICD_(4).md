# Kubernetes(IKS)에서 Jira 활용한 CI/CD 파이프라인 구축하기(4/4)

## Part 4. Jira에서 Gitlab, Jenkins CI/CD 운영하기
> Jira Issue에 소스 커밋, 빌드 정보를 업데이트 하고, 워크플로우에서 Jenkins 자동빌드를 실행할 수 있도록 설정합니다.

## 사전 준비 사항
- [Gitlab(VM) 설치](https://velog.io/@hamon/Ubuntu18.04에-Gitlab-설치하기)
- [Jenkins(VM) 설치](https://velog.io/@hamon/Ubuntu18.04에-Jenkins-설치하기)
- JIRA(IKS) 설치
- [Jira 프로젝트 생성 및 이슈 등록](https://velog.io/@hamon/2-Jira-프로젝트-커스터마이징-하기)

## Features
1. Jira Issue에 Gitlab Commit 정보 업데이트하기
2. Jira Issue에 Jenkins 빌드 결과 업데이트하기
3. Jira Workflow에서 Jenkins 자동빌드 실행하기

## Steps
1. Jira와 Gitlab 연동하기 
2. JJira에서 Jenkins 빌드 확인하기  
3. Jira Workflow에서 Jenkins 자동빌드 설정

### 1. Jira와 Gitlab 연동하기
Gitlab Project에서 `Settings > Integration` 에서 `Jira` 를 선택합니다. 
쿠버네티스에 설치한 Jira의 URL 정보와 Jira에서 Gitlab 정보를 업데이트할 때 사용할 사용자의 Username과 Password를 입력합니다. 

연동을 확인하기 위해서 Gitlab에서 Readme파일을 수정하고, Commit 메세지에 JIRA ISSUE 번호를 입력합니다.(필수) 
예시 : `[JIR-2] Update README.md`
작성한 커밋 메세지를 Push 하면 Jira Issue에서 Gitlab 변동 사항을 다음과 같이 업데이트 받을 수 있습니다. 
![](../image/jira_gitlab_commit.png)

### 2. Jira에서 Jenkins 빌드 확인하기 
Jenkins에서 `Jira Pipeline Steps` 플러그인을 설치합니다. 
`Jenkins 관리 > 시스템 설정 > Jira Steps`에서 Jira Site 정보를 입력합니다. 
![](image/jira_site.png)

Jenkins 파이프라인 설정란에서 `Pipeline script from SCM`을 선택하고, Git 정보를 입력합니다. 
Jenkins에 Gitlab id/password Credentials를 등록해두고, 선택합니다. 디폴트로 프로젝트의 가장 상위 폴더 아래 `Jenkinsfile`에서 스크립트 파일을 읽어옵니다. 

Gitlab 프로젝트에서 Jenkinsfile을 생성하고, Jira Issue에 빌드 결과를 업데이트 하기 위한 스크립트를 작성합니다. 
참고로 Jenkins [Jira Pipeline Steps 문서](https://www.jenkins.io/doc/pipeline/steps/jira-steps/)에 스크립트 작성 사례 및 방법이 상세하게 나와있습니다.

#### Jenkinsfile
```
def JIRA_ID = "JIR-3"

pipeline {
    agent any
    stages {
        stage ('Build') {
            steps {
                sh 'yarn install'
            }
        }
        stage ('Jira Steps') {
            steps {
                script {
                    def comment = [ body: 'Build Complete']
                    jiraAddComment site: "jira", idOrKey: "${JIRA_ID}", input: comment
                }
            }
        }
    }
}
```
Jenkins 파일을 업데이트하면 앞서 Gitlab Push와 Jenkins pipeline build 연동해두었기 때문에 자동 빌드가 시작됩니다. 

다음 화면처럼 Jenkins에서 빌드가 성공하면, 이제 Jira에서도 빌드 성공 여부를 확인할 수 있습니다. 
![](../image/jenkinsfile.png)
![](../image/jira_comment.png)

### 3. Jira Workflow에서 Jenkins 자동빌드 실행하기


## Reference
- Jenkins, (June 12, 2020), https://www.jenkins.io/doc/pipeline/steps/jira-steps/

