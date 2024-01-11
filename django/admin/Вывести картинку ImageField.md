### Меняем класс

```python
from django.utils.safestring import mark_safe

class CustomAdmin(models.Admin):
	readonly_fields = ('preview', )
		
	def preview(self, obj):
		return mark_safe(f'<img src="{obj.img.url}" style="max-height: 200px;">')

preview.short_description = 'Превью картинки'
```
