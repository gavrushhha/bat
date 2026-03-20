# Инструкция

## Через клонирование репозитория:
1. Создайте папку ``scripts`` и склонируйте репозиторий.
2. Убедитесь, что у вас есть доступ к папке-источнику (SourceFolder) и папке-назначению (DestinationFolder) для чтения/записи.
3. Настройка ``Config.ini``.
   * Откройте файл: ``scripts/config/Config.ini``
   * В секции [Settings] задайте:
   * SourceFolder (локальная папка, которую мониторим), например:   ``SourceFolder=C:\Users\sofja\monitor\``
   * DestinationFolder (куда копируем), например:   ``DestinationFolder=C:\Users\sofja\Desktop\winlav\``
   * Сохраните файл.
<img width="830" height="348" alt="image" src="https://github.com/user-attachments/assets/d8e49c28-6da8-4f7a-a62f-1602b5094a31" />

Если `DestinationFolder` указывает на сетевую шару `\\server\share\...` и доступ нужен по логину/паролю:
   - укажите в [Settings]:
     - `Username=DOMAIN\username`
     - `Password=пароль`
   - важное уточнение: `RobocopyMonitor` запускается как служба и сам “не мапит” сетевой диск.
     Поэтому для корректной работы у процесса службы должны быть права на `\\server\share\...`.
     Самый простой способ — запускать службу под той же учеткой, что и `Username`.
     Альтернатива — перед запуском службы выполнить команду `net use` (замените `\\server\share` и учетные данные):
       `net use \\server\share /user:DOMAIN\username пароль /persistent:no`

4. Запуск скрипта.
   * Откройте cmd от имени администратора (терминал, командную строку).
   * Перейдите в папку проекта ``scripts`` - cd /путь/до/scripts
   * Запустите:
     * ``sc.exe create "RobocopyMirrorService2" start= auto obj= LocalSystem binPath= "\"C:\scripts2\dist\RobocopyService\RobocopyService.exe\""``
     * ``sc.exe start "RobocopyMirrorService2"``
     * ``sc.exe query "RobocopyMirrorService2"`` - проверка статуса работы службы
<img width="965" height="464" alt="image" src="https://github.com/user-attachments/assets/0acfdd6f-7c17-499e-b74d-0c379748ee90" />



## Через скачивание ZIP:
1. Скачайте ZIP проекта.
<img width="912" height="646" alt="image" src="https://github.com/user-attachments/assets/ae29dc66-46e2-4539-bc11-76ba3fff6623" />

2. Распакуйте проект у себя на компьютере в папку ``scripts``, перед этим создав ее. (на фото правильное строение)
<img width="793" height="599" alt="image" src="https://github.com/user-attachments/assets/d16b464c-cb6e-4a42-b571-201711f4547b" />

3. Убедитесь, что у вас есть доступ к папке-источнику (SourceFolder) и папке-назначению (DestinationFolder) для чтения/записи.
4. Настройка ``Config.ini``.
   * Откройте файл: ``scripts/config/Config.ini``
   * В секции [Settings] задайте:
   * SourceFolder (локальная папка, которую мониторим), например:   ``SourceFolder=C:\Users\sofja\monitor\``
   * DestinationFolder (куда копируем), например:   ``DestinationFolder=C:\Users\sofja\Desktop\winlav\``
   * Сохраните файл.
  Если `DestinationFolder` указывает на сетевую шару `\\server\share\...` и доступ нужен по логину/паролю:
   - укажите в [Settings]:
     - `Username=DOMAIN\username`
     - `Password=пароль`
   - важное уточнение: `RobocopyMonitor` запускается как служба и сам “не мапит” сетевой диск.
     Поэтому для корректной работы у процесса службы должны быть права на `\\server\share\...`.
     Самый простой способ — запускать службу под той же учеткой, что и `Username`.
     Альтернатива — перед запуском службы выполнить команду `net use` (замените `\\server\share` и учетные данные):
       `net use \\server\share /user:DOMAIN\username пароль /persistent:no`
5. Запуск скрипта.
   * Откройте cmd от имени администратора (терминал, командную строку).
   * Перейдите в папку проекта scripts.
   * Запустите:
     * ``sc.exe create "RobocopyMirrorService2" start= auto obj= LocalSystem binPath= "\"C:\scripts2\dist\RobocopyService\RobocopyService.exe\""``
     * ``sc.exe start "RobocopyMirrorService2"``
     * ``sc.exe query "RobocopyMirrorService2"`` - проверка статуса работы службы


## Скрипт:
* делает начальное зеркало через robocopy /MIR (приводит папку назначения к источнику),
* дальше постоянно мониторит изменения и раз в минуту применяет обновления через robocopy /MON:1 /MOT:1.
