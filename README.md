![Petrovich](https://raw.github.com/rocsci/petrovich/master/petrovich.png)

Склонение падежей русских имён, фамилий и отчеств. Портированная версия с [Ruby](https://github.com/petrovich/petrovich-ruby) на PHP плюс некоторый дополнительный функционал.

Лицензия MIT.

## Установка

```json
{
    "require":{
        "slowprog/petrovich-php": "^1.0"
    }
}
```

## Использование класса

```php
require __DIR__.'./vendor/autoload.php';

$petrovich = new Petrovich();

$firstname  = "Александр";
$middlename = "Сергеевич";
$lastname   = "Пушкин";
$fullName   = 'Васильков Генадий Павлович';

echo $petrovich->detectGender("Петровна"); // Petrovich::GENDER_FEMALE (см. пункт Пол)

echo $petrovich->firstname($firstname, Petrovich::CASE_GENITIVE, Petrovich::GENDER_MALE); // Александра

echo $petrovich->middlename($middlename, Petrovich::CASE_GENITIVE, Petrovich::GENDER_MALE); // Сергеевича

echo $petrovich->lastname($lastname, Petrovich::CASE_GENITIVE, Petrovich::GENDER_MALE); // Пушкина

echo $mihalich->initial($fullName); // Васильков Г. П.

echo $mihalich->inflectFullName($fullName, Petrovich::CASE_GENITIVE); // Василькова Генадия Павловича

echo $mihalich->initial(
    $mihalich->inflectFullName(
        $fullName, 
        Petrovich::CASE_GENITIVE
    )
); // Василькова Г. П.
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

## Обновление правил

Если в [основные правила](https://github.com/petrovich/petrovich-php) были внесены изменения, то сюда их придётся подтянуть вручную:

```bash
git clone https://github.com/petrovich/petrovich-php.git rules
```

После этого удалить внутри *.git* и *.travis*.
