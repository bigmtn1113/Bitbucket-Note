# Git LFS files 작업

<br>

Git LFS(Large File Storage)는 대용량 files 처리 방법을 개선하는 Git extension.  
Repository 대신 원격 server에 저장되는 작은 text pointers로 대체하여 Bitbucket Data Center 및 Server에서 cloning 및 fetching과 같은 작업 속도를 높임.

Git LFS를 사용하면 LFS files을 잠가서 다른 사람이 편집하지 못하도록 할 수도 있음.  
이는 images, videos 또는 3D models과 같이 병합할 수 없는 대규모 binary 자산으로 작업하는 경우 유용할 수 있음.

![image](https://confluence.atlassian.com/bitbucketserver0813/files/1283690293/1283690294/1/1612236950884/GitLFSLock.png)

*files가 잠기면 files 옆에 icon이 표시됨.*  
*files 위로 mouse를 가져가면 누가 files을 잠갔는지, 언제 잠갔는지 확인 가능.*

> [NOTE]  
> 기본적으로 Git LFS는 각 repository에서 비활성화되어 있으며 repository 관리자만 활성화 가능.

<br>

## Git LFS client 설치
Git LFS를 사용하려면 먼저 local machine에 client 설치 필요.

**Git LFS client를 설치하려면:**
1. 다음을 실행하여 Git 1.8.2 이상이 있는지 확인:
    ```
    git --version
    ```
2. Git LFS 설치 program을 download하고 실행.  
  Linux 또는 Mac OS X를 사용하는 경우 package 관리자를 사용하여 `git-lfs` 설치.
3. Terminal이나 명령 prompt에서 다음 명령을 실행:
    ```
    git lfs install
    ```

LFS filters는 home directory의 `.gitconfig` file에 추가되며 모든 repository에서 사용 가능.  
이 작업은 한 번만 수행하면 됨.

<br>

## Git LFS files를 추적하고 잠글 수 있도록 설정
Git LFS client를 설치한 후에는 `track` 명령을 사용하여 처리할 folder 경로나 file type 등록 필요.  
이러한 files를 'lock'하려면 `--lockable` flag를 포함해야 함.  
또한, 이 작업은 각 repository마다 수행해야 함.

**folder 경로 또는 file type을 추적하려면:**
1. Repository directory로 이동.
2. 다음 명령을 실행.  
    > [NOTE]  
    > 필요하지 않은 경우 `--lockable` flag 제거 가능.
  
    ```
    git lfs track '<pattern>' --lockable
    ```
  
    `<pattern>`에 들어갈 내용:
    - Folder 경로(ex: `'path/to/some/folders/*'`).
    - File 이름 또는 file types(ex: `bckgrnd.bin`, `'*.psd'` 또는 `'*.*'`).
    - > [NOTE]  
      > Wildcards를 사용할 때 shell이 wildcards를 확장하지 못하도록 따옴표 포함 필수.

    그러면 pattern이 repository의 `.gitattributes` file에 추가됨.

3. `.gitattributes`에 대한 변경 사항을 commit하고 push:
  ```
  git add .gitattributes
  git commit -m "add Git LFS to the repo"
  git push origin master
  ```

  추적 중인 files를 변경할 때마다 변경 사항을 push해야 해당 repository를 clones하는 모든 사람이 추적 patterns를 갖게 됨.

  이제 pattern과 일치하는 file 이름을 추가하면 LFS에서 자동으로 처리됨.  
  이런 식으로 여러 patterns를 추가할 수 있으며, `git lfs` 명령을 사용하여 추적되는 patterns를 볼 수 있음.

<br>

## Git LFS files 잠금 및 잠금 해제
Git LFS file이 `locakble`으로 등록되면, 작업하는 동안 다른 사람이 편집하지 못하도록 'lock' 가능.  
이는 병합할 수 없는 대규모 binary 자산으로 작업하는 경우 도움이 될 수 있음.

File 잠금은 몇 가지 규칙을 따름:
- 각 file은 한 번에 한 사람만 lock 가능.
- 잠긴 files는 해당 files을 잠근 사람만 잠금을 해제 가능(files를 강제로 잠금 해제하는 방법은 아래 참조).
- `push`에 본인이 잠그지 않은 잠긴 files가 포함되어 있으면 거부됨.
- `merge`에 잠그지 않은 잠긴 files가 포함되어 있으면 해당 files가 차단됨.

**Git LFS file을 잠그려면 다음을 수행:**  
Repository directory로 이동하고 다음 명령을 실행:
```
git lfs lock <filename>
```

**Lock** button을 클릭하여 source 보기에서 직접 Git LFS file을 잠글 수도 있음.  
그러면 file 이름 옆에 자물쇠 icon이 표시됨.

**잠긴 Git LFS file을 잠금 해제하려면 다음을 수행:**  
Repository directory로 변경하고 다음 명령을 실행:
```
git lfs unlock <filename>
```

**Unlock** button을 선택하여 source 보기에서 직접 Git LFS files의 잠금을 해제할 수도 있음.  
그러면 file 옆에 표시된 자물쇠 icon이 제거되어 잠금 해제된 file을 나타냄.

<br>

## 다른 사람이 잠근 files 잠금 해제
Bitbucket의 잠긴 files는 해당 file을 잠근 사람만 잠금을 해제할 수 있으므로 도움을 요청할 수 있도록 file을 잠근 사람이 누구인지 알아내야 할 수도 있음.

다른 사람이 잠근 file을 잠그거나 잠금 해제하거나 push하거나 merge하려고 하면 해당 file을 잠근 사람에게 연락할 수 있도록 해당 file을 잠근 사람의 username과 email 주소가 오류 message에 포함됨.  
다음 명령을 실행하여 repository에 있는 모든 잠긴 files를 볼 수도 있음:  
**잠긴 files를 모두 보려면:**  
Repository directory로 이동하고 다음 명령을 실행:
```
git lfs locks
```

File 잠금 해제를 요청할 수 없는 경우도 있을 수 있음.  
예를 들어, file를 잠근 사람이 조직을 떠났을 수 있음.  
이와 같은 상황에 처한 경우 force flag를 사용하여 file 잠금을 해제할 수 있음.

**File을 강제로 잠금 해제하려면:**  
Repository directory로 이동하고 다음 명령을 실행:
```
git lfs unlock <filename> --force
```

<hr>

## 참고
- **Git LFS files 작업** - https://confluence.atlassian.com/bitbucketserver0813/working-with-git-lfs-files-1283690293.html
