SMS-команды
*****
Безопасность прежде всего
======
AndroidAPS позволяет контролировать телефон ребенка удаленно посредством текстовых сообщений (смс). Если смс-коммуникатор активирован, не забывайте, что телефон, настроенный на подачу удаленных команд, может быть украден. Поэтому всегда защищайте смартфон хотя бы ПИН-кодом.
* AndroidAPS при помощи смс также сообщит, выполнены ли удаленные команды, такие как болюс или изменения профиля. Рекомендуется сделать такую настройку, чтобы подтверждающие тексты направлялись по меньшей мере на два разных телефона на тот случай, если один из них украден.
* **Если вы подаете болюс через SMS-команды необходимо вводить углеводы через Nightscout (NSClient, сайт...)!** Если вы этого не сделаете, AAPS учтет правильное количество активного инсулина IOB, и будет считать, что активных углеводов COB слишком мало и, вероятно, не будет подавать корректировочный болюс, полагая, что у вас много активного инсулина.

Как это работает
=====
* Большинство корректировок временных целей, слежение за работой ААПС и т. д. может выполняться в приложении ` NSclient <../Children/Children.html> ` _ на Android-телефоне с подключением к Интернету.
* Болюсы не могут подаваться через Nightscout, но можно использовать SMS-команды.
* Если у вас iPhone для слежения и, следовательно, нет возможности использовать NSclient, доступны дополнительные SMS-команды.

* В настройках Android телефон перейдите в приложения > AndroidAPS > Разрешения и включите SMS
* В AndroidAPS перейдите в Настройки > SMS коммуникатор и введите номер телефона, от которого вы сможете получать SMS команды (разделенные точками с запятыми), т.е. +4412345678;+4412345679), а также включите опцию 'Разрешить удаленные команды с помощью СМС'.
* Если вы хотите использовать более одного номера:

  * Введите только один номер.
  * Убедитесь, что этот телефон работает с алгоритмом путем отправки и подтверждения команды SMS.
  * Введите дополнительные номера, разделенные точкой с запятой, без пробела.
  
    .. изображение:: ../images/SMSCommandsSetupSpace.png
      :alt: Настройка SMS команд


* Отправьте SMS на телефон с AndroidAPS с одобренного(ых) вами телефона(ов) при помощи команд перечисленных ниже **ЗАГЛАВНЫМИ БУКВАМИ**, телефон ответит подтверждением успешного выполнения команды или запрошенного статуса. Если необходимо, подтвердите команду, отправив код, предлагаемый в ответном SMS-сообщении.

**Подсказка: Если отправляется много SMS, полезно держать функцию SMS незанятой на обоих телефонах,.

Команды
=====

Верхний и нижний регистр не имеет значения при отправке команд.

Команды должны отправляться на английском языке, ответ будет получен на локальном языке, если строка ответа уже " переведена <../translations.html#translate-strings-pl-androidaps-app> ` _.

.. изображение:: ../images/SMSCommandsSetup.png
  :alt: Пример команд SMS

Замкнутый цикл
-----
* ОТКЛЮЧИТЬ ЗЦ
   * Ответ: цикл отключен
* ВКЛЮЧИТЬ ЗЦ
   * Ответ: цикл включен
* СТАТУС ЗЦ
   * Ответ зависит от фактического состояния
      * зцикл не работает
      * зцикл работает
      * Остановлен (на 10 мин)
* ОСТАНОВИТЬ ЗЦ 20
   * Зцикл остановлен на 20 минут
* ВОЗОБНОВИТЬ ЗЦ
   * Ответ: Цикл возобновлен

Данные мониторинга
-----
* BG/ГК
   * Ответ: новая ГК: 5.6 4мин назад, дельта: -0,2 ммоль, активный инсулин IOB: 0.20 ед (болюс: 0.10 ед базал: 0.10 ед)
* CAL 5.6
   * Ответ: Чтобы отправить калибровку 5.6 ответьте кодом Rrt
   * Ответ после получения правильного кода: Калибровка отправлена / Calibration sent (* *Если установлен xDrip. Разрешение на прием калибровок должно быть включено в xDrip+**)

базал
-----
* BASAL STOP/CANCEL
   * Ответ: Чтобы остановить временный базал ответьте кодом EmF [ Примечание: код EmF-это пример]
* BASAL 0.3
   * Ответ: Для запуска базала 0.3ед/ч на 30 минут ответьте кодом Swe
* BASAL 0.3 20
   *Ответ: Для запуска базала 0.3ед/ч на 20 минут ответьте кодом Swe
* BASAL 30%
   * Ответ: Для запуска базала 30% на 30 минут ответьте кодом Swe
* БАЗАЛ 30% 50
   * Ответ: Для запуска базала 30% на 50 минут ответьте кодом Swe

болюс
-----
Удаленный болюс не допускается в пределах 15 минут -значение редактируемое только в том случае, если добавлено 2 номера телефонов-после последней команды болюс или удаленных команд! * Поэтому ответ зависит от времени последнего болюса.

* Болюс 1.2
   *Ответ А: Для подачи болюса 1,2 ед ответьте кодом Rrt
   * Ответ B: Удаленный болюс недоступен. Повторите позже.
* БОЛЮС на 0.60 ЕДЫ
   * Если вы зададите необязательный параметр прием пищи MEAL, то будет задано значение временная цель прием пищи MEAL (значения по умолчанию: 90 мг/дл, 5,0 ммоль/л на 45 мин).
   *Ответ А: Для подачи болюса 0,6 ед на еду ответьте кодом Rrt
   * Ответ B: Удаленный болюс недоступен. 
* УГЛИ 5
   * Ответ: Чтобы ввести 5 г в 12:45 ответить кодом EmF
* УГЛИ 5 17:35/5:35PM
   * Ответ: Чтобы ввести 5 г в 17:35 ответьте кодом EmF
* EXTENDED STOP/CANCEL
   * Ответ: Для прекращения подачи пролонгированного болюса ответьте кодом EmF
* EXTENDED 2 120
   * Ответ: Для начала подачи пролонгированного болюса 2 ед. на 120 мин. ответьте кодом EmF

Профиль
-----
* СТАТУС ПРОФИЛЯ
   * Ответ: Профиль1
* СПИСОК ПРОФИЛЕЙ
   * Ответ: 1. ` Profile1 ` 2. ` Profile2 `
* PROFILE 1
   * Ответ: Чтобы переключиться на Профиль 1 100% ответьте кодом Any
* PROFILE 2 30
   * Ответ: Чтобы переключиться на Профиль 2 30% ответьте кодом Any

Другое
-----
* ОБНОВИТЬ НАЗНАЧЕНИЯ
   * Ответ: Синхронизировать назначения с NS
* ПЕРЕЗАПУСТИТЬ NSCLIENT
   * Ответ: Перезапуск NSCLIENT 1 получатель
* ПОМПА
   * Ответ: Последнее соед: 1 мин. назад временный базал: 0.00ед/ч @11:38 5/30мин IOB: 0.5U Reserv: 34U Batt: 100
* ОТКЛЮЧИТЬ/ОСТАНОВИТЬ СМС
   * Ответ: Чтобы отключить удаленную службу SMS ответьте кодом Any. Имей в виду, что вы сможете его повторно активировать только непосредственно с главного смартфона AAPS.
* ЦЕЛЬ ПРИЕМ ПИЩИ/НАГРУЗКА/ГИПО MEAL/ACTIVITY/HYPO   
   * Ответ: Чтобы установить временную цель MEAL/ACTIVITY/HYPO ответьте кодом Any
* ЦЕЛЬ ОСТАНОВИТЬ/ОТМЕНИТЬ   
   * Ответ: Чтобы отменить временную цель ответьте кодом Any
* СПРАВКА
   * Ответ: ГК, ПЕТЛЯ, НАЗНАЧЕНИЯ, .....
* СПРАВКА БОЛЮС
   * Ответ: БОЛЮС 1.2 БОЛЮС 1.2 НА ЕДУ

Устранение неполадок
=====
Была жалоба на остановку работы SMS команд после обновления на телефоне Galaxy S10. Решается путем отключения опции "отправлять как сообщения чата".

.. изображение:: ../images/SMSdisableChat.png
  :alt: Отключить SMS как сообщение чата