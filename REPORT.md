<!--- Шаблон к оформлению домашней работы -->

## Домашнее задание




1. Скачайте библиотеку *boost* с помощью утилиты **wget**. Адрес для скачивания `https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz`.
```sh
$ wget https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
boost_1_69_0.tar.gz   100%[========================>] 106.53M  5.57MB/s    in 25s     
2025-02-28 06:33:54 (4.26 MB/s) - ‘boost_1_69_0.tar.gz’ saved [111710205/111710205]

```
2. Разархивируйте скаченный файл в директорию `~/boost_1_69_0`
```sh
$ tar -xf boost_1_69_0.tar.gz
#Ничего не выводит, просто распаковывет архив в папку с таким же названием.
```
3. Подсчитайте количество файлов в директории `~/boost_1_69_0` **не включая** вложенные директории.
```sh
$ find -maxdepth 1 -type f | wc -l
12
#find = spisok filov
#wc -l = podschet kolichestve strok(1 file = 1 stroka)
```
4. Подсчитайте количество файлов в директории `~/boost_1_69_0` **включая** вложенные директории.
```sh
$ find -type f | wc -l
61191
```
5. Подсчитайте количество заголовочных файлов, файлов с расширением `.cpp`, сколько остальных файлов (не заголовочных и не `.cpp`).
```sh
$ find -type f -name "*.hpp" -o -name "*.h" | wc -l
15208
$ find -type f -name "*.cpp" | wc -l
13774
$ find -type f -not -name "*.hpp" -a -not  -name "*.h"-a -not  -name "*.cpp"  | wc -l
32505
```
6. Найдите полный путь до файла `any.hpp` внутри библиотеки *boost*.
```sh
$ find -type f -name "any.hpp"
./boost/xpressive/detail/utility/any.hpp
./boost/fusion/algorithm/query/any.hpp
./boost/fusion/algorithm/query/detail/any.hpp
./boost/fusion/include/any.hpp
./boost/spirit/home/support/algorithm/any.hpp
./boost/proto/detail/any.hpp
./boost/any.hpp
./boost/type_erasure/any.hpp
./boost/hana/any.hpp
./boost/hana/fwd/any.hpp
$ readlink -f boost/any.hpp
/home/bibs/EhEhEhEh-labs/workspace/workspace/reports/lab01/boost_1_69_0/boost/any.hpp
```
7. Выведите в консоль все файлы, где упоминается последовательность `boost::asio`.
```sh
$ grep -r "boost::asio" > containsboostasio.txt
V file containsboostasio.txt, toje na gist-e.
```
[containsboostasio.txt](https://gist.github.com/EhEhEhEh-labs/24e91eeb981f4ac8385c20d5e9f566f0#file-containsboostasio-txt/)

8. Скомпилирутйе *boost*. Можно воспользоваться [инструкцией](https://www.boost.org/doc/libs/1_61_0/more/getting_started/unix-variants.html#or-build-custom-binaries) или [ссылкой](https://codeyarns.com/2017/01/24/how-to-build-boost-on-linux/).
```sh
$ ./bootstrap.sh
Bootstrapping is done. To build, run:

    ./b2

```
9. Перенесите все скомпилированные на предыдущем шаге статические библиотеки в директорию `~/boost-libs`.
```sh
$ mkdir ./boost-libs
$ cp ./stage/lib/*a ./boost-libs/
$ cd boost-libs | ls
libboost_atomic.a     libboost_context.a   libboost_date_time.a  libboost_filesystem.a
libboost_container.a  libboost_contract.a  libboost_fiber.a	 libboost_wave.a
```
10. Подсчитайте сколько занимает дискового пространства каждый файл в этой директории.
```sh
$ du -h ./*
4.0K	./libboost_atomic.a
148K	./libboost_container.a
20K	./libboost_context.a
336K	./libboost_contract.a
152K	./libboost_date_time.a
232K	./libboost_fiber.a
400K	./libboost_filesystem.a
4.5M	./libboost_wave.a

```
11. Найдите *топ10* самых "тяжёлых".
```sh
$ du -h ./* | sort -hr
4.5M	./libboost_wave.a
400K	./libboost_filesystem.a
336K	./libboost_contract.a
232K	./libboost_fiber.a
152K	./libboost_date_time.a
148K	./libboost_container.a
20K	./libboost_context.a
4.0K	./libboost_atomic.a
```
