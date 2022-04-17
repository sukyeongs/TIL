# Django Simple JWT  

DRF 공식문서에 따르면 djangorestframework-`simplejwt` 라이브러리를 사용할 것을 권함. (djangorestframework-`jwt` 라이브러리는 더이상 업데이트 x)

## 1. djangorestframework-simple jwt 설치

1) terminal에 입력

```python
pip install djangorestframework-simplejwt
```

2) [settings.py](http://settings.py) 수정

```python
REST_FRAMEWORK = {
    ...
    'DEFAULT_AUTHENTICATION_CLASSES': (
        ...
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    )
    ...
}
```

```python
INSTALLED_APPS = [
    ...
    'rest_framework_simplejwt',
    ...
]
```

3) [urls.py](http://urls.py) 수정

```python
from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)

urlpatterns = [
    ...
    path('api/token/', TokenObtainPairView.as_view(), name='token_obtain_pair'),
		path('api/token/verify/', TokenVerifyView.as_view(), name='token_verify'),
    path('api/token/refresh/', TokenRefreshView.as_view(), name='token_refresh'),
    ...
]
```

`TokenObtainPairView`: simplejwt 라이브러리에서 제공하는 **토큰 생성** 뷰

`TokenVerifyView` : simplejwt 라이브러리에서 제공하는 **토큰 유효성 확인** 뷰

`TokenRefreshView` : simplejwt 라이브러리에서 제공하는 **refresh token**으로 **access token 재발급**하는 뷰