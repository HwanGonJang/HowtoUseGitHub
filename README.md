# GitHub의 모든 것(git을 활용한 버전관리, 백업, 협업)
깃(git)은 리눅스의 개발자인 리누스 토르발즈가 만든 문서 관리 프로그램입니다. git이 세상에 등장하기 전까지는 몇천줄이 되는 코드들을 오픈소스 방식으로 굉장히 복잡하게 작성했지만 git을 통해 수많은 코드들을 효율적으로 관리할 수 있게 되었습니다. 깃에서 할 수 있는 기능으로는 크게 버전관리, 백업, 협업이 있습니다. git은 현재 많은 개발자, 기업들이 문서를 관리하고 협업하는데 이용하고 있는 대표적인 프로그램입니다. 
갑자기 깃허브를 공부해야겠다고 생각한 이유는 7월 29일~31일 3일간의 해커톤 참여 이후였습니다. 해커톤에서 만난 같은 학부 선배님이 저를 비롯한 팀원들에게 간단한 깃허브 협업 방법을 알려주었고 깃허브라는 도구에 대해 중요성을 느끼게 되었습니다. 따라서 이번 기회를 통해 제대로 깃허브를 공부하고 활용하는 방법을 정리해보도록 하겠습니다.

## 1. git 설치하기
https://git-scm.com/
깃을 사용하기 위해 깃 프로그램을 설치해줍니다.

git을 설치한 후 커맨드로 git을 입력해줍니다. usage: 로 시작하는 여러 사용옵션이 나오면 성공입니다.
~~~git
	git
~~~
<img src ='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_1.png?raw=true'></img>

정상적으로 출력이 된다면 다음과 같이 입력하여 사용자 정보를 저장합니다.
~~~git
	git config --global user.name "HwanGonJang"
	git config --global user.email "myggona@gmail.com"
~~~
이것으로 기본적인 git 환경 세팅은 끝났습니다.

## 2. 깃으로 버전 관리하기
우선 테스트 디렉토리를 만들어줍니다.
~~~git
	mkdir TestGit
	cd TestGit
	git init
~~~
TestGit이라는 디렉토리를 만든후 초기화하는 코드입니다.
~~~git
	ls -la
~~~
하위 파일들을 살펴보면 .git/ 파일이 있는데 이곳이 깃의 버전이 저장되는 저장소입니다.

#### 버전?
깃에서 버전이란 문서를 수정하고 저장할 때마다 생기는 것입니다. 개발과정에서 소스코드를 계속해서 수정하고 저장하는데 이때마다 1.2.3 과 같은 방식으로 버전을 붙여주는 것입니다.

#### 스테이지와 커밋
깃에는 작업트리와 스테이지 커밋이라는 개념이 있습니다.

* 작업트리
	* 파일의 수정을 작업하는 디렉터리. (TestGit)
* 스테이지
	* 버전화할 파일이 대기하는 위치. 이곳에서 스테이징된 파일만 버전이 생깁니다.
* 저장소
	 * 저장소는 스테이지의 파일을 버전화하여 저장하는 곳입니다. 저장소에 저장하기 위해 스테이지에서 버전을 만드는데 이때 **커밋** 명령을 내립니다. 


이제 문서 관리를 해보겠습니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_2.png?raw=true'></img>
~~~git
	vim hello.txt
~~~
vim 편집기로 아무 단어나 적은 txt 파일을 만들었습니다.
~~~git
	git status
~~~
위 명령어로 깃의 상태를 확인해보면 Untracked files: 에 hello.txt가 생겼습니다. 이제 파일을 버전 관리할 수 있습니다.
~~~git
	git add hello.txt
	git status
~~~
add 명령어는 작업트리의 파일을 스테이징하는 작업입니다.
이제 new file: hello.txt 를 확인할 수 있습니다. 이 파일을 커밋할 수 있다는 뜻입니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_3.png?raw=true'></img>
~~~git
	git commit -m "commit1"
~~~
스테이징된 파일을 커밋하는 명령어입니다. commit1이라는 메시지와 함께 커밋해줍니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_4.png?raw=true'></img>
~~~git
	git log
~~~
git log 명령을 통해 커밋 기록을 살펴볼 수 있습니다.

이외에도 스테이지, 커밋 되돌리기, 구체적인 로그 확인(git diff) 등 여러가지 유용한 기능이 있습니다.


## 3. 브랜치
 모든 버전관리 시스템에는 브랜치(Branch)라는 개념이 있습니다 여러갈래의 나뭇가지 처럼 파일 데이터의 흐름을 가리키는 말로 사용합니다.

 브랜치가 필요한 이유는 무엇일까요?  예를들면 개발한 서비스를 필요로 하는 고객들의 니즈가 모두 다른 경우가 있습니다. 만약 브랜치가 아니라 단순히 고객별로 개발 소스들을 따로따로 복사하고 니즈에 맞게 수정한다면 깃의 장점인 깔끔한 문서 관리를 완전히 무시하고 다시 복잡한 시스템으로 돌아가는 것입니다. 또 필요한 기능이 다른 고객을 위한 소스트리에 있다고 그 코드를 다시 가져오는 것도 불가능합니다. 이미 그 고객에 맞게 코드가 짜여져있기 때문에 현재 고객을 위한 코드에서 오류가 나올 수 있는 확률이 매우 높기 때문입니다.

 따라서 깃은 브랜치라는 기능을 제공합니다. 깃을 사용하면 master 라는 단어가 보이는데 이것이 기본적으로 만들어지는 브랜치입니다. 여기에 새로운 브랜치를 만든다면 기존 master의 파일들을 유지하면서 파일이나 소스코드를 유지보수 할 수 있습니다. 이렇게 새로 뻗어나오는 가지(Branch)를 분기라고 합니다. 또, 이러한 새로운 브랜치를 보수하고 다시 master 브랜치에 병합하는 것을 머지(merge)라고 합니다.

### 브랜치 만들기
~~~git
	mkdir TestBranch
	cd TestBranch
	git init
	ls -al
~~~
위 처럼 다시 디렉토리를 만들어줍니다.
~~~git
	vim work.txt
~~~
vim으로 content 1 을 적습니다.
~~~git
	git add work.txt
	git commit -m "work 1"
~~~
이 파일을 스테이징하고 커밋해줍니다.

이 파일을 work2,3으로  content2,3을 추가해 두번 더 커밋해줍니다.
다시 git log로 확인해보면 가장 최신에 커밋한 work 3 에 HEAD -> master 가 표시됩니다. master 브랜치가 가장 최신 커밋인 work 3 를 가리키고 HEAD는 master를 가리키고 있습니다. HEAD는 현재 작업 중인 브랜치를 말합니다.

이제 새 브랜치를 만듭니다.
<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_5.png?raw=true'></img>

~~~git
	git branch branch1
	git branch
~~~
위 명령어로 branch1이라는 브랜치를 만들고 확인합니다. git branch를 입력하면 만들어진 branch1을 확인할 수 있습니다. * 표시는 현재 브랜치를 의미합니다.

이제 브랜치를 2개 더 만들어보겠습니다.
~~~git
	git branch branch2
	git branch branch3
	git branch
~~~

이렇게 브랜치를 만들게 되면 해당 브랜치로 이동이 필요합니다. 먼저 현재 master 브랜치에서 새로운 커밋을 추가하겠습니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_6.png?raw=true'></img>
~~~git
	vim work.txt
	//am은 스테이징과 커밋을 한번에 처리하는 옵션입니다.
	git commit -am "master content 4"			
	git log --oneline
~~~

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_7.png?raw=true'></img>
master 브랜치에서 커밋 후에 한 줄에 하나씩 커밋을 보여주는 옵션인 --oneline을 입력하면 다음과 같이 나옵니다. 네번째 커밋은 master content 4 는 master 브랜치에만 적용되어 있습니다.
~~~git
	git checkout branch1
~~~
branch1으로 체크아웃하여 브랜치를 이동합니다. 이렇게 하면 커맨드의 (master) 가 (branch1) 으로 바뀝니다. 

### 새 브랜치에서 커밋하기
브랜치를 바꾼 후에 다시 다음 코드를 입력해줍니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_8.png?raw=true'></img>
~~~git
	 git log --oneline
	 cat work.txt
~~~
이제 로그에는 branch1의 최신 커밋인 work 3만 나오게 되고 work.txt에는 4번째 커밋을 하기 전 파일의 내용이 나옵니다.

### 새 브랜치에서 커밋하기
branch1에서 새로운 커밋을 해보도록 하겠습니다. work.txt에 branch1 content 4 를 추가하고 vim branch1.txt 파일에 branch1 content 4를 추가하고 저장합니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_9.png?raw=true'></img>
~~~git
	git add .
	git commit -m "branch1 content 4"
	git log --oneline
~~~
add 명령어 뒤에 . 을 붙여서 수정한 모든 내용을 스테이징하고 커밋해줍니다. 로그를 확인하면 branch1이 새로운 커밋을 가리킵니다.

### 브랜치 병합하기
작업이 끝난 브랜치를 병합할 때에는 먼저 master 브랜치로 이동해야합니다. 이동 후 머지 명령으로 브랜치를 병합해줍니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_10.png?raw=true'></img>

~~~git
	git checkout master
	git merge branch1
~~~
이렇게 하면 다음과 같이 conflict 오류가 납니다. 이는 수정된 문서에서 충돌 되는 부분이 있어서 병합할 수 없다는 오류로 충돌이 없다면 자동으로 커밋 메시지와 함께 병합됩니다.

충돌의 경우에는 사용자가 직접 수정해주어야 합니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_12.png?raw=true'></img>
~~~git
	vim work.txt
	git commit -am "merge branch1"
	//--graph 명령은 브랜치를 깔끔하게 보여줍니다.
	git log --oneline --graph		
~~~

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_11.png?raw=true'></img>

vim에서 충돌된 부분을 보여줍니다. 여기서 사용할 부분을 제외한 나머지를 지우고 직접 커밋해줍니다. 이후 다시 로그를 확인하면 브랜치의 과정을 깔끔하게 확인할 수 있습니다.

### 브랜치 관리하기
#### 브랜치 삭제
브랜치 삭제는 master에서 진행하여야 합니다.
~~~git
	git branch -d branch1
~~~
브랜치 삭제는 실제로 삭제하는게 아닌 감추는 것입니다.

#### 브랜치 리셋
~~~git
	git reset "해시코드"
~~~
로그에서 확인한 해당 커밋의 해시를 입력하여 최신 커밋을 바꾸는 명령입니다. 연결이 끊어진 다른 커밋을 삭제됩니다.

#### 파일 감추기
~~~git
	git stash
~~~
파일을 커밋하기 전 다른 파일을 수정해야하는 상황에서 git stash 명령으로 잠시 감출 수 있습니다. stash는 파일을 배열에 스택 형식으로 보관하고 pop으로 최신 파일을 꺼내올 수 있습니다.
~~~git
	git stash pop
~~~


## 4. 깃허브 사용하기
지금까지 파일을 관리한 위치는 모두 컴퓨터 자원인 로컬 저장소입니다. 하지만 깃은 깃허브와 연결하여 원격 저장소에 백업할 수 있습니다. 먼저 지역 저장소를 원격 저장소에 연결하겠습니다. 이를 위해선 깃허브에 리포지토리를 하나 만들어주어야 합니다. 저는 TestRepositorty로 만들었습니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_13.png?raw=true'></img>
~~~git
	git init local			//init을 사용하면 한번에 초기화하고 디렉토리를 만듭니다.
	cd local
	vim file.txt			//1 입력
	git add file.txt
	git commit -m "first"
	git log
~~~
파일을 하나 만들어서 커밋해줍니다. 

만든 리포지토리의 주소를 복사합니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_14.png?raw=true'></img>
~~~git
	git remote add origin "복사한 리포지토리 주소"
~~~
이 명령은 원격 저장소에 origin을 추가하는 명령입니다. 이때  origin은 주소를 나타냅니다.
~~~git
	git remote -v
~~~
-v 옵션으로 연결된 주소를 확인할 수 있습니다.

#### 푸시하고 풀하기
깃허브에서는 지역 저장소에서 원격 저장소로 올리는 작업을 푸시, 그 반대를 풀이라고 합니다. 먼저 만들어둔 파일을 푸시 해보겠습니다.
~~~git
	git push -u origin master
~~~
이렇게 하면 깃허브 리포지토리에서 compare&pull 버튼이 생깁니다. 하지만 클릭해보면 안에서 더 할 수 있는 동작이 없습니다. 이는 깃허브의 기본 default 브랜치가 main이기 때문입니다. 흑인 문화를 위해 master 표현이 main으로 바뀌어서 master 브랜치에서는 제대로 push가 되지 않습니다. 따라서 지금은 다음과 같이 브랜치를 변경해줍니다.
~~~git
	git branch main master -f
	git checkout main
	git push origin main -f
~~~
푸시 명령으로 리포지토리에 파일이 올라간 것을 확인할 수 있습니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/g1_15.png?raw=true'></img>

파일을 가져오고 싶을 때는
~~~git
	git pull origin main
~~~
위 명령으로 가져올 수 있습니다.


## 마무리
이렇게 기본적인 깃과 깃허브 사용법을 공부해보았습니다. 이외에도 공부하면서 여러가지 명령어와 기능들을 보았지만 가장 기본적인 부분들만 정리했습니다. 처음 깃허브를 시작할 때는 단순히 개발한 코드들을 올려놓는 사이트라고 시작했지만 제대로 공부하면서 정말 크고 넓은 플랫폼임을 느낄 수 있었습니다. 이제 깃허브를 활용하여 더 효율적이고 간단하게 제 여러가지 개발 결과물을 정리할 수 있을 것 같습니다. 

남은 2021년도 동안 친구와 제대로 된 앱 개발을 하려고 준비하고 있습니다. 이렇게 공부한 깃과 깃허브를 이제 직접 활용하여 협업할 수 있도록 하겠습니다.

*공부한 책: Do it! 깃&깃허브 입문(고경희 저)
