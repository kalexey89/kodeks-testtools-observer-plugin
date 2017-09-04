## TestTools Observer ##
#### Нативный Node.JS модуль для мониторинга производительности системы и процессов. ####

#### Сборка модуля ####
Для сборки модуля требуется **node-gyp** и **C++ компилятор** с поддержкой стандарта **C++11**.

> npm install -g node-gyp

> npm install --save nan bindings

> node-gyp rebuild

#### Поддерживаемые версии Node.JS и ОС ####
Node.JS: 4.4.3 и выше.
ОС: Windows XP / Windows Server 2003 и выше, Linux - в планах.

#### Пример использования модуля ####

    'use strict';
    
    const Observer = require('testtools-observer');
    
    // Создаем экземпляр наблюдателя за системой
    const sysob = new Observer();
    // Перечисляем счетчики, значения которых хотим получить
    const mask =
        1 |    // Количество процессов
        2 |    // Количество потоков
        4 |    // % загрузки процессора
        8 |    // % потребления физ. памяти
        16 |   // потребление физ. памяти в кб
        32 |   // % потребления вирт. памяти
        64 |   // потребление вирт. памяти в кб
        128;   // % загрузки жесткого диска
    // Вызываем функцию опроса счетчиков (она возвращает объект Promise)
    sysob.poll(mask)
        .then(result => console.log(result))    // Выводим результат в случае успеха
        .catch(error => console.error(error));  // Выводим текст ошибки в случае проблем
    // Вывод:
    //  { pid: null,
    //    processes: 70,
    //    pmemusagekb: 2709424,
    //    threads: 882,
    //    procusage: 3.611558994775743,
    //    diskusage: 1.0845601695732017,
    //    pmemusage: 43,
    //    vmemusage: 6,
    //    vmemusagekb: 126048 }