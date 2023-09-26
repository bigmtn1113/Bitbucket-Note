# Repository archive download

<br>

Bitbucket Data Center 및 Server를 사용하면 특정 시점의 source files archive download 가능.  
Source view, Commits list 및 Branches list의 actions dropdown menu에서 source를 .zip file로 download 가능.  
개별 branches, commits 및 tags의 archive를 download 가능.

단일 file을 download하려면 repository의 file로 이동하여 **Raw file**을 선택하고 browser에 열리는 file을 저장.

<br>

## Repository *downloading*과 *clining*의 차이점
Repository를 **cloning**하면 원격 repository의 source files와 repository의 Git history(branches, commits, tags 등)가 local system에 복사됨.  
또한 cloning은 복제된 repository를 다시 가리키는 원격 연결(일반적으로 origin이라고 지칭)을 생성.  
적절하게 초기화된 Git repository인 local directory에만 복제 가능(`git init` 사용).

Repository archive를 **downloading**하면 복사하도록 선택한 항목에 따라 특정 시점의 repository source files만 복사됨.  
Archive download의 가장 큰 차이점은 repository history를 복사하지 않거나 원격 repository에 대한 연결을 생성하지 않는다는 것.  
Source files만 가져오고 `.git` directory에 저장된 Git metadata는 가져오지 않음.

<br>

## Source를 .zip file로 download
**Branch의 repository archive를 download하려면:**
1. Repository의 Source view, Commit view 또는 Branches list로 이동.
2. Branch selector를 사용하여 branch 선택.
3. Branch selector 옆에 있는 actions dropdown을 클릭한 다음, **Download** 선택.  
  ![image](https://confluence.atlassian.com/bitbucketserver0813/files/1283690284/1283690290/1/1614033861206/image2017-6-5+18%3A37%3A49.png)

또한 Branches 목록에서 볼 수 있듯이, 모든 branch의 actions menu에서 특정 branch의 repository archive download 가능.  
![image](https://confluence.atlassian.com/bitbucketserver0813/files/1283690284/1283690288/1/1614033861045/image2017-6-5+18%3A38%3A23.png)

**Commit에서 repository archive를 download하려면:**
1. 단일 commit을 보려면 commit의 hash 번호 선택.
2. 오른쪽 상단 panel에서 **Download this commit** 선택.  
  ![image](https://confluence.atlassian.com/bitbucketserver0813/files/1283690284/1283690287/1/1614033860967/image2017-6-5+18%3A38%3A53.png)

**Tag에서 repository archive를 download하려면:**
1. Repository의 Source view, Commit view 또는 Branches list로 이동.
2. Branch selector를 사용하여 tag 선택.  
  ![image](https://confluence.atlassian.com/bitbucketserver0813/files/1283690284/1283690285/1/1614033860675/image2017-6-5+18%3A43%3A38.png)
3. Branch selector 옆에 있는 actions dropdown을 클릭한 다음, **Download** 선택.  
  ![image](https://confluence.atlassian.com/bitbucketserver0813/files/1283690284/1283690286/1/1614033860888/image2017-6-5+18%3A42%3A28.png)

<br>

## Source를 .tar 또는 .tar.gz file로 download
Bitbucket의 UI에서 source file을 download하면 file이 .zip 형식으로 download됨.  
그러나 URL을 편집하고 .tar, .gz 또는 .tar.gz와 같은 다른 형식으로 archive 가져오기 가능.

**.zip 이외의 file 형식으로 source를 download하려면:**
1. Repository의 Source view, Commit view 또는 Branches list로 이동.
2. Branch selector를 사용하여 branch 선택.
3. Branch selector 옆에 있는 actions dropdown을 클릭한 다음, **Download** link를 마우스 오른쪽 button으로 선택하고 URL 주소를 복사.
4. Browser에 URL을 붙여넣으면 다음과 같이 표시됨.  
    ```
	.../projects/TIS/repos/website/archive?format=zip
	```
5. `format=zip`을 원하는 형식으로 변경.  
  **.tar.gz files**의 경우 인수를 `format=tgz`로 변경.  
  **.tar files**의 경우 인수를 `format=tar`로 변경.
6. **Enter**를 누르면 browser에서 file이 download됨.

<hr>

## 참고
- **Repository archive download** - https://confluence.atlassian.com/bitbucketserver0813/download-a-repository-archive-1283690284.html
