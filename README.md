# Инструкция

1. Создайте папку ``scripts`` и склонируйте репозиторий
2. Убедитесь, что у вас есть доступ к папке-источнику (SourceFolder) и папке-назначению (DestinationFolder) для чтения/записи.
3. Настройка ``Config.ini``
   * Откройте файл: ``scripts/config/Config.ini``
   * В секции [Settings] задайте:
   * SourceFolder (локальная папка, которую мониторим), например:   ``SourceFolder=C:\Users\sofja\monitor\``
   * DestinationFolder (куда копируем), например:   ``DestinationFolder=C:\Users\sofja\Desktop\winlav\``
   * Сохраните файл.
4. Запуск скрипта
   * Откройте cmd от имени администратора (терминал, командную строку)
   * Перейдите в папку проекта scripts
   * Запустите:
     * ``sc.exe create "RobocopyMirrorService2" start= auto obj= LocalSystem binPath= "\"C:\scripts2\dist\RobocopyService\RobocopyService.exe\""``
     * ``sc.exe start "RobocopyMirrorService2"``
     * ``sc.exe query "RobocopyMirrorService2"`` - проверка статуса работы службы


## Скрипт:
* делает начальное зеркало через robocopy /MIR (приводит папку назначения к источнику),
* дальше постоянно мониторит изменения и раз в минуту применяет обновления через robocopy /MON:1 /MOT:1.
