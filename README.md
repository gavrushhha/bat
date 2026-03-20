# Инструкция

1. Склонировать репозиторий
2. Убедитесь, что у вас есть доступ к папке-источнику (SourceFolder) и папке-назначению (DestinationFolder) для чтения/записи.
3. Настройка ``Config.ini``
   * Откройте файл: ``scripts/config/Config.ini``
   * В секции [Settings] задайте:
   * SourceFolder (локальная папка, которую мониторим), например:   ``SourceFolder=C:\Users\sofja\monitor\``
   * DestinationFolder (куда копируем), например:   ``DestinationFolder=C:\Users\sofja\Desktop\winlav\``
   * Сохраните файл.
4. Запуск скрипта
   * Откройте cmd. (терминал, командную строку)
   * Перейдите в папку проекта scripts, где лежит RunRobocopyMonitor.bat, например:   ``cd C:\путь\к\scripts``
   * Запустите:   ``RunRobocopyMonitor.bat``
5. Остановка
   * Нажмите Ctrl+C в окне консоли, где запущен скрипт.


## Скрипт:
* делает начальное зеркало через robocopy /MIR (приводит папку назначения к источнику),
* дальше постоянно мониторит изменения и раз в минуту применяет обновления через robocopy /MON:1 /MOT:1.
