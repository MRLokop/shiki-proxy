# Shikimori proxy

Прокси для shikimori, работающее поверх nginx _(openresty)_

Очень жаль, что `shikimori.one` заблокирован роскомнадзором [(Подробнее)](https://vk.com/shikimori?w=wall-9273458_512370)

Для всех кому сейчас нужен shikimori, есть небольшое решение - проксирование траффика через сервера, где он не заблокирован.


## Рабочие зеркала

* [shiki.nnstd.me](https://shiki.nnstd.me)
* [shiki.anime.ovh](https://shiki.anime.ovh)

## Установка

### Предисловие

#### Домены
Домены, которые будут в примерах:
* `example.ru`, домен на котором будет **главный поддомен** `shiki.example.ru`, на который будут заходить пользователи
* `content.ru`, домен через который будет **проксироваться контент** (`moe.`, `nyaa.` и тд), он может быть таким-же как и `example.ru`.

Это сделано для тех, кто хочет разместить это на другой машине и тд.

Рекомендую использовать [CloudFlare](https://cloudflare.com/), он сделает все сертификаты за вас.

#### Почему openresty

В шикимори, как и на всех сайтах любят печеньки, и только на своём домене (shikimori.one).

Из-за чего приходиться заменять их на свои (shiki.example.ru), средств для этого нет в обычном nginx, поэтому необходимо использовать патченую версию.

### Пошаговая инструкция

Пример для ubuntu. Для других дистрибутивов разбирайтесь сами :D

1. Отключите nginx (если есть)
```shell
sudo systemctl disable nginx
sudo systemctl stop nginx
```
2. Установка OpenResty
```shell
sudo apt-get -y install --no-install-recommends wget gnupg ca-certificates
wget -O - https://openresty.org/package/pubkey.gpg | sudo apt-key add -
echo "deb http://openresty.org/package/ubuntu $(lsb_release -sc) main"     | sudo tee /etc/apt/sources.list.d/openresty.list
sudo apt-get update
sudo apt-get -y install --no-install-recommends openresty   
```
3. Создайте DNS-записи
> ### Примечание:
> Замените *(Ctrl+R)* все `example.ru` на свой домен, к примеру: `nnstd.me`,
> 
> `content.ru` на домен, где будет прокси картинок, можно на тот же самый домен

За основу возьмите файл [dns.txt](dns.txt)

4. Добавьте конфиг в openresty
> Так же замените все `example.ru` и `content.ru`, как и в шаге 3

Файл [nginx.conf](nginx.conf)

5. Перезапустите Openresty
```shell
systemctl restart openresty
```

6. Всё готово, и если у вас прямые руки, то заходим на `shiki.example.ru` и наслаждаемся!

## Лицензия
Лицензии нет, используйте как хотите)

## Credits
[Shikimori](http://shikimori.one/) - Официальный сайт шикимори
[Openresty](https://openresty.org/en/) - для печенек