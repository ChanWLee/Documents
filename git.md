# git terminal

## repository로 push하기 - step by step

1. 초기화<br />
`$ git init`

1. 파일등록<br />
`$ git add *`

1. 상태확인 a:add, m:modify<br />
`$ git status -s`

1. commit 코멘트 작성<br />
`$ git commit`

1. remote 등록<br />
`$ git remote add bit https://url/...`
> bit: 레이블, 이후 url 대신 레이블사용

1. 등록된 모든 remote 확인<br />
`$ git remote -v`

1. remote로 push<br />
`$ git push bit master`
	> Username: 입력
    Password: 입력

1. remote 상태보기<br />
`$ git remote show bit`
