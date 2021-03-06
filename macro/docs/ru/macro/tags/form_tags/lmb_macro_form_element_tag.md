# lmbMacroFormElementTag
## Описание
Родительский класс для всех элементов формы для ввода данных, таких как тег [{{input}}](./input_tag.md), тег [{{textarea}}](./text_area_tag.md) и т.д.

## Область применения
В любом месте MACRO-шаблона, но обычно внутри тега [{{form}}](./form_tag.md).

## Атрибуты

* **id** — идентификатор тега
* **name** — название тега (равняется **id**, если не указано)
* **error_class** — указывает класс стиля, который будет применен к полю, если оно не прошло валидацию.
* **error_style** — указывает стиль, который будет применен к полю, если оно не прошло валидацию. Стиль задается набором CSS-свойств.
* **title** — указывает читабельное название поля. Используется при выводе ошибок валидации.
* **value** — позволяет указать на значение, которые должен иметь тег при отображении. Для <input> тегов — это атрибут value. Для <select> - выбранное значение(-я). Если данный атрибут не используется, тогда элементы форм пытаются брать данные из контейнера данных родительского тега **{{form}}**, в котором они находятся.

А также любые другие атрибуты, которые соответствуют аналогичному html-тегу.

## Краткое для чего нужны title, error_style, error_class
Предположим, что у нас есть вот такой шаблон:

    {{form name="my_form"}}
 
    {{form:errors to="$form_errors"/}}
    {{list using="$form_errors" as="$item"}}{{list:item}}{$item.message}<br/>{{/list:item}}{{/list}}
 
    {{label for="text_field" error_style="color:red; font-weight:bold"}}My text{{/label}}
    {{input type="text" name="text_field" title="My text field" error_class="class_of_error"/}}
 
    {{label for="select_field" error_class="class_of_error"}}My select{{/label}}
    {{select name="select_field" title="My select field" error_style="color:red; font-weight:bold"/}}
 
    {{/form}}

Пусть у нас где-то есть php-скрипт, который используется этот шаблон:

    $error_list = new lmbMacroFormErrorList();
    $error_list->addError('Error in {field}', array('field' => 'text_field'));
    $error_list->addError('Other error in {field}', array('field' => 'select_field'));
 
    $page = new lmbMacroTemplate('tpl.html'); 
    $page->set('form_my_form_error_list', $error_list); 
 
    $page->render();

На выходе получим:

    <form name="my_form">Error in My text field<br/>Other error in My select field<br/>
 
    <label for="text_field" style="color:red; font-weight:bold">My text</label>
    <input type="text" name="text_field" title="My text field" class="class_of_error" value="" />
 
    <label for="select_field" class="class_of_error">My select</label>
    <select name="select_field" title="My select field" style="color:red; font-weight:bold"></select>
 
    </form>;
