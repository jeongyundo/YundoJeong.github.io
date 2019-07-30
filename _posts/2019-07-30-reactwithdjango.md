<h1>뒤는 Django가 앞은 React가 맡는다</h1>

간단예제이다.

---

https://github.com/jeongyundo/reactwithdjango에 올려져 있으며,

이 글은 [https://this-programmer.com/entry/%EA%B0%84%EB%8B%A8%ED%95%9C-react-JS-Django-%EC%96%B4%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98-%EB%A7%8C%EB%93%A4%EA%B8%B0](https://this-programmer.com/entry/간단한-react-JS-Django-어플리케이션-만들기) 을 바탕으로 만들어졌다.

제목 그대로 뒤는 장고가 맡고 앞은 리엑트가 맡는다. 백엔드는 python기반의 django를 이용하고 프론트엔드는 javascript기반의 react를 이용하였다. 

처음에는 어찌 다른 두개의 언어를 이용할 수 있을까? 의문이 들었는데, 두개를 분리해서 사용하면 간단하게 만들 수 있다. Django-rest-framework를 이용해 통신하면된다. React는  GET,POST,DELETE,PUT restful-api 통해서 django로 부터 정보를 가져올 수 있다. 이렇게 두개를 분리하면 일단은 간단하다. 

중요한 포인트만 집고 가겠다. 일단 기본 설정 혹은 실행 방법은 위에 내가 따라한 사이트에 모두 상세히 서술되어있기 때문에 이를 따라주면 된다.



![20190730screenshot1](/images/20190730screenshot1.png)

react는 특정주소로 요청(request)를 하게되면 django에서는 json형태로 react에 요청에 따른 응답(response)를 해주게 된다. 이에 필요한게 django의 rest_framework가 중요하게 사용된다. 

<h2>Django의 연결</h2>

장고의 settings.py 파일이다. 추가된 부분만 올렸다.

```python
INSTALLED_APPS = [
    'post',           # 추가
    'rest_framework', # 추가
    'corsheaders',    # 추가
]

MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',     # 추가
    'django.middleware.common.CommonMiddleware', # 추가
]

CORS_ORIGIN_WHITELIST = [
  'http://localhost:3000'
] 
#script안에서의 리소스 요청을 허용할 도메인 추가
```

<h3>추가된 라이브러리</h3>

```powershell
pip install django-cors-headers
pip install djangorestframework
```

djangorestframework는 api를 통해 json형태로 요청 및 반환을 해주기 위해서 설치된다.

django-cors-headers는 api를 통한 데이터의 접근제어를 위한 HTTP 접근제어 규약(CORS : Cross-Origin Resource Sharing)을 위해서 설치된다.

<h4>Django-cors-headers</h4>

```python
MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',     # 추가
    'django.middleware.common.CommonMiddleware', # 추가
]

CORS_ORIGIN_WHITELIST = [
  'http://localhost:3000'
] 
```

Cors_origin_whitelist를 통해서 리소스 요청을 허용할 도메인 추가해준다. 그러면 React가 실행되는 'http://localhost:3000'의 요청을 허용해준다.



<h4>Django Rest Framework</h4> 

```python
from rest_framework import serializers
from .models import Post

class PostSerializer(serializers.ModelSerializer):
    class Meta:
        fields = (
            'id',
            'title',
            'content',
        )
        model = Post
```

 장고 레스트 프레임워크는 RESTful형식으로 데이터를 GET,POST,PUT,DELETE를 할수있다. 이 라이브러리를 설치해서 사용하면 web APIs를 만들 수 있다. 자세한 사항은 https://www.django-rest-framework.org/ 여기서 확인할 수 있다. 그리고 이중에서 중요한게 response를 해줄때 값을 json형식으로 보내야 하기 때문에 serializer를 만들어 주어야한다. 

 위의 형태로 만들시 id, title, content는 json의 형태로 전송된다.



<h2>React의 연결</h2>

```javascript
async componentDidMount() {
        try {
            const url = 'http://localhost:8000/api/';
            const res = await fetch(url);
            const posts = await res.json();
            this.setState({
                posts
            });
        } catch (e) {
            console.log("error",e);
        }
    }
```

react에서는 fetch를 통해서 값을 가져온다. posts에 json형태로 값을 제공해주면 setState를 통해 값을 설정해 줄 수 있다.

<h2>결과물</h2>

<h3>React 화면</h3>

![20190730screenshot2](/images/20190730screenshot2.png)

<h3>Django 화면</h3>

![20190730screenshot3](/images/20190730screenshot3.png)

---

이렇게 간단하게 Django와 react를 연결해 보았다. 이 방법의 장점은 두개가 분리되어 프론트는 프론트대로 백은 백대로 따로 관리하면 된다는 점이 있다. 그런데 프로그래밍이 간단할리 없지 않겠는가? 인증 작업 및 구분과 SSR에 대한 장애물이 존재하는데 이에 대한 부분은 추후에 공부를 하면서 업로드를 하겠다.
