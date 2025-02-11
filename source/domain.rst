.. sectionauthor:: Maxim Dubinin <maxim.dubinin@nextgis.com>

Как изменить домен
==================

.. note:: 
	Эта функциональность доступна только для пользователей плана `Premium <http://nextgis.ru/nextgis-com/plans>`_.

Создав Веб ГИС, по умолчанию вы получаете домен вида mywebgis.nextgis.com. Вы можете сменить его на домен своей организации, например gis.example.com.

Для этого, необходимо сделать несколько шагов. Эти шаги как правило производятся вашим системным администратором имеющим доступ к управлению доменами вашей организации.

**Шаг 1. Внести в DNS Запись 1 для получения сертификатов HTTPS**

.. code-block:: bash

   _acme-challenge.gis.example.com. CNAME _acme-challenge.nimbo.nextgis.net.
   
замените gis.example.com на домен для Веб ГИС вашей организации.

**Проверка 1**

Администратор организации должен проверить, что изменения были внесены правильно. Используйте `Dig <https://toolbox.googleapps.com/apps/dig/#CNAME/>`_. Для поиска введите: _acme-challenge.gis.example.com. Обратите внимание, что применение изменений DNS может занять время, пожалуйста, дождитесь пока это произойдет.

Ожидаемый ответ: возвращается запись CNAME (TTL и TARGET).

**Шаг 2. Внести в DNS Запись 2 для перенаправления запросов к Веб ГИС**

.. code-block:: bash

   gis.example.com. CNAME example.nextgis.com.

замените gis.example.com на домен для Веб ГИС вашей организации, a example.nextgis.com на адрес вашей Веб ГИС в домене *.nextgis.com

**Проверка 2**

Администратор организации должен проверить, что изменения были внесены правильно. Используйте `Dig <https://toolbox.googleapps.com/apps/dig/#CNAME/>`_. Для поиска введите: gis.example.com. Обратите внимание, что применение изменений DNS может занять время, пожалуйста, дождитесь пока это произойдет.

Ожидаемый ответ: возвращается запись CNAME (TTL и TARGET).

Когда изменения на вашей стороне вступят в силу, сообщите нам на support@nextgis.com, мы произведем финальные настройки.
