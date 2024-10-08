# Using [GitHub](https://github.com)

## What is GitHub

[GitHub](https://github.com)는 앞서 배운 Git의 원격 저장소 역할을 수행하는 서비스로, 개인 계정을 생성하고, 그 계정을 이용해 무료로 원격 저장소를 이용할 수 있다. 무료로!

## Using GitHub

GitHub를 사용하기 위해서는 계정이 필요하다. 먼저 [GitHub](https://github.com) 사이트로 이동해보자.

![](./res/image01.png)

꽤나 현대적인 디자인의 페이지가 우리를 반겨준다. 이제 우측 상단의 Sign up 버튼을 눌러 계정을 생성한 뒤 로그인하자. ~~나선 은하가 뭔지 안다면 좋을 것이다.~~

이제 내 고유한 닉네임이 생겼다. `https://github.com/[YOUR_NAME]`으로 이동하면 내 프로필을 볼 수 있다.

![](./res/image02.png)

예시는 나의 GitHub 프로필 창이다. 상단의 메뉴 중 `Repositories`를 누르면, 내 원격 저장소의 목록이 뜬다. 당신이 방금 GitHub 계정을 처음 만들었다면, 아마 `Repositories`는 비어있을 것이다. 우측 상단의 초록색 `New` 버튼을 눌러 새 저장소를 만들어 보자.

![](./res/image03.png)

몇가지 옵션을 조정할 수 있는데, 간단히 `Repository name`을 `my-repo`로 하고 저장소를 생성해보자. 접근 수준은 `Public`으로 설정하고, `Add a README file`을 체크하여 저장소 생성과 동시에 첫 파일을 추가할 수 있다. 우리가 이전 장에서 `git init --bare`로 생성하던 저장소를 GitHub에서 웹 브라우저로 생성한 것이라고 볼 수 있다.

![](./res/image04.png)

그렇게 하면 내 첫 저장소로 `my-repo`가 생성되고, 간단한 `README.md` 파일이 하나 추가된 것을 볼 수 있을 것이다.

> `README.md` 파일은 저장소에 대한 설명을 적는 공간으로, 특히 GitHub에서는 최상의 경로의 `README.md` 파일은 저렇게 대문짝만하게 보여준다. 누군가에게 프로젝트를 공개할 때는 해당 파일을 잘 작성해두자.
>

## 실습

### Clone from Web

이제 내 컴퓨터에서 원격 저장소의 내용을 복제해 올 시간이다. 앞서 Bare repository를 만든 것을 기억하는가? `git clone [PATH]`를 통해 `[PATH]`에 있는 원격 저장소를 현재 위치로 클론했었다. 이번에는 저 `[PATH]`에 웹 상의 경로를 넣어 복제할 것이다.

```sh
git clone https://github.com/[YOUR_NAME]/my-repo    # GitHub에서 저장소 복제
cd my-repo                                          # 복제된 저장소로 이동
```

위 명령어를 입력하면 내가 웹에서 만든 원격 저장소의 내용이 내 컴퓨터로 클론된 것을 확인할 수 있다. 만약 `README.md` 파일을 만들었다면, 파일도 함께 클론되었을 것이다.

Git config는 저번에 설정하였으니, 이번에는 그냥 푸시하면 될 것이다. 하지만 권한과 관련된 이유로 푸시가 거부되는 모습을 볼 수 있다. 공개 저장소이기에 아무나 클론할 수는 있지만, 그렇다고 아무나 푸시할 수 있다면 당연히 문제가 될 것이기 때문이다.

### Token

우리는 다시 GitHub로 가서 오른쪽 제일 위의 아이콘을 눌러 메뉴 창을 열어, `Settings`로 이동할 수 있다. 그 후  `Developer Settings`, `Personal access tokens/Tokens (classic)`으로 이동해  토큰 생성 화면으로 이동할 수 있다.

GitHub 토큰은 내 GitHub 계정에 대한 부분적인 권한을 부여하는 것으로, 지금은 내 Repositories에 대한 읽기 및 쓰기 권한을 가진 토큰을 만들 것이다. `Generate new token/Generate new token (classic)`을 눌러 토큰 생성 화면으로 이동하자.

![](./res/image05.png)

`Note`에는 토큰의 설명(사실상 이름)을 적고, 아래에 토큰의 유효기간을 설정한다. 그 후 여러 권한 중 제일 위에 있는 `repo` 체크 박스를 체크해 저장소에 대한 전반적인 권한을 부여하고, 토큰을 생성하면 한번만 볼 수 있는 `ghp_...`으로 이루어진 토큰을 복사할 수 있다. 해당 토큰을 복사한 뒤 아래와 같이 사용한다.

### Push

```sh
git remote add origin https://[YOUR_NAME]:[GITHUB_TOKEN]@github.com/[YOUR_NAME]/my-repo # Git이 인식하는 경로를 토큰을 포함하게 변경
```

`[GITHUB_TOKEN]`에는 아까 복사해두었던 `ghp...`을 사용하면 된다. 만약 이미 `origin`이 존재한다고 뜰 경우 아래의 커맨드를 먼저 입력한 뒤 위의 커맨드를 다시 시도해보자.

```sh
git remote remove origin                                                                # 기존에 쓰이던 경로를 삭제
git remote add origin https://[YOUR_NAME]:[GITHUB_TOKEN]@github.com/[YOUR_NAME]/my-repo # Git이 인식하는 경로를 토큰을 포함하게 변경(재시도)
```

이제 아래의 커맨드를 사용하면 새로운 경로를 사용하게 된다.

```sh
git push --set-upstream origin main # 새 경로를 main 브런치와 연결
```

위 커맨드에서 보았던 `remote`라던가 `origin`이라던가 하는 내용은 다음에 좀 더 자세히 알아보도록 하고, 지금은 기존에 클론했던 `https://github.com/[YOUR_NAME]/my-repo`를 `https://[YOUR_NAME]:[GITHUB_TOKEN]@github.com/[YOUR_NAME]/my-repo`로 바꾸어 인증을 진행한다고 이해하고 있자.

이후에는 토큰이 유효한 이상 간단히 `git push/pull`로 사용 가능하다. 아래의 순서를 따라한 뒤 웹 브라우저에서 내 저장소를 다시 확인해보자.

```sh
echo "Hello, GitHub!" > github.txt      # 파일 추가
git add .                               # 파일 등록
git commit -m "feat: add github.txt"    # 파일 커밋
git push                                # 푸시
```

이제 브라우저에서 내 저장소를 확인하면 내가 푸시한 파일이 올라가 있는 것을 볼 수 있다.

만약 내 개인 컴퓨터라면 토큰을 하나 발급하여 로컬에 저장해두고 사용함으로서 간단히 GitHub에 접근할 수 있을 것이다.

또한 비공개 저장소에 저장된 내용을 클론하려고 한다면 이 역시 토큰이 필요한데, 기본적으로 클론을 시도하면 로그인을 하라는 내용이 나오게 된다. 하지만 비밀번호로는 로그인을 하여도 로그인이 되지는 않는다. 해당 기능은 더이상 지원되지 않는 기능으로, 로그인을 통한 GitHub 접근은 더이상 불가능하다는 의미이다. 대신 비밀번호 자리에 토큰을 넣어 사용할 수 있다.

또는 애초에 클론을 진행할 때 토큰을 사용하여 아래와 같이 사용할 수도 있다.

```sh
git clone https://[YOUR_NAME]:[GITHUB_TOKEN]@github.com/[YOUR_NAME]/my-repo # 처음부터 경로에 토큰을 포함해서 클론
```

이렇게 클론된 저장소는 클론될 때 부터 경로에 토큰이 포함되므로, 별도의 과정없이 커밋과 풀, 푸시 등이 모두 가능하므로 번거로운 과정을 피하고 싶다면 이 방법을 추천한다.

> 만약 당신이 VS Code와 같은 도구를 사용하여 프로그래밍한다면, 해당 도구에서 GitHub 계정에 로그인 해두고, 해당 도구의 Shell 창을 이용하는 방식으로 토큰 없이 내 GitHub 계정에 손쉽게 접근 가능하다. 보통은 이 방식을 이용하는 것이 좋다.
>

## 미션 1

GitHub는 그 외에도 마치 커뮤니티와 같은 여러가지 기능을 제공해준다. 아래의 내용들을 한번 따라해보자.

1. 사용자 프로필을 수정해보자. 아이콘 및 소개, 경력 등을 수정할 수 있다.
2. [YOUR_NAME]/[YOUR_NAME] Repository를 만들어보자. 해당 저장소의 README 파일은 내 프로필에서 표시되는 일종의 메인 페이지이다.
3. 검색을 이용해 다른 사람의 프로필과 공개되어있는 저장소들을 보러가자. 대표적으로 [Microsoft](https://github.com/microsoft), [Apple](https://github.com/apple) 등의 저장소를 구경할 수 있을 것이다. ~~아니면 [이 아저씨](https://github.com/torvalds)의 [그것](https://github.com/torvalds/linux)~~
4. 마음에 드는 저장소를 Starring 할 수 있다. 몇가지 저장소를 Starred로 만들어 보자.
5. 마음에 드는 유저를 팔로우 할 수도 있다. 몇 명의 유저를 찾아 팔로우를 걸어보자. ~~[이 아저씨](https://github.com/torvalds)는 팔로잉이 0이니까 팔로우 하지 말자.~~

## 미션 2

현재 사용한 클래식 GitHub 토큰은 모든 저장소에 대해 같은 수준의 권한을 갖기 때문에 비교적 보안에 취약하다. 현재는 Beta로 표시되어 있는 `Fine-grained tokens`를 만들어 `my-repo`에 대한 권한만을 취득해서 사용해보자.

---

### References
1. Test alone
2. [GitHub Docs - Managing your personal access tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)

<p align=center><a href="../README.md">Go to main menu</a></p>
