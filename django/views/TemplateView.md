### Общая структура

```python
from django.views.generic import TemplateView # импорт модуля
from apps.models import Model

class Home(TemplateView):
	template_name = 'index.html'

	def dispatch(self, request, **kwargs):
		""" Метод Dispatch """
		pass

	def get_context_data(self, **kwargs):
		""" Получение контекста """
		context = super().get_context_data(**kwargs)
		context['some_data'] = Model.objects.all()
		return context

	def get(self, request, **kwargs):
		""" Метод GET """
		context = self.get_context_data(**kwargs)
		return self.render_to_response(context)

	def post(self, request, **kwargs):
		""" Метод POST """
		pass
```

Обязательный параметр <u>**template_name**</u> Путь к шаблону

Метод <u>**dispatch**</u> отрабатывает до методо GET и POST и делегирет на них. На него лучше ставить логику отключения csrf_token или проверку на авторизацию юзера.

Метод <u>**get**</u> стандартный метод отрисовки страницы

Метод <u>**post**</u> стандартный метод  POST

Метод <u>**get_context_data**</u> используется для получения контекста(доп данных для шаблона)

#### Простой вариант

```python
class Contact(TemplateView):
	""" Страница контакты """
	template_name = 'contact.html'
```