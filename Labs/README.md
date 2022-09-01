# Цикл лабораторных работ для ИВТ

Ссылки на подробные методические материалы по каждой работе (*в производстве*):
1. ALU (Arithmetic Logic Unit)
2. RF (Register File & Memory)
3. MD (Main Decoder)
4. DP (Datapath)
5. LSU (Load/Store Unit)
6. IC (Interrupt Controller)
7. PU (Peripheral Units)
8. Programming

# Обзор лабораторных работ

<img src="../pic/labs.png"  border=3 />

Курс *Архитектур процессорных систем* включает в себя цикл из 8 лабораторных работ, в течение которых используя язык описания аппаратуры **Verilog HDL** на основе **FPGA** (ПЛИС, программируемая логическая интегральная схема), с нуля, последовательно, создается система, под управлением процессора с архитектурой **RISC-V**, управляющего периферийными устройствами и программируемого на языке высокого уровня **C**.

Создаваемая система на ПЛИС состоит из: процессора, памяти, контроллера прерываний и контрллера периферийных устройств. 

<img src="../pic/ml7_done.png"  border=3 />

Разработка лабораторных работ это последовательный процесс в результате которого будут освоен ряд различных инструментов и средств. В общих словах это:

**Verilog HDL** - язык описания аппаратуры, благодаря которому схемы не рисуются, а описываются с помощью текста (кода).

**Testbench** - тестовые окружения, котоорые представляют собой несинтезируемые (то есть не существующие в реальном физическом мире) блоки, созданные на языке Verilog HDL для автоматического тестирования разрабатываемых устройств и проверки их корректной работоспособности.

**FPGA** - программируемая логическая интегральная схема (ПЛИС), изменяя внутреннюю конфигурацию которой можно создать любые цифровые устройства (в рамках предоставляемых ресурсов).

**Vivado** - система автоматизированного проектирования, которая превращает Verilog-код в конфигурацию и прошивает ей ПЛИС на отладочной плате. 

**Архитектура RISC-V** - открытая и свободная система команд и процессорная архитектура на основе концепции RISC для микропроцессоров и микроконтроллеров.

**Язык ассемблера RISC-V** - список основных команд и особенности их использования и написания программ.

**Ассемблер RISC-V** - программа, которая превращает код, написанный на языке ассемблема RISC-V в машинные инструкции для процессора с архитектурой RISC-V.

Далее приводится краткое описание и цель каждой отдельной лабораторной работы.

## 1. Арифметико-логическое устройство (ALU)
<img src="../pic/ml1.png" border=3 />
На первой лабораторной работе изучаются базовые конструкции языка описания аппаратуры Verilog HDL, с помощью которого разрабатывается блок арифметико-логического устройства (АЛУ). АЛУ - это устройство, на входы которого подаются операнды, над которыми нужно выполнить некоторую операцию (сложение, вычитание и тому подобное) и код операции, которую нужно выполнить, а на выходе появляется результат этой операции. Проще говоря АЛУ - это "калькулятор" процессора.

Для проверки правильной работоспособности АЛУ в конце лабораторной работы, на языке Verilog HDL, пишется tesetbench (тестовое окружение), которое автоматически проверяет корректность его реализации.

## 2. Регистровый файл и память (RF)
<img src="../pic/ml2.png" border=3 />
На второй лабораторной разрабатываются элементы памяти для будущего процессора: память команд, память данных и регистровый файл. В памяти команд будет храниться программа, которую будет выполнять процессор. В памяти данных хранятся данные, которые будут обрабатываться процессором. Регистровый файл - это маленькая память, тоже с данными, которые могут быть поданы непосредственно на АЛУ. Особенность RISC-архитектур в том, что данные перед обработкой необходимо перенести из памяти данных в регистровый файл, только после этого к ним можно применять различные операции.

В рамках этой же работы из реализованных блоков собирается примитивное программируемое устройство, для которого пишется программа в машинных кодах. Это необходимо, чтобы обучающиеся глубже понимали принципы работы разрабатываемого устройства.

## 3. Основной дешифратор команд (MD)
<img src="../pic/ml3.png" border=3 />
Третья лабораторная посвящена разработке устройства управления – основному дешифратору команд. Функция основного дешифратора - получать на вход коды выполняемых операций и преобразовывать их в управляющие сигналы для всех блоков процессора (АЛУ, память, регистровый файл, мультиплексоры). Работа требует внимательности в реализации, а ее результат проверяется заранее подготовленными автоматическими тестами.

## 4. Тракт данных (DP)
<img src="../pic/ml4.png" border=3 />
Разработанные блоки объединяются, образуя тракт данных, управляемый основным дешифратором команд. Результатом четвертой лабораторной работы является однотактный процессор, с архитектурой RISC-V, поддерживающий стандартный набор целочисленных инструкций. В качестве проверки на процессоре запускаются программы, заранее написанные на языке ассемблера RISC-V. Сравнивается результат полученный на симуляторе и на разработанном процессоре.

## 5. Блог загрузки и сохранения данных (LSU)
<img src="../pic/ml5.png" border=3 />
В современных компьютерах память является отдельным от процессора устройством. В пятой работе память программ и память данных выносится за пределы процессора, объединяются в одну общую память и подключается через общую шину. В процессоре для этого появляется блок Load/Store Unit.

## 6. Подсистема прерывания (IC)
<img src="../pic/ml6.png" border=3 />
Одной из основных функций процессоров является возможность реагировать на внешние события (дернуть мышку, нажать кнопку и т.п.), автоматически запуская, при их возникновении, соответствующие программы. В шестой работе создается и подключается подсистема прерывания, к которой относятся контроллер прерываний с циклическим опросом и блок регистров статуса и управления.

## 7. Периферийные устройства (PU)
<img src="../pic/ml7.png" border=3 />
На седьмой работе создаются и подключаются к общей шине и подсистеме прерывания контроллеры периферийных устройств, такие как контроллер клавиатуры и VGA-контроллер.

## 8. Программирование на языке высокого уровня
<img src="../pic/ml8.png" border=3 />
В рамках восьмой работы настраивается компилятор GCC для RISC-V и для разработанной системы пишется программное обеспечение на языке программирования C.