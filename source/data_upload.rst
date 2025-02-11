.. _ngcom_data_upload:

Как загружать данные
================================

Загрузка растровых и векторных геоданных в :ref:`Веб ГИС <ngcom_description>` происходит путем создания ресурсов :ref:`Растровый слой <ngcom_raster_layer>` и :ref:`Векторный слой <ngcom_vector_layer>`.

.. note:: 
	Ограничение на размер загружаемых файлов зависит от выбранного тарифного плана. Для **Premium** - 1.0 GB, для **Free** и **Mini** - 128 Mb. Для растров это ограничение соответствует файлам без сжатия в EPSG:3857.

.. _ngcom_raster_layer:

Растровые данные
-------------------------------

#. Откройте :ref:`Группу ресурсов <ngcom_resources_group>`, в которой вы хотите создать слой (на главной странице Веб ГИС по умолчанию открыта Основная группа ресурсов);
#. Выберите :menuselection:`Создать ресурс --> Растровый слой` на правой панели :ref:`веб-интерфейса <ngw_admin_interface>` Веб ГИС;
#. В открывшемся окне заполните поле :guilabel:`Наименование` на вкладке :guilabel:`Ресурс` и выберите файл с растровыми геоданными на вкладке :guilabel:`Растровый слой`;
#. Нажмите кнопку :guilabel:`Создать`. Если Растровый слой создался успешно, то информация о нем появится в блоке :guilabel:`Дочерние ресурсы` соответствующей Группы ресурсов.

.. important::
	Если вы планируете просматривать Растровый слой с помощью :ref:`Веб-карты <ngcom_webmap_create>` или публиковать его по протоколу :term:`WMS`, необходимо создать для него `Стиль <https://docs.nextgis.ru/docs_ngcom/source/styles.html#ngcom-raster-style>`_.


.. _ngcom_raster_requirements:

Требования к исходным данным
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Поддерживаемые формат:  :term:`GeoTIFF`
* Данные должны быть географически привязаны и иметь корректно сформированное описание системы координат (в тегах GeoTIFF).

.. figure:: _static/Raster_layer.gif
   :name: Raster_layer
   :align: center
   :width: 850px

Больше информации о загрузке растровых геоданных в Веб ГИС - :ref:`здесь <ngw_create_raster_layer>`. 


.. _ngcom_raster_volume:

Замечания по загрузке растров большого объёма
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Данные БПЛА, космической съемки высокого разрешения и другие растры могут занимать значительный объем. При этом сам по себе размер файла растра не очень репрезентативен, так как реальный объем данных может быть значительно больше из-за сжатия. Чтобы быстро показывать их на веб картах и раздавать с помощью сервисов, они должны быть специальным образом преобразованы перед загрузкой в Веб ГИС и созданием соответствующих растровых слоёв.

Существует три ограничения, касающиеся загрузки растров большого размера:

#. Размер загружаемого файла - максимальный размер каждого файла составляет **1 Гб**. Это значение нельзя изменить в облаке, но можно на `на своем сервере <https://nextgis.ru/pricing>`_;
#. Общий объем данных - на плане Премиум вы можете загрузить до `50 Гб данных <https://nextgis.ru/pricing-base/#volume-premium>`_ (это значение можно увеличить);
#. Время обработки - максимальное время обработки составляет 3 минуты, после этого процесс импорта будет прерван и выведено сообщение об ошибке. Растровый слой не будет создан.


Время обработки зависит от следующих параметров загружаемых растров:

#. Система координат
#. Внутреннее сжатие, часто это JPEG или LZW.

Как следствие, для гарантированной загрузки рекомендуется:

#. Перепроецировать исходные данные в 3857
#. Убрать внутреннее сжатие

Если это сделано, то растр размером до 1 Гб должен загрузиться. Если ваш растр меньше по размеру, то он тоже загрузится в случае, если перепроецирование и распаковка займут менее 3 минут.

.. _ngcom_vector_layer:

Векторные данные
----------------

#. Откройте :ref:`Группу ресурсов <ngcom_resources_group>`, в которой вы хотите создать слой (на главной странице Веб ГИС по умолчанию открыта Основная группа ресурсов);
#. Выберите :menuselection:`Создать ресурс --> Векторный слой` на правой панели :ref:`веб-интерфейса <ngw_admin_interface>` Веб ГИС;
#. В открывшемся окне заполните поле :guilabel:`Наименование` на вкладке :guilabel:`Ресурс`, затем выберите файл с векторными геоданными и укажите его кодировку на вкладке :guilabel:`Векторный слой`;
#. Нажмите кнопку :guilabel:`Создать`. Если Векторный слой создался успешно, то информация о нем появится в блоке :guilabel:`Дочерние ресурсы` соответствующей Группы ресурсов.

Веб ГИС может принимать многослойные наборы данных на входе. Если в архиве содержится несколько слоёв, то после его загрузки пользователю будет предложено выбрать слой, на основе которого будет создан ресурс "Векторный слой".

.. important::
	Если вы планируете просматривать Векторный слой с помощью :ref:`Веб-карты <ngcom_webmap_create>` или публиковать его по протоколу :term:`WMS`, необходимо создать для него :ref:`Стиль <ngcom_styles>`.

Требования к исходным данным
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Поддерживаемые форматы: ESRI Shapefile (zip-архив без вложенных папок и других архивов, один слой - один архив), GeoJSON, GML или KML
* Не должно быть полей со следующими названиями: *id(ID), geom(GEOM)*

Если нужно загрузить данные в другом формате, вы можете использовать NextGIS Connect.

.. note::
	Мы рекомендуем не использовать кириллицу в названиях полей атрибутов. Несмотря на то, что такие данные могут быть загружены в Веб ГИС и показаны на картах, в некоторых случаях вы можете испытывать проблемы в работе с такими данными через WFS, в NextGIS Mobile и визуализацией (особенно если условные обозначения сформированы на базе одного из таких полей). Переименуйте поля латиницей перед загрузкой и используйте синонимы полей (алиасы) для их отображения кириллицей на картах.

.. figure:: _static/Vector_layer.gif
   :name: Vector_layer
   :align: center
   :width: 850px

Больше информации о загрузке векторных геоданных в Веб ГИС - :ref:`здесь <ngw_create_vector_layer>`.

.. note:: 
	Вы также можете загружать растровые и векторные данные в Веб ГИС :ref:`с помощью настольного приложения NextGIS QGIS <ngcom_ngqgis_connect_data_upload>`.
