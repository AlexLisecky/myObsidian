Ссылка на [pypi](https://pypi.org/project/django-ace/)

Устанавливаем

```console
pip install django-ace
```

Подключаем в настройках

```python
INSTALLED_APPS = [
	'django.contrib.admin',
	'django.contrib.auth',
	'django.contrib.contenttypes',
	'django.contrib.sessions',
	'django.contrib.messages',
	'django.contrib.staticfiles',
	'django.contrib.sitemaps',
	'django.contrib.humanize',
	'django_cleanup.apps.CleanupConfig',
	# Подключаем 
	'django_ace',
]
```

Пример перенастройки поля 

```python
from apps.project.models import Project
from django_ace import AceWidget

@admin.register(Project)

class ProjectAdmin(admin.ModelAdmin):
	list_display = ('name', 'title', 'h1')
	list_editable = ('title', 'h1',)
	prepopulated_fields = {"slug": ("name",)}
	search_fields = ('name',)

	# основная часть для переопределения
	def formfield_for_dbfield(self, db_field, **kwargs):
		if db_field.attname == "text": # text - имя поля в модели
		kwargs['widget'] = AceWidget(wordwrap=False, width="100%", height="300px", showprintmargin=True, mode='html', theme='twilight')

		return super().formfield_for_dbfield(db_field, **kwargs)
```

Настройки: 
mode = ['html', 'css', 'python' ] редактор чего
theme = 'twilight' темная тема(если не надо убрать)
