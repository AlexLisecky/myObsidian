### Модуль редиректов

1. Создаем файл middleware.py в одном из приложений
2. Создаем модель
3. Подключаем в админке
4. Добавляем в настройки проекта middleware

### Middleware.py

```python
from django.http import HttpResponsePermanentRedirect
from apps.base.models import Redirect

class RedirectMiddleware:

	def __init__(self, get_response):
		self.get_response = get_response

	def __call__(self, request):
		url = request.get_full_path()
		redirect_url = Redirect.objects.filter(forpath=url).first()
		
		if redirect_url:
			return HttpResponsePermanentRedirect(f'{redirect_url.inpath}')
			
		response = self.get_response(request)
		return response
```

### models.py

```python
from django.db import models

class Redirect(models.Model):

	""" Редиректы """
	forpath = models.CharField(verbose_name='Старый url', max_length=3300, help_text='/from')
	inpath = models.CharField(verbose_name='Новый url', max_length=3300, help_text='/to')
	created_at = models.DateTimeField(auto_now_add=True)
	updated_at = models.DateTimeField(auto_now=True)

	def __str__(self):
		return f"{ str(self.forpath) } -> { str(self.inpath) }"
```

### admin.py

```python
from django.contrib import admin
from apps.base.models import Redirect

@admin.register(Redirect)
class RedirectAdmin(admin.ModelAdmin):
	list_display = ('forpath','inpath', 'created_at', 'updated_at')
	search_fields = ('inpath', 'forpath')
```

### Settings.py

```python
MIDDLEWARE = [
	'django.middleware.security.SecurityMiddleware',
	'django.contrib.sessions.middleware.SessionMiddleware',
	'django.middleware.common.CommonMiddleware',
	'django.middleware.common.CommonMiddleware',
	'django.middleware.csrf.CsrfViewMiddleware',
	'django.contrib.auth.middleware.AuthenticationMiddleware',
	'django.contrib.messages.middleware.MessageMiddleware',
	# добавляем middleware
	'apps.base.middleware.RedirectMiddleware',
]
```