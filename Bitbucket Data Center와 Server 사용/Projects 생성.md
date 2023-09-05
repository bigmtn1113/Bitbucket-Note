# Projects 생성

<br>

Bitbucket Data Center 및 Server의 projects를 사용하면 repositories를 그룹화하고 이에 대한 권한을 집계 방식으로 관리 가능.

> [!IMPORTANT]  
> `Project creator` 권한 필요.

<br>

## 절차
1. Navigation bar에서 **Projects > Create project** 선택.
2. 양식 작성.  
  Project의 식별자로 사용되고 URL에 표시되는 짧은 project key를 사용하는 것을 권장.  
  ![image](https://confluence.atlassian.com/bitbucketserver/files/776639848/1206790931/1/1675730998996/createproject.png)
3. 선택사항: Project의 avator 선택 가능. 이는 **Bitbucket** 전체에 표시되며 project를 식별하는데 용이.
4. 완료되면 **Create project** 선택.

이제 project에 repositories 추가 가능.

<br>

## Repository 설정 변경 제한
기본적으로 repository 설정은 project 설정을 상속하며 repository 관리자가 수정 가능.  
신규 및 기존 projects 모두에 대해 일부 repository 설정(Access keys, HTTP access tokens, Project 권한)에 대한 변경 사항을 제한하거나 제어하도록 선택 가능.

> [!IMPORTANT]  
> `Project admins` 권한 필요.

<hr>

## 참고
- **Projects 생성** - https://confluence.atlassian.com/bitbucketserver/creating-projects-776639848.html
