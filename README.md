# Shikimori proxy

Конфигурационные файлы для [nginx], позволяющие запустить своё зеркало [shikimori](https://shikimori.one/) для обхода блокировок Роскомнадзором. [(подробнее про ситуацию с блокировками)](https://vk.com/shikimori?w=wall-9273458_512370)

## Рабочие зеркала

- [shiki.nnstd.me](https://shiki.nnstd.me)
- [shiki.anime.ovh](https://shiki.anime.ovh)

## Известные проблемы

- Не работает OAuth авторизация из-за проксирования (можно связаться с поддержкой и попросить добавления Вашего домена)
- Не работает ReCaptcha, так-же из-за проксирования (можно связаться с поддержкой и попросить добавления Вашего домена)
- Не работают некоторые XHR запросы, так-же из-за проксирования (уже связались с разработчиком, для решения данной проблемы)

## Установка
  
### Предисловие

#### Домены

Список доменов, которые будут в примере:

- `example.ru`, домен, на котором будет располагаться **главный поддомен** - `shiki.example.ru`
- `content.ru`, домен, на котором будет располагаться поддомены контента Shikimori (`moe`, `nyaa`, `desu`), можно использовать такой-же, как и в `example.ru`, чтоб не создавать себе лишних проблем.

Это сделано для тех, кто хочет разместить это на другой машине и тд.

Рекомендуется использовать [CloudFlare](https://cloudflare.com/) (во вкладке SSL / TLS выберите `Flexible`), ибо он сделает все SSL сертификаты за Вас и защитит от DDOS атак ваши сервера. :)

#### OpenResty или nginx

В Shikimori, как и на всех сайтах любят cookies, а для безопасности все хранится на своем домене, из-за чего приходиться заменять их на свои (shikimori.one -> shiki.example.ru), средств для этого нет в обычном nginx, поэтому необходимо использовать OpenResty.

### Пошаговая инструкция

Для примера используется ОС `ubuntu 20.04`, решения для других дистрибутивов приветствуются в PR.

1. Установите nginx (если его у вас нет)

```shell
sudo apt install nginx -y
```

2. Создайте DNS-записи

> Замените с помощью *(Ctrl+R)*:
> `example.ru` на свой домен, к примеру: `nnstd.me`,
> `content.ru` на свой домен, где будет прокси картинок, можно использовать тот же самый домен.
> `content\.ru` на тот-же домен, что и content.ru, только добавьте '\' перед точкой. 

За основу возьмите файл [dns.txt](dns.txt)

3. Добавьте конфиг в openresty

> Так же замените все `example.ru` и `content.ru`, как и в шаге 3

Файл [nginx.conf](nginx.conf)

4. Перезапустите Openresty

```shell
systemctl restart nginx
```

5. Всё готово, и если у вас прямые руки, то заходим на `shiki.example.ru` и наслаждаемся!

## Лицензия

Copyright (C) 2021 Artyom Mishin <themrlokopoff@gmail.com>
This work is free. You can redistribute it and/or modify it under the
terms of the Do What The Fuck You Want To Public License, Version 2,
as published by Sam Hocevar. See the `LICENSE.md` file for more details.

**Делайте всё, что хотите** :)

## Credits

- [shikimori](http://shikimori.one/) - Официальный сайт Shikimori
- [nginx](https://nginx.org/ru/) - HTTP сервер
