# Notifications

<br>

Email 알림을 보내려면 Bitbucket Data Center 및 Server에 email server를 구성해야 함.  
Mail server에 장애가 발생하면, 알림은 삭제됨.

<br>

## Batched email 알림
알림은 각 pull request에 대해 user별로 집계되며 일괄적으로 email로 전송됨.  
일정 시간(기본값은 10분)동안 조용해지거나 가장 오래된 알림이 `stale`(기본값은 30분)되는 경우 중 먼저 도래하는 경우 일괄 처리가 전송됨. 

기본적으로 email 알림은 일괄 처리되지만:
- 알림을 즉시 받을 수 있도록 개인 계정 설정의 **Notifictation settings** tab에서 변경 가능.
- Pull request 알림과 repository 알림에는 알림을 일괄 처리하거나 즉시 수신하도록 별도의 설정이 존재.  
  예를 들어 pull request 알림을 즉시 수신하도록 선택할 수 있지만, repository 알림은 일괄적으로 수신하도록 설정 가능.
- Bitbucket 관리자는 Bitbucket Server config properties file에서 비활성 기간과 비활성 시간 초과 기간 구성 가능.
- Bitbucket 관리자는 system property를 사용하여 Bitbucket instance의 알림 모드를 `immediate`로 변경 가능하지만 users는 일괄 알림을 계속 선택 가능.

<br>

## Mentions를 사용해 누군가에게 알림
Bitbucket 2.0부터 `mentions`를 사용하여 자신이 작성 중인 pull request description이나 댓글을 다른 user에게 알림 가능.  
Bitbucket은 해당자에게 email을 전송.
- 개인 계정 설정에서 일괄 처리를 선택한 경우, email이 일괄 처리 됨.

`@`을 입력하면 name, username 또는 email 주소가 Bitbucket이 제공하는 목록으로 표시되는데 여기서 선택.  
공백이 있는 경우와 같이 특이한 이름에는 따옴표 사용 가능.  
Mention을 미리 보려면 Control-Shift-P 또는 Command-Shift-P 사용.

<hr>

## 참고
- **Notifications** - https://confluence.atlassian.com/bitbucketserver0813/notifications-1283690267.html
