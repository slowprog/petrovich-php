![Petrovich](https://raw.github.com/rocsci/petrovich/master/petrovich.png)

Склонение падежей русских имён, фамилий и отчеств. Портированная версия с [Ruby](https://github.com/petrovich/petrovich-ruby) на PHP.

Лицензия MIT.

## Установка

```json
{
    "require":{
        "slowprog/petrovich-php": "^1.0"
    }
}
```

## Обновление правил

Если в [основные правила](https://github.com/petrovich/petrovich-php) были внесены изменения, то сюда их придётся подтянуть вручную:

```bash
git clone https://github.com/petrovich/petrovich-php.git rules
```

После этого удалить внутри *.git* и *.travis*.

### Использование класса

```php
require __DIR__.'./vendor/autoload.php';

$petrovich = new Petrovich(Petrovich::GENDER_MALE);

$firstname = "Александр";
$middlename = "Сергеевич";
$lastname = "Пушкин";

echo $petrovich->detectGender("Петровна");	// Petrovich::GENDER_FEMALE (см. пункт Пол)

echo '<br /><strong>Родительный падеж:</strong><br />';
echo $petrovich->firstname($firstname, Petrovich::CASE_GENITIVE).'<br />'; //	Александра
echo $petrovich->middlename($middlename, Petrovich::CASE_GENITIVE).'<br />'; //	Сергеевича
echo $petrovich->lastname($lastname, Petrovich::CASE_GENITIVE).'<br />'; //		Пушкина
```

## Падежи

Названия суффиксов для методов образованы от английских названий соответствующих падежей. Полный список поддерживаемых падежей приведён в таблице ниже.

| Суффикс метода | Падеж        | Характеризующий вопрос |
|----------------|--------------|------------------------|
| CASE_NOMENATIVE| именительный | Кто? Что?            |
| CASE_GENITIVE  | родительный  | Кого? Чего?            |
| CASE_DATIVE    | дательный    | Кому? Чему?            |
| CASE_ACCUSATIVE| винительный  | Кого? Что?             |
| CASE_INSTRUMENTAL   | творительный | Кем? Чем?              |
| CASE_PREPOSITIONAL  | предложный   | О ком? О чём?          |

## Пол
Метод ```Petrovich::detectGender``` возвращает пол, на основе отчества. Возвращаемое значение не зависит от пола, переданного в конструктор.
Для полов определены следующие константы
* GENDER_ANDROGYNOUS - пол не определен;
* GENDER_MALE - мужской пол;
* GENDER_FEMALE - женский пол.
