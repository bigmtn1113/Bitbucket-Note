# Repository clone

<br>

Terminal에서 Sourcetree, Git을 사용하거나 원하는 client를 사용하여 Git repository clone 가능.

<br>

## 절차
1. Repository의 sidebar에서 **Clone**를 선택하여 Clone dialog를 표시.
2. Clone URL(SSH 또는 HTTPS) 복사.  
  SSH protocol을 사용하는 경우 public key가 올바르게 구성되었는지 확인.
3. Terminal 창에서 repository를 clone하려는 local directory로 변경.
4. git clone을 입력하고 복사한 clone URL을 입력.  
    HTTPS를 통한 clone
    ```
    $ git clone https://username@bitbucket.org/teamsinspace/documentation-tests.git
    ```
    SSH를 통한 clone  
    ```
    $ git clone git@bitbucket.org:teamsinspace/documentation-tests.git
    ```

Clone이 성공하면 local drive에 새 하위 directory가 나타나는데, 이 directory는 clone한 Bitbucket repository와 이름이 동일.  
여기에는 Git이 source files에 대한 변경 사항을 유지하는데 필요한 files와 metadata가 포함.

<br>

## Mirror repository clone
1. Bitbucket Data Center 및 Server의 repository로 이동.
2. Repository의 sidebar에서 **Clone**를 선택하여 Clone dialog를 표시.
3. Mirros가 구성되었다면 **Clone from** dropdown을 사용하여 가장 가까운 mirror를 선택하면 clone URL이 변경됨.
4. Clone URL(SSH 또는 HTTPS)을 복사.  
  SSH protocol을 사용하는 경우 public key가 올바르게 구성되었는지 확인.
5. Terminal 창에서 repository를 clone하려는 local directory로 변경.
6. git clone을 입력하고 복사한 clone URL을 입력.  
  SSH를 통한 clone
    ```
    $ git clone git@bitbucket-au.example.com:7999/upstream/PROJ/repo.git
    ```
    > [!NOTE]  
    > HTTP 또는 HTTPS 사용 불가.

Clone이 성공하면 local drive에 새 하위 directory가 나타나는데, 이 directory는 clone한 Bitbucket repository와 이름이 동일.  
여기에는 Git이 source files에 대한 변경 사항을 유지하는데 필요한 files와 metadata가 포함.

<hr>

## 참고
- **Repository clone** - https://confluence.atlassian.com/bitbucketserver/clone-a-repository-790632786.html
