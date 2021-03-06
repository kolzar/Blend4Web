.. _physics:

******
Физика
******

Подготовка к использованию
==========================

Для задействования физики на сцене необходимо установить флаг ``Enable Physics`` в вкладке сцены в Blender'е.

.. image:: src_images/physics/scene_interface_phys_enable.png
   :align: center
   :width: 100%

|

Настройка физических параметров производится в режиме ``Blender Game``.

.. image:: src_images/physics/info_panel.jpg
   :align: center
   :width: 100%

|

Статический тип физики
======================

Может использоваться как ограничитель движения других объектов, например, для определения столкновений с ландшафтом, стенами и т.д. В настройках физики такого объекта для опции ``Physics Type`` должно быть выбрано значение ``Static`` (значение по умолчанию).

.. image:: src_images/physics/physics_panel_static.png
   :align: center
   :width: 100%

|

Меш может быть покрыт одним или несколькими физическими материалами. Во вкладке ``Material`` должна быть включена опция ``Blend4Web > Special: Collision``. Также во вкладке ``Material`` на панели ``Physics`` (в режиме ``Blender Game``) располагаются физические настройки материала. Поддерживаются следующие физические настройки материала: трение (``Friction``), упругость (``Elasticity``). 

.. image:: src_images/physics/material_panel_physics.png
   :align: center
   :width: 100%
   
|

Поле ``Collision ID`` предназначено для определения столкновения со специфическим материалом, и может быть оставлено пустым. Пример использования ``Collision ID`` - определение нахождения игрового персонажа на разных типах покрытия ландшафта - трава, песок, деревянное покрытие и т.д.

Опция ``Ghost`` исключает материал из физических взаимодействий, но сообщает приложению о контакте с ним. Пример - определение, что игровой персонаж находится на вертикальной лестнице.

.. image:: src_images/physics/water_tower.jpg
   :align: center
   :width: 100%

|

Поле ``Collision Group`` отвечает за физическую группу, к которой относится материал.
Поле ``Collision Mask`` определяет все физические группы, с которыми будет взаимодействовать данный материал.


Динамический тип физики
=======================

Предназначен для симуляции движения жесткого тела. 

.. image:: src_images/physics/physics_dynamic.jpg
   :align: center
   :width: 100%

|

В настройках физики такого объекта для опции ``Physics Type`` может быть выбрано значение ``Rigid Body`` (с вращениями) или ``Dynamic`` (без вращений). В настройках ``Collision Bounds`` может быть выбран тип коллайдера, поддерживаются: ``Box``, ``Capsule``, ``Sphere``, ``Cylinder``, ``Cone``. Другие поддерживаемые настройки: масса (``Mass``), демпфирование (``Damping``) - для перемещения (``Translation``) и вращения (``Rotation``). 

Поле ``Collision Group`` отвечает за физическую группу, к которой относится объект.

Поле ``Collision Mask`` определяет все физические группы, с которыми будет взаимодействовать данный объект.

.. image:: src_images/physics/physics_panel_dynamic.png
   :align: center
   :width: 100%
   
|

В настройках панели физики объекта должен быть установлен флаг ``Detect Collisions``. Поле ``Collision ID`` предназначено для определения столкновения со специфическим объектом (например, прикрепленный к камере объект для определения близости FPS персонажа к предметам), и может быть оставлено пустым. 

.. image:: src_images/physics/object.png
   :align: center
   :width: 100%
   
|

Для материала такого объекта поддерживаются: трение (``Friction``), упругость (``Elasticity``). В случае использования на одном меше нескольких материалов физические настройки считываются с первого из них.

Для объекта-камеры должна использоваться настройка ``Physics Type`` = ``Dynamic``, должен быть установлен флаг ``Detect Collisions``.


Ограничители (Constraints)
==========================

Физические ограничители используются для уменьшения числа степеней свободы объектов.

.. image:: src_images/physics/physics_constraints.jpg
   :align: center
   :width: 100%
   
|

Установка физического ограничителя (``Rigid Body Joint``) на объект происходит в панели ``Object Constraints``. Поддерживаемые типы (``Pivot Type``): ``Ball``, ``Hinge``, ``Cone Twist``, ``Generic 6 DoF``. Физический ограничитель можно установить на один из двух взаимодействующих объектов, при этом другой выступает в качестве цели (``Target``). Оба объекта могут быть со статическим и/или динамическим типом физики. В ограничителях (кроме ``Ball``) могут настраиваться пределы перемещения и вращения.

.. image:: src_images/physics/physics_constraints_panel.png
   :align: center
   :width: 100%
   
|


Колесные транспортные средства
==============================

Модель транспортного средства (ТС) должна состоять из 6 отдельных объектов - шасси, 4 колеса, рулевое колесо. Центр меша шасси должен соответствовать центру масс. Центры мешей колес и рулевого колеса должны располагаться на осях вращения. Рулевое колесо должно быть ориентировано в локальной системе координат: X - ось вращения, Y - вправо, Z - вверх. Объекты могут иметь любые названия.

.. image:: src_images/physics/physics_vehicle_wheeled.jpg
   :align: center
   :width: 100%

|

На всех 6 объектах нужно выставить ``Vehicle Part``, указать один и тот же идентификатор в поле ``Vehicle Name``, выбрать соответствующий тип объекта - ``Chassis``, ``Steering Wheel``, ``Back Right Wheel`` и т.д. Для колес имеется также настройка компенсирующего хода подвески ``Suspension Rest Length``.

Для шасси необходимо указать реалистичную массу (т.к. значение по умолчанию 1 кг). Для этого перейти в настройки физики, для опции ``Physics Type`` выбрать значение ``Rigid Body``, и выставить нужное значение (например, 1000 кг) в поле ``Mass``.

Параметры настройки для шасси
-----------------------------

*Vehicle Settings > Force Max*
    Максимальная движущая сила транспортного средства.

*Vehicle Settings > Brake Max*
    Максимальный коэффициент торможения.

*Vehicle Settings > Suspension Compression*
    Коэффициент демпфирования при растяжении подвески.

*Vehicle Settings > Suspension Stiffness*
    Коэффициент жесткости подвески.

*Vehicle Settings > Suspension Damping*
    Коэффициент амортизации подвески.

*Vehicle Settings > Wheel Friction*
    Константа трения колес о поверхность. Для реалистичных Т.С. должен быть в районе 0.8. Но может быть значительно увеличен, для улучшения управляемости (1000 и более)

*Vehicle Settings > Roll Influence*
    Снижает вращающий момент от колес, уменьшая вероятность переворота транспортного средства (0 - нет вращающего момента, 1 - реальное физическое поведение).

*Vehicle Settings > Max Suspension Travel Cm*
    Максимальный ход подвески в сантиметрах.

Для рулевого колеса(``Steering Wheel``) необходимо указать максимальный угол поворота(``Steering Max``) и передаточное отношение угла поворота руля к 
передним колесам (``Steering Ratio``). Максимальное значение угла поворота указывается в оборотах. Один оборот равен 360 градусам. Таким образом,
поставив ``Steering Max`` равным единице, а ``Steering Ratio`` равным 10, максимальный поворот руля получится равным 360 градусам, а максимальный
поворот передних колес 36 градусов.

На этом этапе можно произвести экспорт и загрузить сцену в движок. Рекомендуется создать дорожную поверхность с физическим материалом. В просмотрщике нажать клавишу ``Q`` для выбора контролируемого объекта, и выбрать шасси. Использовать ``W``, ``A``, ``S``, ``D`` для управления.

Дополнительно можно настроить демпфирование ``Damping`` перемещения (``Translation``) и вращения (``Rotation``). Свойство влияет на скорость перемещения и инерционность ТС.

Настройка трения и эластичности физического материала дорожного покрытия не влияют на поведение ТС.


Плавающие объекты
=================

.. image:: src_images/physics/physics_floater.jpg
   :align: center
   :width: 100%

|

Для того, чтобы объект мог плавать на поверхности воды (объекта с материалом ``Special Water``), необходимо выставить свойство ``Floating``. Существует два типа частей плавающего объекта: ``Main Body`` - непосредственно сам плавающий объект и ``Bob`` - вспомогательный объект-поплавок, на который будет действовать выталкивающая из воды сила. Плавающий объект может иметь неограниченное количество объектов типа ``Bob``. В качестве поплавков могут использоваться как меши, так и объекты типа ``Empty``.

Всем объектам, входящим в состав одного плавающего объекта необходимо выставить одинаковое имя в поле ``Floater Name``

Параметры настройки плавающего объекта
--------------------------------------

*Floating Settings > Floating Factor*
    Коэффициент выталкивания объекта из воды.

*Floating Settings > Water Linear Damping*
    Демпфирование линейной скорости при нахождении объекта на поверхности воды (или под водой). Когда объект находится вне воды, используется значение из настроек физики.

*Floating Settings > Water Rotation Damping*
    Демпфирование вращения при нахождении объекта на поверхности воды (или под водой). Когда объект находится вне воды, используется значение из настроек физики.

Плавающие транспортные средства
===============================

.. image:: src_images/physics/physics_boat.jpg
   :align: center
   :width: 100%

|

Плавающие транспортные средства используют часть параметров из настроек ``Vehicle Settings`` и все настройки аналогичные ``Floating Settings``. На основном объекте необходимо выставить ``Vehicle Part``, типа ``Hull``. Так же как и плавающий объект плавающее транспортное средство требует наличия вспомогательных объектов типа ``Bob``.

Параметры настройки плавающего транспортного средства
-----------------------------------------------------

*Vehicle Settings > Force Max*
    Максимальная движущая сила транспортного средства.

*Vehicle Settings > Brake Max*
    Максимальный коэффициент торможения.

*Floating Settings > Floating Factor*
    Коэффициент выталкивания объекта из воды.

*Floating Settings > Water Linear Damping*
    Демпфирование линейной скорости при нахождении объекта на поверхности воды (или под водой). Когда объект находится вне воды, используется значение из настроек физики.

*Floating Settings > Water Rotation Damping*
    Демпфирование вращения при нахождении объекта на поверхности воды (или под водой). Когда объект находится вне воды, используется значение из настроек физики.

Особенности использования в приложениях
=======================================

Физическая подсистема реализована в модуле **uranium.js** и загружается отдельно от основного кода движка. Модуль **uranium.js** представляет собой модификацию физического движка `Bullet <http://bulletphysics.org/>`_, портированную для работы в браузерах. Быстрое подключение физической подсистемы можно осуществить, разместив файлы **uranium.js** и **uranium.js.mem** в той же директории, где расположен исходный код движка, используемого в приложении.

В противном случае необходимо указать путь к модулю, используя конструкцию вида:

.. code-block:: javascript

    m_config.set("physics_uranium_path", ".../uranium.js");

.. note::

    При разработке приложения :ref:`в составе SDK <sdk_dev>` путь к физическому движку определяется автоматически.

Если использование физики не требуется, рекомендуется отключить флаг ``Enable Physics`` во вкладке сцены в Blender'е. Также можно принудительно отключить загрузку модуля **uranium.js**, если до начала инициализации движка вызывать следующий метод:

.. code-block:: javascript

    m_config.set("physics_enabled", false);
