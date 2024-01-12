
1. Подключаем jQuery и плагин jQuery Validation
2. Создаем форму в HTML
3.  Пишем JS

#### Подключение библиотек 

```js
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.19.3/jquery.validate.min.js"></script>
```
***

#### Создание формы

```html
{% csrf_token %}
<form id="myForm" method="post">
	<label for="name">Ваше имя</label>
	<input type="text" id="name" name="name" required autocomplete="off">
	
	<label for="email">Email</label>
	<input type="email" id="email" name="email" required autocomplete="off">
	
	<label for="message">Message</label>
	<textarea id="message" name="message" required></textarea>
	
	<button type="submit" id="submitBtn">Submit</button>
</form>
```
***

### Пример JS

##### Документация валидаторов 
<https://jqueryvalidation.org/documentation/>

```js
$(document).ready(function() {
	$("#myForm").validate({
		// правила валидации, в rules пишем name от input
		// пример: name='phone', пишем phone:'required'
		rules: {
			name: "required", // обязательность заполнения поля
			email: {
				required: true, // обязательность заполнения поля
				email: true // проверка REGEX на почту
			},
			message: {
				required: true, // обязательность заполнения поля
				minlenght: 3, // минимальное количество символов
				maxlength: 200, // максимальное количество символов
			} 
		},
		// Отправка сообщений при провале валидации
		// Заменяется текст в label на ниже указанной при определенных проверках
		// так же добавляет class='error' к label и input так что
		// стилизуем как нам надо
		messages: {
			name: "Общий текст ошибки",
			email: {
				required: "Текст ошибки при провале обязательности заполнения",
				email: "Текст ошибки при провале валидации email(REGEX)"
			},
			message: {
				required: "Текст ошибки при провале обязательности заполнения",
				minlenght: "Минимальное количество символов 3",
				maxlength: "Максимальное количество символов 200",
			} 
		},
		// Что делать при нажатии на кнопку submit формы после валидации
		submitHandler: function(form) {
			let data = {};
			// csrf указан для примера здесь, лучше вынести вне функцию на
			// глобальный уровень
			let csrftoken = $('input[name=csrfmiddlewaretoken]').val();

			// добавляем все инпуты по ключ: значению
			$(form).find('input, textarea').each(function() {
				data[this.name] = $(this).val();
			});
			
			$.ajax({
				url: "/api/send_form",
				type: "POST",
				data: data,
				headers: {
					'X-CSRFToken': csrftoken,
				},
				success: function(response) {
					// Что то делаем при успехе
					alert("Form submitted successfully!");
					// Обнуляем форму
					$(form)[0].reset();
				},
				error: function(jqXHR, textStatus, errorThrown) {
					// Что то делаем при ошибке
					alert("Error submitting form: " + errorThrown);
				}
			});
		}
	});
});
```

#### Короткий пример

```js
let validate_rules = {
	rules: {
		user_name: { required: true },
		user_tel: { required: true }
	},
	messages: {
		user_name: { required: '<span>' + icon_error + 'Необходимо ввести имя</span>' },
		user_tel: { required: '<span>' + icon_error + 'Необходимо ввести номер телефона</span>' }
	},
};

$('#qform').validate(validate_rules);
$('#anotherform').validate(validate_rules);
```