Статическая сборка на основе Qt 15.5.1 MinGWx64 в Windows 10

### 1. Запускаем qt-unified-windows-x86-4.2.0-online.exe 

- он имеется в архиве или скачать последнюю версию с сайта qt https://download.qt.io/official_releases/online_installers/qt-unified-windows-x86-online.exe

Qt устанавливать нужно на диск C
(1,2,3 скриншот)
- Установить Qt 15.5.1 MinGW 8.1.0 32-bit
- Установить Qt 15.5.1 MinGW 8.1.0 64-bit
- Установить Qt Creator 6.0.1 MinGW 8.1.0 32-bit
- Установить Qt Creator 6.0.1 MinGW 8.1.0 64-bit
- Установить Qt Creator 6.0.1 CMake 3.21.1 64-bit

### 2. Запускаем установшики Python Perl Ruby (64 битные версии)
- они имееются в архиве или скачать последнюю версию с сайтов производителей
- Python https://www.python.org/downloads/
- Perl https://strawberryperl.com/
- Ruby https://rubyinstaller.org/downloads/ (WITHOUT DEVKIT)


Дальше нужно установить(Устанавливать нужно на диск C):
- Python последней версии 64 битную
- Perl последней версии 64 битную
- Ruby последней версии 64 битную

### 3. Добавляем пути к программам и библиотекам в параметры системы:
- Поиск->Система->Дополнительные параметры системы->Параметры среды->Системные переменные->Path->Изменить

Создаём пути (скриншот 4)

### 4. Далее скачиваем исходник QT 15.5.1 или копируем его из архива qt-everywhere-src-5.15.1.zip
-он есть в архиве или или скачать с сайта qt https://download.qt.io/official_releases/qt/5.15/5.15.1/single/qt-everywhere-src-5.15.1.zip

Разархивируйте его в папку Qt , для удобства создайте папку Src или разархивируйте туда , должно получиться вот так после разахивирования(C:\Qt\Src\qt-everywhere-src-5.15.1\)

### 5. Запускаем cmd и переходим в папку 
- C:\Qt\Src\qt-everywhere-src-5.15.1\
Команды для командной строки:

C:\Users\Cereg>cd..

C:\Users>cd..

C:\>cd Qt

C:\Qt>cd Src

C:\Qt\Src>cd qt-everywhere-src-5.15

C:\Qt\Src\qt-everywhere-src-5.15.1>

В Командную строку вставляем это команду:
configure -static -debug-and-release -platform win32-g++ -qt-zlib -qt-pcre -qt-libpng -qt-libjpeg -qt-freetype -opengl desktop -no-angle -no-openssl -opensource -confirm-license -make libs -nomake tools -nomake examples -nomake tests -prefix C:\Qt\5.15.1\mingw81_64_static

После завершения проверки вставляем это команду:
mingw32-make -k -j16 
(16 это количество ядер на компьютере)

После завершения вставляем это команду:
mingw32-make -k install

ВЫПОЛНЕНИЕ МОЖЕТ ПРОХОДИТЬ ОЧЕНЬ ДОЛГО (4-6 ЧАСОВ), ВСЕ ЗАВИСИТ ОН МОЩНОСТЬИ ВАЩЕГО КОМПЬЮТЕРА , И ОТ КОЛИЧЕСТВА БИБЛИОТЕК КОТОРЫЕ ВАМ НУЖНЫ

### 6. После завершения процедуры переходим в Qt Creator и запускаем какой-то проект
Переходим в Проекты->Управление->Профили Qt->Добавить
Добавляем qmake.exe и для удобства называем Qt  (5.15.1) static (скриншот 5)

ЕСЛИ НЕ ХВАТАЕТ КАКОЙ-ТО БИБЛИОТЕКИ ИЛИ ФАЙЛА (ЭТО БУДЕТ НАПИСАНО ПОД qmake path), ТО ПЕРЕХОДИМ C:\Qt\5.15.1\mingw81_64\bin И КОПИРУЕМ НЕОБХОДИМЫЕ ФАЙЛЫ(ФАЙЛЫ С ОДИНАКОВЫМ НАЗВАНИЕМ) В C:\Qt\5.15.1\mingw81_64_static\bin (БЕЗ ЗАМЕНЫ)

Переходим в Проекты->Управление->Комплекты->Добавить
Добавляем новую сборку (скриншот 6)

Переходим в Проекты, и добавляем сборку в проект , нажать на зеленый плюсик (скриншот 7)

Переходим в .pro файл и добавляем строку QMAKE_LFLAGS_RELEASE += -static -static-libgcc

И собираем проект для релиза

### 7. ЕСЛИ ВЫЛЕТАЮТ ОШИБКИ cannot found -ltiff,cannot found -lwebp:

Нужно в папку (C:\Qt\Tools\) добавить библиотеки (они находятся в архиве, разархивируйте их туда и переменуйте папки в lift и libwebp)
И добавляем пути в систему, как в пункте 3 (скриншот 8)
Повторяем 5 пукнт и добавляем в команду -qt-tiff -qt-webp, полная команду будет выглядить так:
configure -static -debug-and-release -platform win32-g++ -qt-zlib -qt-pcre -qt-libpng -qt-tiff -qt-webp -qt-libjpeg -qt-freetype -opengl desktop -no-angle -no-openssl -opensource -confirm-license -make libs -nomake tools -nomake examples -nomake tests -prefix C:\Qt\5.15.1\mingw81_64_static
и заново создаем сборщик, как в пункте 5

НО ЕСТЬ ГОТОВЫЙ СКОМПИЛИРОВАННЫЙ mingw81_64_static.rar

https://doc.qt.io/qt-5/configure-options.html
