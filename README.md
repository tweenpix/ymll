# ymll

YMLL - Yandex Metrica Lazy Load (APEXWEB)
отложенная загрузка скрипта Яндекс Метрики

Яндекс Метрика начинает загружаться без задержки в случае если:

    1. Открыт адрес отличный от переменной thisSite
    2. На страницу зашел Яндекс бот

В остальных случаях загрузка скрипта Яндекс Метрики будет происходит один раз по скролу через X количество секунд указанных в переменной lazytimer
Для чего это?

Для сокращения времени загрузки сайта и увеличения показателей Google PageSpeed.

Для работы скрипта требуется подключение jquery (но это не обязательно, можете переписать на чистом JS)

--

apexweb.ru

Taras Penzin