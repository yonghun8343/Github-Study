# github

- 매우 주의. 작성 단계에서 컴퓨터 두개로 테스트를 해 볼 수 없기 때문에 지극히 글 쓴이의 머리에서 나온 시나리오입니다 ㅠ.ㅠ

## 목차

1. 조 구성
2. 깃 레포 만들기
3. 만든 레포에 사람 초대하기
4. 클론 받기
5. 푸쉬 해 보기
6. 브런치 파기
7. 충돌 일으키기
8. 충돌 해결하기
9. 포크 해보기
10. PR 던져보기

## 1. 조 구성

우리가 깃허브를 주로 사용할 때가 언제인지 생각을 해 보면 지금까지는 혼자 개인 프로젝트를 진행 할 때 사용 해 왔습니다.

하지만 이제부터 회사에서 깃허브를 사용 하였을 때를 가정하여 학습을 진행하려고 합니다.

그렇다면 우리가 이제 2인 1조를 맺고 깃허브를 따라 해 봅시다.

## 2. 깃 레포 만들기

우선 조에 속한 둘 다 깃허브 레포지토리를 생성 해 봅시다.

깃허브 레포지토리는 홈페이지에서 만들어야하니 깃허브 홈페이지에서 만들어 봅시다.

## 3. 만든 레포에 사람 초대하기

자 이제 우리는 테스트를 해 보기 위해서 한 사람만 다른 사람의 깃허브를 초대해 봅시다.

깃허브 초대 역시 홈페이지에서 해야하기 때문에 계속 작업을 진행합니다.

깃허브를 초대하는 방법은 다음과 같습니다.

1. Settings에 들어갑니다.
2. Access에 Collaborators에 들어갑니다.
3. 이후 Add people을 누릅니다.
4. 닉네임이나 이메일을 이용하여 초대 해 줍니다.

이제 초대 받은 사람의 이메일에서 깃허브에 들어가는 것을 봅시다.

## 4. 클론 받기

이제 클론을 받아 봅시다.

두가지 방법으로 진행할 예정이기 때문에 한명 당 하나의 방법으로 진행 해 봅시다.

1. 첫번째 방법

   - 깃허브의 Github Desktop을 설치합니다.
   - 깃허브 Code 페이지에서 `<> Code` 를 눌러 Open With GitHub Desktop을 눌러 추가 합니다.

2. 두번째 방법

   - git CLI를 실행합니다.
   - `<> Code`에 나와있는 HTTPS 링크를 복사 합니다.
   - CLI에서 git clone `링크`를 입력 해 줍니다.

다른 방법으로

1. Github CLI라는 것을 별도로 설치하여 사용
2. ZIP을 다운받아 github 연동

이후 아래의 명령을 실행 합니다.

새로운 레포지토리일 경우

```bash
echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/yonghun8343/test.git
git push -u origin main
```

기존에 존재하는 레포지토리일 경우

```bash
git remote add origin https://github.com/yonghun8343/test.git
git branch -M main
git push -u origin main
```

## 5. 푸쉬 해 보기

두 컴퓨터 모두에서 작업을 해 봅시다.

푸쉬는 커밋들을 올리는 것을 푸쉬라고 합니다.

그렇다면 커밋은 내가 작업한 영역을 중간 저장하기 위해서 마킹 해 둔다고 이해하면 좋습니다.

커밋을 하기 위해서 내가 작업한 파일을 추가 해 줍니다.

추가는 아래와 같습니다.

첫번째, 작업 디렉토리의 변경 내용의 일부만 스테이징 영역에 넘기고 싶을 때는 수정한 파일이나 디렉토리의 경로를 인자로 넘깁니다.

```bash
git add <파일/디렉토리 경로>
```

두번째, 현재 디렉토리의 모든 변경 내용을 스테이징 영역으로 넘기고 싶을 때는, .을 인자로 넘김니다.

```bash
git add .
```

이제 파일을 추가 했으면 커밋을 남겨 봅시다.

```bash
git commit -m "메세지"
```

그리고 이제 푸쉬를 해 봅시다.

```bash
git push
```

푸쉬를 해 보니 두명 중 늦게 푸쉬를 한 사람의 컴퓨터에서는 푸쉬가 안됩니다.

그 이유는 HEAD 즉 내 컴퓨터에서 깃허브를 바라 보는 위치가 다르기 때문입니다.

깃허브는 최신 코드를 가지고 있지만, 올리기 실패한 컴퓨터에는 최신코드를 가지고 있지 않으면서 push를 시도하였기 때문에 항상 최신 코드를 유지하려고 하는 깃허브에서 실패를 보낸 것 입니다.

이를 방지하는 가장 좋은 방법은 add를 하기 전에 아래의 명령어를 입력 해 보는 것 입니다.

```bash
git status
```

위의 코드를 입력하였을 때 최신코드라고 나오면 푸쉬를 하였을 때 꼬이지 않습니다.

하지만 우리는 이미 최신 코드가 있다고 나오기 때문에 pull을 진행 한 후 푸쉬를 해 봅시다.

```bash
git pull
git push
```

지금까지는 다른파일을 가지고 푸쉬를 하였기 때문에 push를 했을 때 충돌이 나지 않았습니다.

그렇다면 이제 첫번째 마크다운 파일을 둘이 다른 내용으로 수정 해 봅시다.

그리고 add 후 push를 해 봅시다.

충돌이 제대로 발생합니다.

이를 해결하기 위해서 Visual Studio Code를 이용해 봅시다.

작업 시작 .... (아마 안될 수 있을지도)

CLI로 이를 해결하기에는 매우 힘들다는 것을 참고 해 주세요.

## 6. 브런치 파기

브런치라는 것은 내가 분기점으로 부터 코드를 분할하여 새로운 작업을 진행할 때 사용 됩니다.

자 그렇다면 우선 두 컴퓨터에서 최신코드를 유지 해 주세요.

```bash
git pull
```

이제 브런치를 파 보겠습니다.

첫번째 브런치의 이름은 branch-A

두번째 브런치의 이름은 branch-B

로 통일 하겠습니다.

```bash
git branch <브런치 이름>
```

브런치를 만들었습니다. 하지만 우리의 현재 브런치는 새로 만든 브런치로 되어있지 않습니다!

이제 만든 브런치로 움직여 보겠습니다.

```bash
git checkout <브런치 이름>
```

자 이제 푸쉬를 하지 않았기 때문에 각자가 만든 브런치를 삭제 하려합니다.

다시 main 브런치로 이동해 봅시다.

그리고 아래의 명령어를 입력합니다.

```bash
git branch -d <브런치 이름>
```

이제 브런치 생성과 이동을 한번에 해 봅시다.

```bash
git checout -b <브런치 이름>
```

각자 브런치로 이동을 한 후 같은 파일을 수정 한 후 push를 해 봅시다.

이제 잘 동작하는 것을 알 수 있습니다!

## 7. 충돌 일으키기

자 이제 서로 푸쉬는 잘 되는것을 알 수 있습니다. 하지만 우리 서로 어떤 코드를 작성하였는지는 푸쉬를 하고 pull을 해도 볼 수가 없습니다. 그 이유는 브런치가 다르기 때문에 영역이 다른 곳에 쓰여진 것이기 때문입니다.

```bash
git pull
```

git pull을 한 후 서로의 브런치로 움직이면 본인의 파일의 내용이 바뀌면서 움직이는 것을 알 수 있습니다.

그렇다면 이제 하나의 브런치로 합치는 방법에 대해서 알아 봅시다.

하나로 합치는 방법은 merge라는 것을 이용합니다.

merge는 하나의 계정으로 진행하겠습니다.

main으로 이동 해 봅시다.

```bash
git checkout main
```

이제 `branch-A`를 병합 해 봅시다.

```bash
git merge branch-A
```

성공적으로 병합이 되었을 것 입니다.

그렇다면 이제 `branch-B`를 병합 해 봅시다.

```bash
git merge branch-B
```

## 8. 충돌 해결하기

충돌이 제대로 발생합니다.

이를 해결하기 위해서 Visual Studio Code를 이용해 봅시다.

작업 시작 ....

CLI로 이를 해결하기에는 매우 힘들다는 것을 참고 해 주세요.

이제 충돌을 해결하면 개인 프로젝트에서 여러명이 들어왔을 때 관리 하는 방법에 대해서 알아 보았습니다.

자 이제 역할을 바꾸어 다시 반복 해 봅시다.

## 9. 포크 해보기

깃허브를 회사계정이나 팀장의 계정에서 초대를 하였음에도 불구하고 코드를 검사받거나 코드리뷰를 하는 회사의 경우 Fork를 이용하여 진행 할 수 있습니다.

Fork라는 것은 깃허브 레포지토리를 내 깃허브 계정으로 가지고 와서 작업을 진행한다고 생각하면 좋습니다.

내 계정으로 가지고 오는 이유는 작업에 용이하기 위해서 그리고 Pull Request라는 것을 이용하기 위해서 작업 합니다.

우선 포크하는 방법을 알아 봅시다.

이번에는 지금까지 실습하던 레포 이외에 다른 레포지토리에서 작업 하려 합니다.

포크는 상대 레포지토리에 들어간 후 메인 페이지에서 우측 상단의 Fork버튼을 눌러 할 수 있습니다.

Fork를 하면서 기존의 방법을 통해서 코드를 관리해도 큰 문제가 없을 것 같은 느낌이 들 수 있습니다. 예를들어 merge를 하여 코드를 관리한다거나 하는 것을 관리자가 해 주면 안되는지 생각 해 볼 수 있습니다.

하지만 잘 생각 해 보세요... 실수로 관리자가 제 코드를 날렸더라도 관리자는 제 코드를 복구 해 주지 않습니다.

어? 코드가 날라갔네요 다시 찾아서 올려주세요 ......

또 다른 이유로는 우리가 지금까지 push를 해 보니 누가 언제 어느 코드를 수정하였는지는 일일히 다 업데이트를 확인 해야하는 불편함이 있습니다.

그렇다면 Fork를 할 때 merge가 될 예정인데 미리 merge에서 발생할 충돌을 검사를 해 주거나, 내가 허락하였을 때에만 merge가 되는 것이 필요합니다.

내 코드를 검사하고 합쳐주세요! 라고 하는 것이 PR(Pull Request)입니다.

## 10. PR 던져보기

브런치를 생성하고 파일을 생성하여 푸쉬를 해 봅시다.

자 여기서 주의할 점은 푸쉬는 기존 레포지토리가 아니라 Fork를 한 레포지토리에 푸쉬가 된다는 점 입니다.

그러므로 나의 푸쉬를 기존 레포지토리에 알려주어야합니다.

깃허브 홈페이지에서 Pull Reqeust에 들어가 봅시다.

자 이제 우측 상단의 New pull request를 눌러 봅시다.

이제 해당 내용을 자세히 봅시다.

제일 상단의 내 포크한 레포지토리에서 메인 레포지토리의 브런치로 뭔가 보낸다는 것을 알 수 있습니다.

그리고 제목과 내용을 입력 해 줍니다.

내가 수정한 코드가 맞는지 확인 하고 PR을 보냅니다.

여기서 검토자를 입력하는것도 하나의 좋은 방법입니다.

아참 참고로 Fork는 초대받지 않아도 가능하니 참고 해 주세요.

## 11. PR 병합하기

PR을 받은것을 병합 해 봅시다.

여기서 코드 리뷰를 진행할 수 있습니다.

코드 아래에 피드백을 넣고 거부 할 수 있습니다.

한번 우리가 피드백을 넣고 거부 해 봅시다.

그렇게 되었을 때 해당 피드백을 확인하고 새롭게 푸쉬를하고 PR을 다시 날리거나 할 수 있습니다.

수정 한 후 다시 PR을 보내 봅시다!

자 이제 수락을 하려고 하는데 merge를 하는 방법에 대해서 묻는 것이 있습니다.

github의 merge방식은 아래의 홈페이지를 참고 해 주세요.

[링크](https://mangchhe.github.io/git/2021/09/04/GitMerge/)

자 이제 우리는 일반 merge를 이용하여 합쳐 봅시다.

## 12. 포크 레포 최신화 하기

기존 레포지토리의 코드가 제대로 반영이 되었으나 Fork를 한 레포지토리는 그대로입니다!

그렇다면 이를 동기화 해 주어야하는데요

방법이 3가지가 있으니 제가 소개하는 방법 이외는 [링크](https://docs.github.com/ko/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork)를 참고 해 주시고 우리는 CLI를 이용하여 동기화 해 봅시다.

명령어는 다음과 같습니다.

```bash
git fetch upstream
git checkout main
git merge upstream/main
```
