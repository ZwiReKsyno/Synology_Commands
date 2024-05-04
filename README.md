# SYNOLOGY basic commands




#### Будьте осторожны: некоторые команды могут стереть ДАННЫЕ, поэтому читайте внимательно.


# Шпаргалка

#### Рабочая группа печати для NAS:

     synowin -getWorkgroup
     
#### Присоединяйтесь к новой рабочей группе NAS:

     synowin -joinWorkgroup <group>

#### Распечатать общую информацию:

      synoservice --status

#### Настройка почты через cli:

      synosyslogmail

#### Проверьте обновления:

      synoupgrade --check 3

#### Дамп данных о вашем NAS:

     syno_system_dump

#### Распечатать информацию о сети, вкл. текущий дуплекс:

     synonet --show
     
#### Распечатать текущее имя хоста:

     synonet --get_hostname
     
#### Установите новое имя хоста:

    synonet --set_hostname
     
#### Установите новый шлюз:

    synonet --set_gateway gateway
    
#### WOL Пробуждение:

    synonet --wake xx:xx:xx:xx:xx:xx <interface>

#### Распечатайте таблицу расположения разделов.

    synopartition --list
    
## Совместное использование

##### Распечатать информацию об акции:

    synoshare --get <sharefolder>

##### Подключите общую зашифрованную папку:

    synoshare --enc_mount <sharefolder> <password>

##### Размонтируйте зашифрованную папку:

    synoshare --enc_unmount <sharefolder>

##### Разрешено удалить:

    synoshare --del {TRUE|FALSE} sharename1 sharename2 ... 
    
##### Задайте описание для общей папки (просматривается в комментариях в файловом браузере)

    synoshare --setdesc sharename desc

###### Разрешить просмотр общей папки

    synoshare --setbrowse sharename browse_flag{0|1} 
    
##### Переименуйте общую папку:

    synoshare --rename  old_sharename new_sharename
    
##### Установите пользователей, которым разрешено просматривать общую папку:

    synoshare --setuser sharename user_auth{NA|RO|RW} operator{+|-|=} user_name_list_with_comma

### Пользователь
####  Распечатать основные данные о пользователе

    sh-4.3# synouser --get wuseman
    User Name   : [wuseman]
    User Type   : [AUTH_LOCAL]
    User uid    : [1026]
    Primary gid : [100]
    Fullname    : []
    User Dir    : [/var/services/homes/wuseman]
    User Shell  : [/bin/sh]
    Expired     : [false]
    User Mail   : []
    Alloc Size  : [82]
    Member Of   : [2]
    (100) users
    (101) administrators
    
#### Установить новый пароль/Изменить пароль:

    synouser --setpw oldpassword newpassword

#### Переименуйте пользователя:

    synouser --rename old_username new_username
    
#### Добавьте имя пользователя с полной информацией:

    synouser --add [username pwd "full name" expired{0|1} mail privilege]

## Уведомления:
    
### Отправьте электронное письмо о хранилище: 

    synostorage --mail
  
#### Управление блокировкой

    synostorage --lock

## Настройка функционала:
  
##### Получить текущий профиль настройки:

    synotune --get   
    Outut: Current Profile: performance_throughput
    
#### Установить новый функционал, параметры:

    synotune --set    performance_throughput OR performance_latency
    
#### Сохраните информацию о вашем Synology Nas:

    syno_system_dump
    
## Обновление

##### Настройте вашу систему на автоматическую обработку обновлений:

    synoupgrade --auto
    
##### Проверьте текущие настройки обновления:

    synoupgrade --check

##### Загрузите последнее обновление, если есть новое:

    synoupgrade --download 
   
##### Начать обновление:

    synoupgrade --start
    
#### Проверьте таблицу расположения разделов:

    synopartition --check /dev/sd<X>
 
#### Просмотр монитора Synology NFS:

   synonfstop
     
#### Сброс Synology NAS (только настройки)

     /usr/syno/sbin/./synodsdefault --reset

#### Сброс Synology Nas к заводским настройкам по умолчанию (ВСЕ ДАННЫЕ OBS OBS БУДУТ УДАЛЕНЫ)

     /usr/syno/sbin/./synodsdefault --factory-default

#### Переустановите Synology Nas Station, все данные будут сохранены:

     /usr/syno/sbin/./synodsdefault --reinstall; reboot

#### Правильный способ перезапустить SSHD вашего NAS через cli:

     synoservicectl --restart sshd

#### Получение списка, удаление или установка файла пакета .spk (доступен локально)

      synopkg

#### Установите набор сетевых и двоичных инструментов отладки ELF (и перейдите в корневой сеанс)

     synogear

#### Напишите и прочитайте файл стиля .ini со строками пар ключ=значение.

     synosetkeyvalue
     synogetkeyvalue

#### Завершите работу и выключите NAS (так же, как сейчас выключение -h)

     synopoweroff

#### Показать установленные пакеты

     synopkg list | sed 's/: .*$//' 

#### Удалить пакет

     sudo synopkg uninstall 

#### Выключение Synology и выключение питания тоже

     syno_poweroff_task

#### Установить/установить пароль для локального пользователя

     synoauth local_username password

#### Управление функцией автоблокировки IP-адресов

     synoautoblock OPTIONS 

####Управление функцией блог

     synoblog_backup [-r|-b] p [-u username] [-o]

#### Устройство управления дисками Synology: что-то вроде /dev/hda или /dev/sda.

     syno_disk_ctl OPTIONS DEVICE  

#### Инструмент Synology Clear .tbd-File

     SYNOClearTdb FILE 

#### Различные способы распечатать различную информацию о вашем NAS

     more /etc.defaults/VERSION 
     cat /etc/synoinfo.conf
     cat /proc/cmdline
     synoshare --enum ALL 
     synonet --show 
     synodisk --enum 
     synospace --enum -a 

#### Перезапустить индекс

     synoservicectl --restart synoindexd

#### Проверьте наличие обновлений

     sudo synoupgrade --check

#### Перезапустить веб-сервер

     /usr/syno/sbin/synoservicecfg --restart httpd-user 
     /usr/syno/sbin/synoservicectl --restart pkgctl-WebStation

#### Создайте список того, что вы можете контролировать

     /usr/syno/sbin/synoservice --list

#### DSM API — предоставление информации DSM.

     syno dsm getInfo --pretty 

#### API File Station: предоставление информации File Station.

     syno fs getInfo --pretty 

#### File Station API - Enumerate files in a given folder

     syno fs listFiles --payload '{"folder_path":"/path/to/folder"}' --pretty 

#### Download Station API — список задач загрузки

     syno dl listFiles --payload '{"limit":5, "offset":10}' --pretty 

#### Download Station API — создание задачи загрузки

     syno dl createTask --payload '{"uri":"https://link"}'

#### API Audio Station — поиск песни

     syno as searchSong --payload '{"title":"my_title_song"}' --pretty

#### API Video Station — список фильмов

     syno vs listMovies --payload '{"limit":5}' --pretty

#### Video Station DTV API — список каналов

     syno dtv listChannels --payload '{"limit":1}' --pretty 

#### API Surveillance Station — получение информации о камере

     syno ss getInfoCamera --payload '{"cameraIds":8}' --pretty 

#### Перезапустить, включить, остановить samba

     /usr/syno/etc/rc.sysv/S80samba.sh --help

#### Получить date Synology

     synodate --getSysDate

#### Printer stuff

    synoprint

#### Обновить индекс раньше

    indexfolder --type={SHARE_CREATE|SHARE_REMOVE} --share=<SHARED_FOLDER> --share_path=<SHARED_FOLDER>

#### Запустить медиасервер

    /usr/syno/bin/mediaserver.sh start

#### !!!!ОСТОРОЖНО, УБИВАЕМ NAS

    servicetool --get-service-volume download 

#### Получите ключ 2FA, если потеряете

    ssh root@nas cat /usr/syno/etc/preference/wuseman/google_authenticator

#### Вывести информацию о диске очень необычным способом

    dhm_tool -s 

## Автоблокировка Synology

#### Я видел много тем на форуме Synology по этой теме. НЕ трогайте файл БД, если он вам действительно не нужен, вместо этого используйте команду synoautoblock, см. примеры ниже:

#### Добавьте IP в базу данных автоблокировки:

    synoautoblock --deny <ip-address>
    
#### Сбросьте IP-адрес, который был добавлен по ошибке:

    synoautoblock --reset <ip-address>
    
#### Добавьте любой IP в белый список:

    synoautoblock --in-white-list <ip-address>
   
## Отладка и состояние системы:

#### Отладка поклонников и отправка результата по электронной почте (если адрес электронной почты настроен)

    syno_fan_debug
    
#### Запустите проверку работоспособности вашей системы и отправьте результат по электронной почте:

    syno_disk_health_record
    
#### Проверьте ~remain lifetime:

    syno_disk_remain_life_check
    
#### Запустите smartmontools и отправьте электронное письмо после завершения:

    syno_disk_smart_mail_send
    
#### Отладка спящего режима:

    syno_hibernation_debug
   
## Светодиод (получите минимальное и максимальное значение в: /usr/syno/etc.defaults/led_brightness.xml)

##### Получить текущую настройку:

    syno_led_brightness --get (Default on DS416: 1985157252)
    
##### Установите новую настройку:

    syno_led_brightness --set <brightness> 
    
## Пропускная способность

##### Распечатайте данные об использовании полосы пропускания пользователем:

    synobandwidth --status [<list=user|group|all(default)> <transfer=upload|download|all(default)>] <merge=0|1(default)>]
    
##### Установите новый лимит пропускной способности для пользователя:

    synobandwidth --set-global-conf <state=enabled|disabled> [<protocol=filestation|webdav|ftp|rsync|all(default)>

##### Распечатать статус пользователя за пользователем для всех служб:

     sh-4.3# synobandwidth --preview wuseman
        Protocol     Upload   Download
        filestation  0.00       0.00
        webdav       0.00       0.00
        ftp          0.00       0.00
        rsync        0.00       0.00

## ISCI

### Анализатор производительности Synology iSCSI

    synoiscsitop40
    
## Смена MTU:

     synonet --set_mtu eth0 9000

## Вентилятор

## Установите конфигурацию вентилятора (самый громкий звук будет похож на звук самолета)

     synofanconfig -parseXML 1000000


## Дополнительные команды Synology перечислены:

     sync
     synologconvert
     syno-dbus-check.sh
     synologrotated
     syno-letsencrypt
     synologset
     syno-move-coredump
     synologset1
     syno8021Xtool
     synolunbackup
     synoRTCTime
     synolunbkp
     syno_adv_test
     synoluntransform
     syno_dc_ctrl_adapter.sh
     synomediaparserd
     syno_disk_config_check
     synomkflv
     syno_disk_ctl
     synomkflvd
     syno_disk_data_collector
     synomkthumb
     syno_disk_db_update
     synomkthumbd
     syno_disk_dsl
     synomoduletool
     syno_disk_health_record
     synomount
     syno_disk_information_daily_record
     synomustache
     syno_disk_log_convert
     synomyds
     syno_disk_log_import_from_xml
     synonclient_send
     syno_disk_remain_life_check
     synonet
     syno_disk_smart_mail_send
     synonetd
     syno_disk_test_log_import_from_xml
     synonetdtool
     syno_disk_test_scheduler_set
     synonetseqadj
     syno_disk_testlog_convert
     synonfstop
     syno_disk_wcache_config_init
     synonotify
     syno_dvb_admin.sh
     synootp
     syno_fan_debug
     synoovstool
     syno_hdd_util
     synopartition
     syno_hibernation_debug
     synopasswordmail
     syno_hw_video_transcoding.sh
     synopayment
     syno_iptables_common
     synoperfeventd
     syno_led_brightness
     synoperformancediagnose
     syno_mem_check
     synopftest
     syno_pkgicon_sprite.py
     synophoto_acl
     syno_poweroff_task
     synophoto_acl_pgsql
     syno_scemd_connector
     synophoto_autoblock
     syno_smart_result_collect
     synophoto_backup
     syno_smart_test
     synophoto_config
     syno_ssd_trim
     synophoto_config_root
     syno_system_dump
     synophoto_dsm_user
     synoabnormalloginmail
     synophoto_external_access
     synoacltool
     synophoto_extract_preview
     synoagentregisterd
     synophoto_music
     synoappbkp
     synophoto_sdk_share_set
     synoappnotify
     synophoto_sns_utils
     synoapppriv_updater
     synophoto_update_db
     synoarchivetool
     synophoto_watermark_util
     synoauth
     synophotoio
     synoautoblock
     synopingpong
     synobackup
     synopkg
     synobackupd
     synopkgctl
     synobandwidth
     synopkghelper
     synoblog_backup
     synoplatform
     synobootseq
     synoportforward
     synobootupcheck
     synopoweroff
     synobtrfssnap
     synopreferencedir
     synocacheclient
     synoprint
     synocachepinfiletool
     synopsql
     synocachepinfiletool-status
     synoquota
     synocachepinfiletoolha
     synoraidtool
     synocerttool
     synorecycle
     synocfgen
     synorelayd
     synocgid
     synoretainer
     synocgitool
     synoretention-lun
     synocheckhotspare
     synoretentionconf
     synocheckiscsitrg
     synoretentiontest
     synochecknetworkcfg
     synoretentiontestutil.sh
     synocheckshare
     synorouterportfwd
     synocheckswapconfig
     synoroutertool
     synocloudserviceauth
     synorsyncdtool
     synocmsclient
     synosavetime
     synocodectool
     synoscgi
     synoconfbkp
     synoscgi
     synoschedtask
     synocontentextract
     synoschedtool
     synocontentextractd
     synoscimprofile
     synocopy
     synosdutils
     synocredential
     synosearch
     synocrond
     synosearchagent
     synocrtregister
     synoselfcheck
     synocrtunregister
     synoservice
     synodatacollect
     synoservicecfg
     synodataverifier
     synoservicectl
     synodate
     synoservicemigrate
     synodctest
     synosetkeyvalue
     synodd
     synoshare
     synoddnsinfo
     synosharequota
     synoddsmtool
     synosharesnapshot
     synodisk
     synosharesnaptool
     synodiskdatacollect
     synosharesnaptree
     synodiskfind
     synosharingbackup
     synodiskpathparse
     synosharingchecker
     synodiskport
     synosharingcron
     synodriveencode
     synosharingurl
     synodrivehook
     synosmartblock
     synodriveindex
     synosnapschedtask.sh
     synodriveobject
     synosnmpcd
     synodrivesettings
     synospace
     synodriveversion
     synospace.sh
     synodrivevolume
     synosshdutils
     synodsdefault
     synostgpool
     synodsinfo
     synostgsysraid
     synodsmnotify
     synostgvolume
     synoeaupgrade
     synostorage
     synoethinfo
     synostoragecore
     synoexternal
     synostoraged
     synofanconfig
     synosupportchannelchecker
     synofileutil
     synosyncdctime
     synofirewall
     synosyslogmail
     synofirewallUpdater
     synotc
     synoflashcache
     synotc_common
     synoflvconv
     synothumb
     synofstool
     synotifyd
     synogear
     synotifydutil
     synogetkeyvalue
     synotimecontrol
     synogpoclientd
     synotlstool
     synogrinst
     synotune
     synogroup
     synotunnelexec
     synoguest
     synoupgrade
     synohacore
     synoupnp
     synoindex
     synoups
     synoindex_mgr
     synoupscommon
     synoindex_package.sh
     synousbcam
     synoindexd
     synousbcopy
     synoindexplugind
     synousbdisk
     synoindexscand
     synousbmodemd
     synoindexworkerd
     synouser
     synoiscsiep
     synouserdir
     synoiscsihook
     synouserhome
     synoiscsitool
     synovolumesnapshot
     synoiscsitop
     synovpnc
     synoiscsitop40
     synovspace
     synoiscsiunmap
     synovspace_wrapper
     synoiscsiwebapi
     synow3
     synoisns
     synow3tool
     synokerneltz
     synowebapi
     synolanstatus
     synowifid
     synoldapclient
     synowin
     synoldapclientd
     synowireless
     synologaccd
     synowsdiscoveryd
     synologand
     synowstransferd
     synologanutil
     synozram
     synologconfgen
     

