# Repository archive

<br>

Repository를 삭제하는 것 대신 보관 가능.  
이는 repositories 목록을 정리하고 보다 정확한 code 검색 결과를 보장하는 데 용이.

> [!IMPORTANT]  
> Data Center license 필요.

> [!NOTE]  
> Repository를 archive하면 읽기 전용이 되며 searches 및 comparison에서 제외됨.  
> 이는 또한 다음을 수행할 수 없음을 의미.
> - Pull requests 생성  
> - Branches 생성  
> - Comments 추가  
> - Repository details 변경  
> - Repository 이동  

<br>

## 참고사항
- Archive된 repository는 계속 fork 및 clone 가능.
- Open pull requests가 있는 repository는 archive 불가.
- Repository 관리자는 archive된 repositories에 대해 archive 취소 가능.
- Repository를 archive해도 disk 공간이 줄어들진 않음.
- Archive된 repositories에서 code 검색 가능.
- Archive처리한 repositories는 계속해서 조회 가능.  
  
  ![image](https://confluence.atlassian.com/bitbucketserver0813/files/1283689897/1283689903/1/1670143433183/repo_list.png)

<br>

## Repository 설정에서 단일 repository archive 또는 unarchive
> [!IMPORTANT]  
> `Repository admins` 권한 필요.  
> Bitbucket Data Center 8.0 이상에서 사용 가능.

1. **Repository settings** > **Repository details**로 이동.
2. **Manage repository** > **Archive** 선택.  
  Unarchive하려면 **Manage repository** > **Unarchive** 선택.
3. 확인 modal에서 **Archive** 선택.

![image](https://confluence.atlassian.com/bitbucketserver0813/files/1283689897/1283689901/1/1670143448812/repo.png)

<br>

## Administration area에서 repositories를 대량으로 archive하거나 unarchive
> [!IMPORTANT]  
> `System 및 global admins` 권한 필요.  
> Bitbucket Data Center 8.0 이상에서 사용 가능.

단일 repository 또는 여러 repositories를 한 번에 archive 가능.

1. **Administration** > **Git** > **Repositories**로 이동.
2. Archive하려는 repositories 옆에 있는 checkboxes 선택.  
  Unarchive하려면 unarchive하려는 repository 옆에 있는 **More actions ●●●** > **Unarchive** 선택.
3. **Archive** 선택.
4. 확인 modal에서 **Archive** 선택.

![image](https://confluence.atlassian.com/bitbucketserver0813/files/1283689897/1283689902/1/1670143441513/global.png)

<hr>

## 참고
- **Repository archive** - https://confluence.atlassian.com/bitbucketserver0813/archive-a-repository-1283689897.html
