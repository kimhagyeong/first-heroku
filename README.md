# first-heroku

2019년 7기 멋쟁이 사자처럼 과제   
heroku 를 사용해 배포하기   

* Link : <https://gentle-dusk-67227.herokuapp.com/>   


1. 프로젝트 폴더(manage.py가 있는 위치)에 .gitignore 파일 추가
```
### Django ###
*.log
*.pot
*.pyc
__pycache__/
local_settings.py
db.sqlite3
media
```
2. git init
->git status 
->git add . 
->git commit -m "commit"
->git remote add origin http
->git push -u origin master
왼쪽에 폴더들의 색깔이 하나라도 있으면 푸시 잘 안된겁니다.

3. Settings.py >>
```python
SECRET_KEY = os.environ.get('DJANGO_SECRET_KEY', 'cg#p$g+j9tax!#a3cup@1$8obt2_+&k3q+pmu)5%asj6yjpkag')
```

```python
DEBUG = bool( os.environ.get('DJANGO_DEBUG', True) )
```
4. 프로젝트 폴더 아래 Procfile 
```
web: gunicorn 프로젝트명.wsgi --log-file -
```
5. pip install gunicorn
6. pip install dj-database-url
7. pip install psycopg2-binary
8. Setting.py>>
```python
# Heroku: Update database configuration from $DATABASE_URL.
import dj_database_url
db_from_env = dj_database_url.config(conn_max_age=500)
DATABASES['default'].update(db_from_env)
```
9. pip install whitenoise
10. setting.py >> 미들웨어에 white
```bash
MIDDLEWARE = [
    'whitenoise.middleware.WhiteNoiseMiddleware',
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```
11. pip freeze > requirements.txt
12. manage.py 같은 위치에 runtime.txt
```
python-3.7.1
```
+3.7.2도 가능하다고 업데이트됨.
+본인 버전이 3.8 이상이면 히로쿠에서 제공하는 파이선 버전보다 높을 확률이 있으니 버전이 높다면 heroku python version 확인해보시고
제공하는 버전 이외라면 버전업이나 다운그레이드 해야합니다.

13. setting.py 
```bash
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
STATIC_URL = '/static/'
```
14. manage.py 와 같은 위치에 static 폴더
15. python manage.py collectstatic
그다음 꼭 깃에 업데이트를 다시해줘야함.
왜냐면 왜냐면 왜냐면 왼쪽에 폴더들이 알록달록해졌으니까.
16. git add .
->git commit -m "commit2"
->git push -u origin master
17. heroku login
18. heroku create
+크리에이트 했는데 본인이 히로쿠에서 app을 5개 이상  경우는 크리에이트가 되지 않음.
19. git push heroku master
20. heroku open


* 안된 원인
1. "", '' 문제
2. 오타
3. python version이 당시 3.8 대여서 -> 어느정도 버전 업이 되었다고 함. 파이썬 확인하고 다운그레이드 해야함.
4. heroku app이 5개가 넘어서
5. 경로문제
![image](https://user-images.githubusercontent.com/31887934/84564517-43f7b780-ad9d-11ea-98a4-6de8403e57e7.png)
