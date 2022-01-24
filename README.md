# ymll

YMLL - Yandex Metrica Lazy Load
отложенная загрузка скрипта Яндекс Метрики

Яндекс Метрика начинает загружаться без задержки в случае если:

    1. Открыт адрес отличный от переменной thisSite
    2. На страницу зашел Яндекс бот

В остальных случаях загрузка скрипта Яндекс Метрики будет происходит один раз по скролу или через X количество секунд указанных в переменной lazytimer
Для чего это?

Для сокращения времени загрузки сайта и увеличения показателей Google PageSpeed.

Для работы скрипта требуется подключение jquery (но это не обязательно, можете переписать на чистом JS)
Сам код:
//begin APEXWEB Yandex Metrica lazy load

jQuery(document).ready(function () {
let thisSite = "https://example.ru/"; // адрес сайта
let ymid = 07254000; // id счетчика Яндекс Метрики
let lazytimer = 3; // задержка загрузки скрипта на 3 секунды

console.log("YMLL: Готов к работе");

//функция загрузки скриптов
jQuery.cachedScript = function (url, options) {
options = $.extend(options || {}, {
dataType: "script",
cache: true,
url: url,
});
return jQuery.ajax(options);
};

function ym_load() {
//YMLL - Yandex Metrica Lazy Load
//
//скрипт отложенной загрузки скрипта Яндекс Метрики
//Яндекс Метрика начинает загружаться без задержки в случае если:
//1. Открыт адрес отличный от переменной thisSite
//2. На страницу зашел Яндекс бот
//В остальных случаях загрузка скрипта Яндекс Метрики будет происходит один раз по скролу или
//через X количество секунд указанных в переменной lazytimer

$.cachedScript("https://mc.yandex.ru/metrika/tag.js").done(function (
script,
textStatus
) {
(function (m, e, t, r, i, k, a) {
m[i] =
m[i] ||
function () {
(m[i].a = m[i].a || []).push(arguments);
};
m[i].l = 1 * new Date();
(k = e.createElement(t)),
(a = e.getElementsByTagName(t)[0]),
(k.async = 1),
(k.src = r),
a.parentNode.insertBefore(k, a);
})(
window,
document,
"script",
"https://mc.yandex.ru/metrika/tag.js",
"ym"
);

ym(ymid, "init", {
clickmap: true,
trackLinks: true,
accurateTrackBounce: true,
webvisor: true,
ecommerce: "dataLayer",
});
});
console.log("YMLL: Яндекс Метрика загружена");
}

if (
navigator.userAgent.indexOf("YandexBot") > -1 ||
navigator.userAgent.indexOf("YandexMetrika") > -1
) {
ym_load();
} else if (location.href == thisSite) {
$(window).one("scroll", function (event) {
console.log("YMLL: Яндекс Метрика загружается");
window.setTimeout(function () {
ym_load();
}, lazytimer * 1000);
});
} else {
console.log("YMLL: Яндекс Метрика загружается");
ym_load();
}
});
//end APEXWEB Yandex Metrica lazy load
