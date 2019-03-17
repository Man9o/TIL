# Django로 프로젝트 시작하기

먼저 VS code를 키고 폴더 열기로 앞서 만든 likelion 폴더를 엽니다. 지난 시간에 배운 터미널 명령어를 활용해서 VS code를 열어도 좋습니다.

    code .

## 가상환경 켜기

장고 프로젝트를 시작하려면 가장 먼저 가상환경을 켜야합니다.

    source myvenv/Script/Activate

꼭 터미널 경로에 myvenv 폴더가 있는 위치에서 진행해야합니다.

[](https://www.notion.so/26c9dc5201214f49a93bb05e0a56b62a#088720d022c24819afe7e84d58ed98d9)

가상환경 켜진게 확인 되나요?

## 첫번째 Django 프로젝트 시작하기

가상환경이 켜진 상태에서 바로 아래 명령어를 입력해서 프로젝트를 만듭니다.

    django-admin startproject firstsite

`startproject` 뒤에는 만들고 싶은 파일명을 적으면 되지만 지금은 그냥 `firstsite`로 통일합니다.

[](https://www.notion.so/26c9dc5201214f49a93bb05e0a56b62a#7f6116c9d57f43ce9938a5f861693899)

짠, firstsite라는 폴더가 생기고 그안에 firstsite와 manage.py라는 파일이 생겼습니다.

firstsite 안에 firstsite라는 폴더가 생겼습니다. 지칭이 헷갈릴것 같으니 상위 폴더 이름을 firstsiteproject로 바꿔줍니다. 그리고 그 폴더 안으로 터미널 경로를 이동 합시다.

[](https://www.notion.so/26c9dc5201214f49a93bb05e0a56b62a#2e4aed2e99124c2a831298b14ac99497)

열어보면 원가 많은 파일들이 생겼습니다. 간단한 설명은 아래 해두었으니 참고하세요.

- `startproject`로 생성된 파일들

시간이 많다면 파일을 하나하나 열어서 읽어보세요. 시간이 많다면 말이죠.

## Django 서버 작동시키기

믿기진 않겠지만 우리의 첫번째 프로젝트 생성이 끝났습니다. 아래 명령어를 통해 어떤 웹사이트가 만들어졌는지 확인해봅시다.

    python manage.py runserver

서버를 작동시키는 명령어를 치면 아래와 같이 동작합니다.

[](https://www.notion.so/26c9dc5201214f49a93bb05e0a56b62a#277e10d006844028bc9f3a9d4b937f80)

오 뭔가 작동한다.

이제 우리가 만든 웹앱을 확인할 차례입니다. [http://127.0.0.1:8000/](http://127.0.0.1:8000/) 로 브라우저 창을 열어봅시다.

- 뭐죠.. 저 주소는?

[](https://www.notion.so/26c9dc5201214f49a93bb05e0a56b62a#46452254092d4736a129518817aab0e8)

로켓이 날라간다

위 화면이 뜨면 성공적으로 장고프로젝트를 생성하고 서버를 작동시킨 겁니다. 축하합니다.

서버를 끄려면 서버가 실행중인 터미널창에서 `ctrl` + `c`를 누르면 됩니다.

# Hello World 페이지 띄워보기

장고 프로젝트를 시작했지만 우리가 원한건 날아가는 로켓이 아니였습니다. 내가 만든 페이지를 웹에 띄우는 작업을 해봅시다.  그러기 위해서는 `app`을 만들어야합니다.

아무것도 모르는 걸 아니까 하나씩 그냥 따라서 만들어봅시다.

## app 만들기

app은 아까 만든 프로젝트의 구성 단위입니다. app이 프로젝트의 작은 부분들이고, app이 모인것이 project라고 생각하면됩니다. 터미널에 app을 만드는 명령어를 쳐봅시다.

(app을 만들때 명령을 내리는 경로를 잘 확인하세요. app은 어디에 만들어도 상관없지만, 편의를 위해 manage.py가 있는 폴더에서 명령을 내리는 것을 추천합니다.)

    python manage.py startapp hello

[](https://www.notion.so/26c9dc5201214f49a93bb05e0a56b62a#d824ac69696d442ea66028fa411886df)

억.. 안그래도 복잡한데 hello라는 폴더가 또 생겼다.

[](https://www.notion.so/26c9dc5201214f49a93bb05e0a56b62a#c0842c3349b94daebd093858e67b8810)

hello 폴더 안에서 일단 알아야 할 파일은 views.py 입니다. 앞으로 페이지 만들기 위해서는 아래순서에 따라 작업해야한다고 외워둡시다.

1. settings.py ⇒ project에게 app의 존재 알리기
2. templates ⇒ views.py에서 처리된 데이터를 받아 사용자에게 화면을 보여줌
3. views.py ⇒ 데이터를 처리하는 함수 작성
4. urls.py ⇒ 요청에 맞는 함수를 views.py에서 찾아 요청 전달

**settings.py** → **templates**  → **views.py → urls.py** 순으로 연결하는 작업을 하면됩니다. 작업순서는 그냥 외우면 좋습니다.

(개발에 정해진 작업순서는 없지만, 학습의 편의를 위해 정한 순서입니다. 실제 개발은 왔다갔다하며 이루어집니다.)

## 1. project에 app의 존재 알리기 : settings.py

hello라는 app을 만들었지만 project는 그 app의 존재를 아직 모릅니다. 그래서 app을 만들었다고 등록해주는 절차가 필요합니다. settings.py파일을 열면 아래와 같은 영역이 있습니다. 

    # Application definition
    
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
    ]

여기에 만든 app을 추가해줍니다.

    INSTALLED_APPS = [
        'hello.apps.HelloConfig',
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
    ]

`hello.apps.HelloConfig` 라고 적어줍니다. 외계어 같지만 찬찬히 뜯어보면 별거 아닙니다.

hello 라는 apps 을 구성했다고 인사하는 겁니다. `hello` 폴더 안을 보면 apps.py라는 파일이 있고 그 파일을 열어보면 `HelloConfig`라는 클래스가 정의되어 있습니다. 그 녀석을 등록해주는 절차입니다.

위 작업을 마치고나면 `project`가 hello라는 `app`의 존재를 인식합니다.

- 깨알팁

## 2. Template만들기

template은 유저가 보는 화면이라 생각하면 됩니다. 웹 기본 강의에서 배웠던 html파일을 만든다고 생각하면 됩니다. 만드는 방법은 app폴더 안에 templates라는 폴더를 만들고 그 안에 html파일을 만들면 됩니다.

[](https://www.notion.so/26c9dc5201214f49a93bb05e0a56b62a#af1b7d2e395c4eb1b23610bb4ad3fd12)

왼쪽에 폴더 내용처럼 만들면 됩니다. hello라는 폴더 안에 templates라는 폴더를 만들고 그 안에 home.html을 만듭니다.

## 3. 앱 기능 구현하기 : views.py 에 함수만들기

`app`의 기능을 구현하는 부분이 이 views.py입니다. 열어보면 `from`으로 시작하는 `import` 구문과 주석 한줄 딸랑 있습니다. 아래에 우리가 사용할 함수를 정의해 주면 됩니다.

    from django.shortcuts import render
    
    # Create your views here.
    
    
    def home(request):
        return render(request, 'home.html')

여기서는 큰 기능 없이 요청이 들어오면 home.html 파일을 열어주는 home 이라는 함수를 구현했습니다. html 파일(template)을 연결하기 위해 사용하는 이런 함수가 기본이니 외워둡시다.

## 4. URL 요청을 views에 연결하기 : urls.py

먼저 firstproject 폴더안의 urls.py를 열면 아래와 같은 코드가 적혀있습니다.

    from django.contrib import admin
    from django.urls import path
    
    
    urlpatterns = [
        path('admin/', admin.site.urls),
    ]

위에 친절한 주석은 나중에 읽어보시기 바랍니다. 일단 urls.py에서 hello폴더안에 있는 views.py을 읽어와야하니 `import`를 해줍니다.

    from django.contrib import admin
    from django.urls import path
    import hello.views
    
    urlpatterns = [
        path('admin/', admin.site.urls),
    ]

hello.views는 hello폴더안에 views 파일이라는 뜻입니다. 이렇게 `import` 했으면 urlpatterns에 path를 추가해줍니다.

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('', hello.views.home, name='home'),
    ]

path는 3가지 인수를 받습니다. 제일 먼저 route라는 녀석인데, 도메인 뒤에 붙는 url 부분이라고 보면됩니다. 

- route 이해하기

두번째로 오는 건 내가 연결하고 싶은 views안에 정의된 함수입니다. hello폴더 안에 views파일 안에 home이라고 정의된 함수를 실행시키겠다라는 말입니다.

마지막에 적힌 **name='home'**은 이 path의 이름을 home이라 정하겠다고 약속을 하는 내용으로, 이렇게 약속을 하면 django프로젝트 어디에서든 home이라고 불러서 호출해 낼 수 있습니다.

가능한 함수이름과 path의 name을 일치시켜주는게 정신건강에 이롭습니다.

이 파일 저파일 왔다갔다 정신 없을 겁니다.

정리해보자면,

1. project를 만들고, 
2. app을 만들고,
3. project에 app을 연결하고,
4. app에서 templates폴더를 만들고 그 안에 html파일(template)을 만들고,
5. app에서 views.py를 만든다음,
6. urls.py에서 templates안의 html파일과 연결해주는 과정입니다.

그 결과 서버를 돌리면... Hello world가 짜잔하고 브라우저에 나타납니다.

[](https://www.notion.so/26c9dc5201214f49a93bb05e0a56b62a#5cf73a124c844f078e03eaee4b532542)
