# Статическая сборка на основе Qt 5.15.1 MinGWx64 в Windows 10

### 1. Запускаем _qt-unified-windows-x86-4.2.0-online.exe_

- [Cкачать с сайта Qt](https://download.qt.io/official_releases/online_installers/qt-unified-windows-x86-online.exe)

Qt устанавливать нужно на диск C
- Установить _Qt 5.15.1 MinGW 8.1.0 32-bit_
- Установить _Qt 5.15.1 MinGW 8.1.0 64-bit_
- Установить _Qt Creator 6.0.1 MinGW 8.1.0 32-bit_
- Установить _Qt Creator 6.0.1 MinGW 8.1.0 64-bit_
- Установить _Qt Creator 6.0.1 CMake 3.21.1 64-bit_
![1](https://github.com/CEREGATOR/qtcreator_static_build/blob/main/1.PNG)
![2](https://github.com/CEREGATOR/qtcreator_static_build/blob/main/2.PNG)
![3](https://github.com/CEREGATOR/qtcreator_static_build/blob/main/3.PNG)

### 2. Запускаем установшики Python, Perl, Ruby (64 битные версии)

Cкачать последнюю версию с сайтов производителей:
- [Python x64](https://www.python.org/downloads/)
- [Perl x64](https://strawberryperl.com/)
- [Ruby x64 (WITHOUT DEVKIT)](https://rubyinstaller.org/downloads/)

Дальше нужно установить(Устанавливать нужно на диск C):
- _Python_
- _Perl_
- _Ruby_

### 3. Добавляем пути к программам и библиотекам в параметры системы:

_Поиск:arrow_right:Система:arrow_right:Дополнительные параметры системы:arrow_right:Параметры среды:arrow_right:Системные переменные:arrow_right:Path:arrow_right:Изменить_

- Создаём пути

![4](https://github.com/CEREGATOR/qtcreator_static_build/blob/main/4.PNG)

### 4. Далее скачиваем исходник QT 5.15.1
- [Cкачать с сайта Qt](https://download.qt.io/official_releases/qt/5.15/5.15.1/single/qt-everywhere-src-5.15.1.zip)

Разархивируйте его в папку Qt, для удобства создайте папку Src и разархивируйте туда 
- Должно получиться вот так, после разахивирования

```C:\Qt\Src\qt-everywhere-src-5.15.1\```

### 5. Запускаем cmd и переходим в папку

```C:\Qt\Src\qt-everywhere-src-5.15.1\```

- Команды для командной строки:

```
C:\Users\Cereg>cd..
C:\Users>cd..
C:\>cd Qt
C:\Qt>cd Src
C:\Qt\Src>cd qt-everywhere-src-5.15.1
C:\Qt\Src\qt-everywhere-src-5.15.1>
```

- В Командную строку вставляем это команду:

```configure -static -debug-and-release -platform win32-g++ -qt-zlib -qt-pcre -qt-libpng -qt-libjpeg -qt-freetype -opengl desktop -no-angle -no-openssl -opensource -confirm-license -make libs -nomake tools -nomake examples -nomake tests -prefix C:\Qt\5.15.1\mingw81_64_static```

- После завершения проверки вставляем это команду:

```mingw32-make -k -j16```
(16 это количество ядер на компьютере)

- После завершения вставляем это команду:

```mingw32-make -k install```

___ВЫПОЛНЕНИЕ МОЖЕТ ПРОХОДИТЬ ОЧЕНЬ ДОЛГО (4-6 ЧАСОВ), ВСЕ ЗАВИСИТ ОН МОЩНОСТЬИ ВАЩЕГО КОМПЬЮТЕРА , И ОТ КОЛИЧЕСТВА БИБЛИОТЕК КОТОРЫЕ ВАМ НУЖНЫ___

### 6. После завершения процедуры переходим в Qt Creator и запускаем какой-то проект
- Переходим в:

_Проекты:arrow_right:Управление:arrow_right:Профили Qt:arrow_right:Добавить_

- Добавляем qmake.exe и для удобства называем ```Qt (5.15.1) static```
 
![5](https://github.com/CEREGATOR/qtcreator_static_build/blob/main/5.PNG)

____
### ___ЕСЛИ НЕ ХВАТАЕТ КАКОЙ-ТО БИБЛИОТЕКИ ИЛИ ФАЙЛА (ЭТО БУДЕТ НАПИСАНО ПОД qmake path), ТО ПЕРЕХОДИМ В___
```C:\Qt\5.15.1\mingw81_64\bin```

### ___И КОПИРУЕМ НЕОБХОДИМЫЕ ФАЙЛЫ(ФАЙЛЫ С ОДИНАКОВЫМ НАЗВАНИЕМ) В___
```C:\Qt\5.15.1\mingw81_64_static\bin```___(БЕЗ ЗАМЕНЫ)___
____

- Переходим в:

_Проекты:arrow_right:Управление:arrow_right:Комплекты:arrow_right:Добавить_

- Добавляем новую сборку

![6](https://github.com/CEREGATOR/qtcreator_static_build/blob/main/6.PNG)

- Переходим в Проекты, и добавляем сборку в проект, нажать на зеленый плюсик 

![7](https://github.com/CEREGATOR/qtcreator_static_build/blob/main/7.PNG)

- Переходим в .pro файл и добавляем строку 

```QMAKE_LFLAGS_RELEASE += -static -static-libgcc```

- И собираем проект для релиза

# ЕСЛИ ВЫЛЕТАЮТ ОШИБКИ: _cannot found -ltiff, cannot found -lwebp_
Можно взять библиотеку tiff из этого репозитория или [скачать](http://gnuwin32.sourceforge.net/downlinks/tiff-bin-zip.php)

Можно взять библиотеку webp из этого репозитория или [скачать](https://storage.googleapis.com/downloads.webmproject.org/releases/webp/libwebp-1.2.2-rc2-windows-x64.zip)

- Нужно в папку ```C:\Qt\Tools\``` добавить библиотеки
- Разархивируйте их в папку ```C:\Qt\Tools\``` и переменуйте папки в ```lift``` и ```libwebp```
- И добавляем пути в систему, как в [пункте 3](https://github.com/CEREGATOR/qtcreator_static_build#3-добавляем-пути-к-программам-и-библиотекам-в-параметры-системы)

![8](https://github.com/CEREGATOR/qtcreator_static_build/blob/main/8.PNG)

- [Повторяем 5 пукнт](https://github.com/CEREGATOR/qtcreator_static_build#5-запускаем-cmd-и-переходим-в-папку) и добавляем в команду ```-qt-tiff -qt-webp```, полная команду будет выглядить так:

```configure -static -debug-and-release -platform win32-g++ -qt-zlib -qt-pcre -qt-libpng -qt-tiff -qt-webp -qt-libjpeg -qt-freetype -opengl desktop -no-angle -no-openssl -opensource -confirm-license -make libs -nomake tools -nomake examples -nomake tests -prefix C:\Qt\5.15.1\mingw81_64_static```
- И заново создаем сборщик, как в [пункте 5](https://github.com/CEREGATOR/qtcreator_static_build#5-запускаем-cmd-и-переходим-в-папку)

# НО ЕСТЬ ГОТОВЫЙ СКОМПИЛИРОВАННЫЙ [mingw81_64_static.rar](https://github.com/CEREGATOR/qtcreator_static_build/releases/download/mingw81_64_static/mingw81_64_static.rar)

### 7. [Документация QT](https://doc.qt.io/qt-5/configure-options.html)
