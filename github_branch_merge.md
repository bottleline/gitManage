https://cheonmro.github.io/2019/04/13/merge-branches/

여러 사람이 작업한 branch를 merge하는 방법
APRIL 13, 2019  GIT
원격저장소에 push 되어있는 branch들을 dev 브랜치로 merge 하는 방법
예시: 두 사람이(A와 B) login 브랜치와 text 브랜치를 따로 따서, 각각 원격에 push하고, 이 브랜치들을 dev 브랜치에 merge하는 과정을 순서대로 나열하면 다음과 같다.



# 1. A라는 사람이 자신의 로컬에 있는 login 브랜치를 원격 저장소에 있는 login 브랜치에 push 한다.
git add .

git commit -m "add login functions

git push origin login



# 2. B라는 사람이 자신의 로컬에 있는 text 브랜치를 원격 저장소에 있는 text 브랜치에 push 한다.
git add .

git commit -m "add text functions

git push origin text



# 3. merge를 담당하는 사람이 자신의 로컬에 있는 dev 브랜치에 원격에 있는 두 브랜치를 모두 merge 한다.
로컬에서 원격 브랜치에 접근하기 위해서는 다음의 명령어를 실행해야 한다.

git remote update

이는, 현재 원격에 있는 브랜치들을 갱신하여, 원격 브랜치들을 tracking 할 수 있게 한다.(remote-tracking branches set up locally)

fetch와 동일하다.

참고: git remote branch 가져오기



# 4. 로컬의 dev 브랜치로 이동한다.
git checkout dev

로컬의 dev 브랜치로 이동하여, 원격에 push 되어있는 새로운 브랜치(login/text)를 merge를 해야한다.



# 5. 원격에 push 되어있는 새로운 브랜치(login/text)를 merge 한다.
login 브랜치 merge

git merge origin/login

text 브랜치 merge

git merge origin/text

이때 겹치는 코드가 있다면 충돌(conflict)이 일어날 수 있다. 충돌이 난다면, 코드를 보면서 적절하게 고치면 된다.



# 6. 모든 브랜치들을 로컬의 dev 브랜치로 merge 했다면, 이 dev 브랜치를 원격으로 push 한다.
git push origin dev



참고: remote-tracking branches set up locally



# 7. merge된 원격 dev 브랜치를 다른 팀원이 로컬로 받아와, 코드를 동일하게 해야 한다.
자신의 로컬의 dev 브랜치에서, 원격에 있는 dev 브랜치의 코드와 동일하게 하기 위해서는, 다음의 명령어를 사용해야 한다.

git pull origin dev

이렇게 하면, 모든 새로운 기능들이 추가된 코드를 모든 팀원이 공유하게 되고, 다시 새로운 브랜치를 따서 새로운 기능을 개발하면 된다.
