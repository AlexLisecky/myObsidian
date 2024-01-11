### Основное назначение, добавление одинакого контекста к разным страницам

#### Общая структура 

```python
from django.views.generic.base import ContextMixin

class BaseContextMixin(ContextMixin):
	def get_context_data(self, **kwargs):
		context = super().get_context_data(**kwargs)
		context['some_data'] = Model.objects.all()
		return context

class Home(TemplateView, BaseContextMixin):
	def get(self, request, **kwargs):
		context = self.get_context_data(**kwargs)
		print(context['some_data'])
		return self.render_to_response(context)

class Contact(TemplateView, BaseContextMixin):
	def get(self, request, **kwargs):
		context = self.get_context_data(**kwargs)
		print(context['some_data'])
		return self.render_to_response(context)

	def get_context_data(self, **kwargs):
		context = super().get_context_data(**kwargs)
		context['other_data'] = OtherModel.objects.all()
		return context
```


При создании класса страницы добавляем к классу TemplateView BaseContextMixin и получаем по наследованию контект миксина

#### Примеры

```python
class LastViewedOfferMixin(ContextMixin):
""" Примесь добавление последних просмотренных товаров """

	def get_context_data(self, **kwargs):
		context = super().get_context_data(**kwargs)
		viewed_products = deque(self.request.session.get('viewed_products', []), maxlen=8)
		context['viewed_products'] = Offer.offers.filter(pk__in=viewed_products)
		return context
```

```python
class BusinessQuestOfferMixin(ContextMixin):
""" Примесь добавление Вопрос-Ответ и бизнесс план Линии """

	def get_context_data(self, **kwargs):
		context = super().get_context_data(**kwargs)
		context['business_quest_line'] = BusinessLine.objects.all()
		context['quest_line'] = QuestLine.objects.all()
		return context
```