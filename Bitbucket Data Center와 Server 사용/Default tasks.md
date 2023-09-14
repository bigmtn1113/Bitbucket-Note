# Default tasks

<br>

Default tasks을 통해 project 및 repository 관리자는 pull request가 열릴 때 자동으로 생성되는 tasks 목록 구성 가능.  
이러한 tasks를 통해 관리자는 개발자가 pull requests 작업을 수행할 때 따라야 할 일관된 processes 설정 가능.

**No incomplete tasks** merge check는 불완전한 default tasks가 포함된 pull requests가 merge되는 것을 방지하는 데 사용 가능.  
그리고 pull request에서 target branch를 변경하면 pull request의 default task도 update 됨.

Project 또는 repository 설정 page에서 default tasks 정의 가능.  
관리자가 project 수준에서 default tasks를 생성하면 project의 모든 repositories는 repository 설정에서 default tasks를 상속.  
Repository 관리자는 상속된 tasks를 덮어쓰거나 제거 불가.  
관리자는 repository 설정에서 repository와 관련된 추가 tasks 추가 가능.

<br>

## Default task 생성
Projects 또는 repositories에 대한 default tasks를 편집하거나 삭제하려면 project 또는 repository 권한이 있는 관리자여야 함.

> [!NOTE]  
> Project 수준에 default task가 있는 경우, repository 수준과 동일한 task 생성 불가.  
> Source 및 target branches와 description(모든 형식 포함)을 확인하여 중복 감지.

1. **Project** 또는 **Repository settings**에서 **Default tasks** 선택.
2. **Add a default task** 선택.
3. **Default task description** field에 task 세부 정보를 입력.
    > [!NOTE]  
    > Markup, emojis, @mentions는 모두 description에서 지원되며 task가 생성될 때 렌더링 됨.
4. 특정 source 및 target branch를 설정하여 특정 pull requests가 열릴 때에만 적용되도록 default task 구성 가능.  
  모든 pull requests에 default task을 적용하려면, source 및 target branch 모두에 대해 **Any branch**를 선택.
5. **Save** 선택.  
  ![image](https://confluence.atlassian.com/bitbucketserver/files/1167692866/1167692868/1/1662435393713/add.png)

<br>

## Default tasks 조회
Default tasks는 사용자 **Bitbucket** 아래의 pull request overview page에 표시됨.  
Default tasks를 보려면, pull request로 이동하여 해당 **Activity** 확인.
Pull request를 검토할 때, **Open tasks list** button을 선택하여 조회 가능.

![image](https://confluence.atlassian.com/bitbucketserver/files/1167692866/1167692867/1/1662435393589/view.png)

<br>

## Default task 편집 또는 삭제
Projects 또는 repositories에 대한 default tasks를 편집하거나 삭제하려면 project 또는 repository 권한이 있는 관리자여야 함.

1. **Project** or **Repository settings**에서 **Default tasks** 선택.
2. **default task description** link를 선택하거나 특정 task에 대해 •••  > **Edit** 또는 **Delete** 선택.

참고 사항:
- 편집 내용은 새로 열린 pull requests에만 적용 됨.
- Default task을 삭제하면 pull request가 열릴 때 더 이상 default task가 생성되지 않음.  
  이전에 열린 pull requests는 삭제된 task를 유지.

<hr>

## 참고
- **Default tasks** - https://confluence.atlassian.com/bitbucketserver/default-tasks-1167692866.html
