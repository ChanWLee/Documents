# SSH key & multi GitHub & IntelliJ


## SSH key 발급

1. git bash에서 실행
1. 아래 명령 입력, 이메일은 수정
```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
1. 엔터 클릭
```bash
Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
```
1. SSH 암호 입력, 암호입력없이 하려면 엔터
```bash
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
```
1. ssh key 클립보드에 복사
```bash
$ clip < ~/.ssh/id_rsa.pub
```

## 발급한 SSH key를 ssh-agent에 등록

1. ssh-agent 시작하기<br />
`# start the ssh-agent in the background`
> Git Bash<br />
`$ eval "$(ssh-agent -s)"`<br />
 다른 terminal<br />
`$ eval $(ssh-agent -s)`

1. SSH key를 ssh-agent에 추가<br />
`$ ssh-add ~/.ssh/id_rsa`


## GitHub 계정에 SSH key 등록

1. Sign in  > 아이콘 클릭 > Settings
> ![](https://help.github.com/assets/images/help/settings/userbar-account-settings.png)

2. SSH keys > New SSH key
>![](https://help.github.com/assets/images/help/settings/settings-sidebar-ssh-keys.png)

3. Title 입력, Key > Ctrl+V
>![](https://help.github.com/assets/images/help/settings/ssh-key-paste.png)

5. Addd SSH key
>![](https://help.github.com/assets/images/help/settings/ssh-add-key.png)

1. GitHub 암호 입력

***


Multi SSH keys 셋팅
---
1. 위의 방법으로 여러개의 키를 생성, ssh-agent에 추가

2. 저장된 keys 확인<br />
`$ ssh-add -l`

1. ssh config 수정
```bash
    $ cd ~/.ssh/
    $ touch config
    $ vi config
```

1. 내용추가
```shell
    #activehacker GitHub계정ID
    Host github.com-activehacker
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_rsa_activehacker

    #jexchan GitHub계정ID
    Host github.com-jexchan
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_rsa_jexchan
```
***
## IntelliJ 에 SSH key 적용

1. VCS > Checkout from Version Control > Git
> Git Repository URL:  `github.com-jexchan:jexchan/repo`
```
github.com-jexchan: config에서 설정한 Host
jexchan: github의 id
repo: repository 이름
```
 Parent Directory: `/User/workspace`<br />
 Directory Name: `repo`

1. Test 클릭

1. Clone 클릭
