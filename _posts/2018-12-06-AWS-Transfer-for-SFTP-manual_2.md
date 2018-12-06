---
layout: post
title: AWS Transfer for SFTP add user
excerpt: "AWS Transfer for SFTP 설정 (add user): AWS SFTP, AWS S3, AWS IAM,SSH Public key"
categories: [AWS,S3,SFTP,SSH,SSH key]
tags: [AWS SFTP, SFTP add user,SSH,SSH Key]
comments: true
---
<br>
<br>
## AWS Transfer for SFTP Add user (유저 생성, SSH public key 생성)

###Add user
![Create server](https://fakett.github.io/blog/images/sftp/5.png)
- Add user를 선택 한다.

![Create server](https://fakett.github.io/blog/images/sftp/6.png)
- username : sftp 접속 때 사용할 계정 명
- Access : s3 스토리지에 접근할 IAM 정책 (S3 정책설정은 아래 URL 참고)
[S3 스토리지 IAM 간단 설정]() <- full access 정책을 적용한다고 정상적으로 동작할까? AWS는 뒷통수를 두번 친다.**명심!! 메모**
- Policy : 사용자에게 부여할 접근 권한인데 None으로 하자. (IAM 고수라면 계정마다 따로 권한 주자)
- Home directory : 친절하게도 S3버킷을 홈디렉터리로 지정할 수 있게 해 놓았다. 
오른쪽 filed 값을 넣지 않으면 선택된 버킷이 홈디렉터리가 된다. (넣어도 되고 안 넣어도 되고)


### AWS Transfer for SFTP SSH public keys
![Create server](https://fakett.github.io/blog/images/sftp/7.png)
- AWS Transfer for SFTP는 ID/PW로 Login 하지 않는다.
- 우리가 AWS를 사용하면서 지겹게 접한 SSH key를 가지고 접속 한다.
- 우선 ssh key를 만들어 보자.

```bash
[root@ip-172-31-18-233 ~]# ssh-keygen -P "" -f sftp-key
Generating public/private rsa key pair.
Your identification has been saved in sftp-key.
Your public key has been saved in sftp-key.pub.
The key fingerprint is:
SHA256:WUPsZnPkqp9lfnaugmFXMqnD9eGc4lMNiDNKrWd1J6U root@ip-172-31-18-233
The key's randomart image is:
+---[RSA 2048]----+
|         ..      |
|         .. .   .|
|         oo+ o o |
|        .oX.X E .|
|       .S* X O B |
|        o X o * .|
|         = *oo   |
|        . .=+ o .|
|         .o .=.+.|
+----[SHA256]-----+
```
- 위와 같이 `ssh-keygen -P "" -f sftp-key`를 실행하면 두개의 파일이 생성 된다.
- sftp-key, sftp-key.pub
- sftp-key.pub 파일을 cat으로 연 후 그 내용을 그대로 긁어 [**SSH piblic keys**]에 붙여 넣으면 끝

### Tag
![Create server](https://fakett.github.io/blog/images/sftp/8.png)
- 우리같은 초보는 태그를 넣지 않는다.
- [**add**]를 클릭하고 유저 생성을 마무리 짓는다.

### 3부 SFTP 접근하기 ###


