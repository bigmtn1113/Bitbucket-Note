# Webhooks 관리

<br>

Webhooks는 특정 event가 발생할 때마다 server 또는 다른 외부 service에 요청하도록 Bitbucket Data Center 및 Server를 구성하는 방법을 제공. webhook은 다음으로 구성됨.
- 하나 이상의 events – 기본 event는 repository push지만, 여러 events를 선택하여 webhook trigger 가능.
- URL – 일치하는 event가 발생할 때 Bitbucket이 event payloads를 보내도록 하려는 endpoint. Project 또는 repository key와 같은 추가 event context를 URL 변수로 추가하고 단일 webhook을 사용하여 여러 URLs로 data 전송 가능.

Webhook에는 Webhooks 생성과 webhook trigger 두 단계가 존재:  
Event에 대한 webhook를 생성하면, 해당 event가 발생할 때마다 Bitbucket은 event를 describes하는 payload 요청을 지정된 URL로 전송.

Project와 repository 수준 모두에서 webhooks 생성 가능.  
Project 수준에서 생성된 webhooks는 해당 project의 모든 repositories에 상속됨.

<br>

## Webhooks을 사용해야 하는 경우
- User가 repository에 commits를 push할 때마다, CI server에 build를 시작하도록 알리고 싶을 경우.
- User가 commits를 push하거나 pull request를 생성할 때마다, application에 알림을 표시하고 싶을 경우.
- User가 repository에 commits를 push하고 mirror가 해당 변경 사항을 동기화할 때마다, CI system에 build를 시작하도록 알리고 싶을 경우.

<br>

## Webhooks의 장점
Webhooks가 없이 Bitbucket에서 event가 발생하는 시기를 감지하려면 API polling 필요.  
그러나 API polling은 불편하고 비효율적이며 오류가 발생하기 쉬움.

Webhooks는 API가 매분 동일한 활동을 확인할 필요가 없음을 의미.

<br>

## Webhook 보안
Secret token을 사용하거나 basic authentication을 사용하여 webhook 보호 가능.

**Secret token**: Secret tokens를 사용하여 payload를 인증하고 Bitbucket과 endpoint간에 contents가 변조되지 않도록 보장.  
HTTPS와 결합하면, 전송된 message가 Bitbucket이 보내려고 했던 message인지 확인하는 데 유용.

webhook에 대한 secret을 정의하면, 각 요청은 HMAC(Hash 기반 message 인증 code)를 통해 서명됨.  
이 algorithm의 기본값은 HMACSha256. X-Hub-Signature header가 정의되어 있으며 HMAC를 포함.  
예를 들어 POST request의 header는 다음과 같이 encoding된 일반 text.
```
x-hub-signature: sha256=c3383246d4fd871e66e962b50cc12222222222222222222222222222222222
```

Message payload의 유효성을 인증하기 위해, 수신자는 secret을 HMAC algorithm의 key로 사용하여 수신된 본문에 대해 HMAC algorithm 수행 가능.  
결과가 일치하지 않으면, 전송에 문제가 있어 message payload가 변경되었음을 확인 가능.

**Basic authentication**: Endpoint가 basic authentication(username 및 password)을 사용하는 경우, 이 방법을 사용하여 webhook을 보호.  
Webhook data가 전송되면, 인증 header가 HTTP 요청에 포함됨. 인증 header에 대한 인증 자격 증명은 base64로 encoding됨.

<br>

## Webhooks 생성
Bitbucket 또는 API를 사용하여 webhook 생성 가능.

Project 관리자는 project 수준 webhooks(repository 수준에 상속되고 표시됨)를, repository 관리자는 repository 수준 webhooks를 아례의 단계를 걸처 생성 가능.
1. webhook을 생성하려는 위치에 따라 project 또는 repository로 이동.
2. **Project Settings** > **Webhook** 또는 **Repository Settings** > **Webhook**을 선택한 다음 **Create webhook** 선택.
3. 간단한 설명과 함께 **Title** 및 application server의 **URL** 입력.  
  이때 URL 변수도 추가 가능.
4. **Optional**: 인증 방법을 선택하고 선택한 인증 방법에 따라 추가 세부정보를 추가.
5. **Optional**: 자체 서명된 인증서를 사용하는 내부 URL과 통합하려면, SSL/TLS 인증서 확인 활성화 확인란을 선택 취소.
6. **Webhook events**: Webhook을 trigger할 event 선택.  
  기본적으로 webhook에 대한 event는 **Repository push** field에 표시된대로 repository push.
7. **Optional**: 필요한 경우 Test connection buttion 사용.
8. **Optional**: Webhook을 생성한 후 webhook이 활성화되지 않도록 하려면, Active off.
9. **Create** 선택.

API를 사용하여 webhook를 생성하려면, Bitbucket이 예상하는 HTTP request 형식과 Bitbucket이 server에 반환하는 HTTP 응답 형식을 알아야 함. 

<br>

## URL 변수 추가
다음 URL 변수 추가 가능.

URL 변수 | 사용 가능
:---: | :---:
`project.key` | All events
`repo.slug` | Repository and pull request events
`repo.ref.branchName` | Repository push events
`pr.fromRef.branchName` | Pull request events
`pr.toRef.branchName` | Pull request events

<br>

## Webhooks trigger
webhook과 관련된 event가 발생하면, Bitbucket은 event payload가 포함된 webhook URL로 요청을 전송.

다음 events에 대한 webhooks 생성 가능.

**Project events**
- 수정됨(project 수준 webhooks에서만 사용 가능)

**Repository event**
- Push
- 수정됨
- Forked
- Commit에 댓글이 추가됨.
- Commit 시 댓글이 수정됨.
- Commit 시 댓글이 삭제됨.
- Mirror가 동기화됨
- Secret이 감지됨.

**Pull request events**
- 개설됨
- Source branch가 update됨.
- 수정됨
- Reviewers가 update됨.
- 승인됨
- 승인되지 않음
- 변경이 요청됨
- 병합됨
- 거절됨
- 삭제됨
- 댓글이 추가됨.
- 댓글이 수정됨.
- 댓글이 삭제됨.

> [!NOTE]  
> 여러 branches에 대한 변경 사항이 함께 push되면, 각 branch 변경에 대해 별도의 webhook request가 전송됨.

<br>

## Webhooks troubleshooting
Webhook을 trigger하는 작업을 수행했지만 작동하지 않는 경우, **Event log** page를 사용하여 무엇이 잘못되었는지 파악 가능.

Event log를 보고 문제를 해결하려면, Webhooks page로 이동하여 작동하지 않는 Webhook에 대해 **View details**(**Actions** 열에서)를 선택.  
![image](https://confluence.atlassian.com/bitbucketserver/files/938025878/938025880/1/1505800457466/EventlogWH.png)

문제를 해결하려면, 최신 request 결과(ex: Webhook event details)를 선택.  
![image](https://confluence.atlassian.com/bitbucketserver/files/938025878/939712385/1/1509947559477/Webhooks+event+detail.png)

### Circuit breaking
Bitbucket instance를 보호하기 위해, Bitbucket webhooks system에 circuit breaking 기능이 구현됨.  
이는 지속적으로 실패하는 경우, 일정 기간 동안 잘못 동작하는 webhooks를 건너뛰는 것을 의미.

기본적으로 webhook이 5번 실패하면, 비정상으로 간주되어 건너뜀.  
처음에는 짧은 기간(10초) 동안만 건너뛰지만 계속해서 실패하면 점차적으로 최대 10시간까지 더 오랜 기간 동안 건너뜀.  
진행 중인 webhooks가 너무 많으면 webhook을 건너뛸 수도 있음.  
250개의 webhooks가 호출되는 경우, 진행 중인 수가 250개 미만으로 떨어질 때까지 추가 requests를 건너뜀.

Instance의 요구 사항이 다른 경우, 이러한 제한을 완전히 구성 가능.

Webhook을 건너뛰는 경우, Bitbucket의 JMX metrics 출력 또는 logs를 통해 확인 가능.

<hr>

## 참고
- **Webhooks 관리** - https://confluence.atlassian.com/bitbucketserver/manage-webhooks-938025878.html
