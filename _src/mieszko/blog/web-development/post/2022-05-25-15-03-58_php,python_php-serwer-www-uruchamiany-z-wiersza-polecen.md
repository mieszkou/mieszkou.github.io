<!--t PHP: serwer WWW uruchamiany z wiersza poleceń t-->
<!--d Jak szybko uruchomić serwer WWW z wiersza poleceń? Jest na to kilka sposobów: - PHP ``` php -S 127.0.0.1:8080 -t ./www ``` - python ``` # python d-->
<!--tag php,python tag-->

Jak szybko uruchomić serwer WWW z wiersza poleceń? Jest na to kilka sposobów:

- PHP
```
php -S 127.0.0.1:8080 -t ./www
```
- python
```
# python 3.x
python -m http.server 8080
# python 2.X
python -m SimpleHTTPServer 8080
```