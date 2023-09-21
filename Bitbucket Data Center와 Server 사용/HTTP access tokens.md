# HTTP access tokens

<br>

Bitbucket Data Center의 HTTP access tokens는 사용자는 물론 projects 및 repositories에서 작업하는 팀을 위해 생성될 수 있음.  
HTTPS를 통한 Git의 비밀번호 대신 사용하거나 Bitbucket REST API를 사용할 때 인증 용도로 사용.

> [!NOTE]  
> Web UI를 통해 login하는 데 token 사용 불가.  
> 사용자를 대신하여 변경 작업을 수행하는 데 token 사용 불가(ex: 새 tokens 생성 또는 사용자 계정 세부 정보 update).  
> 병합으로 commit이 생성되므로 pull request를 병합하는 데 token 사용 불가(유효한 email 주소가 있는 사용자만 commit 생성 가능).

<br>

## HTTP access tokens 생성
1. **Profile picture > Manage account > HTTP access tokens** 이동.
2. **Create token** 선택.
3. token name, permissions 및 expiry 설정  
  ![image](https://confluence.atlassian.com/bitbucketserver/files/939515499/1095239964/1/1636429838193/CreateHTTPtoken.png)

<br>

## Projects 또는 repositories에 대한 HTTP access tokens 생성
> [!IMPORTANT]  
> Projects 및 repositories에 대한 HTTP access tokens를 생성하려면 Data Center license가 필요.

팀이 특정 사용자가 아닌 project 또는 respository 수준에서 권한을 부여하기 위해 HTTP access tokens 생성 가능.

Bitbucket 8.8부터 project 관리자는 **Restrict changes to repository settings** dropdown을 사용하여 repository 관리자가 repository 수준 tokens를 관리하지 못하도록 제한 가능.
Project 관리자가 변경 사항을 제한하는 경우, repository 관리자가 추가한 기존 access tokens는 자동으로 삭제되지 않음.

1. **Project** 또는 **Repository settings**에서 **HTTP access tokens** 선택.
2. **Create token** 선택.
3. token name, permissions 및 expiry 설정.

### permissions
Token이 수행할 수 있는 작업 제한.  
Tokens는 비밀번호와 같으므로 tokens의 권한은 기본적으로 현재 access 수준으로 설정됨.  
그러나 tokens의 권한을 필요한 수준으로만 제한하는 것을 권장.

Token에 할당할 수 있는 권한 조합:  
> [!NOTE]  
> Repo 권한은 project 권한에서 상속됨.  
> Token의 repository 권한은 project 권한만큼 높아야 함.  
> Token project에 쓰기 권한을 부여하면, `repository read` 권한만 부여 불가(쓰기 수준 이상 필수).  
> Repository tokens 경우, project 수준 권한 부여 불가.

| | Project read | Project write | Project admin |
:---: | :---: | :---: | :---:
**Repository read** | Repositories pull 및 clone | 조합 불가 | 조합 불가
**Repository write** | - Pull request 수행<br><br> - Repositories push, pull 및 clone(merge 제외) | - Pull request 수행<br><br> - Repositories push, pull 및 clone(merge 제외) | 조합 불가
**Repository admin** | - Pull request 수행<br><br> - Repositories push, pull 및 clone(merge 제외)<br><br> - Repository 설정 및 권한 update | - Pull request 수행<br><br> - Repositories push, pull 및 clone(merge 제외)<br><br> - Repository 설정 및 권한 update | - Pull request 수행<br><br> - Repositories push, pull 및 clone(merge 제외)<br><br> - Repository 설정 및 권한 update<br><br> - Project 설정 및 권한 update<br><br> - Repositories 생성

**HTTP access tokens page** 내에서 tokens의 권한을 수정하거나 token 취소 가능.

<br>

### Expiry
보안을 강화하기 위해 token을 생성할 때 자동으로 만료되도록 설정가능.  
이는 선택 사항이지만, 관리자가 이를 요구사항으로 설정했다면 관리자가 설정한 한도 내에서 만료 날짜를 선택하는 것은 필수.  
Token이 생성되면 만료 날짜는 변경 불가.  
**HTTP access tokens** page 목록에서 모든 tokens의 만료 날짜 확인 가능.

<br>

## HTTP access tokens 사용
> [!NOTE]  
> Integration당 하나의 token mapping.
> 
> HTTP access tokens는 scripts를 사용하고 외부 applications를 Bitbucket과 통합하는 안전한 방법.  
> Integration당 하나의 token만 mapping하는 것을 권장.  
> 이렇게 하면 system이 손상된 경우, 간단히 token을 취소 가능하며 다른 integrations에는 영향을 주지 않음.

Git 작업(ex: `git clone`)의 경우 사용자의 access token을 비밀번호 대신 사용 가능:
```
> git clone https://bitbucketserver.com/scm/projectname/teamsinspace.git
Cloning into 'teamsinspace'...
Username for 'https://bitbucketserver.com':username
Password for 'https://username@bitbucketserver.com':MDM0MjM5NDc2MDxxxxxxxxxxxxxxxxxxxxx
```

Basic Auth 사용:
```
git clone https://username:MDM0MjM5NDc2MDxxxxxxxxxxxxxxxxxxxxx@bitbucketserver.com/scm/projectname/teamsinspace.git
```

REST 작업의 경우에 Basic Auth 사용:
```
curl -u username:MDM0MjM5NDc2MDxxxxxxxxxxxxxxxxxxxxx https://bitbucketserver.com/rest/api/latest/resource/path
```

Project 또는 repository tokens의 경우 username 없이 Bearer Auth만 사용하는 것을 권장:
```
curl -H 'Authorization: Bearer MDM0MjM5NDc2MDxxxxxxxxxxxxxxxxxxxxx' https://bitbucketserver.com/rest/api/latest/resource/path
```

HTTP Git 작업에 대한 Bearer Auth:
```
git clone -c http.extraHeader='Authorization: Bearer MDM0MjM5NDc2MDxxxxxxxxxxxxxxxxxxxxx' https://bitbucketserver.com/scm/projectname/teamsinspace.git
```

<hr>

## 참고
- **HTTP access tokens** - https://confluence.atlassian.com/bitbucketserver0813/http-access-tokens-1283689908.html
