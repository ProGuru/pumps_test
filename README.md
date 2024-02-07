Задача:
Блок управления подпиточными насосами

Входы (все дискретные):
1 Датчик перепада давления на насосах (10)
2 Датчик-реле давления для включения насосов (11)
3 Датчик сухого хода (14)
4 Сброс аварий
Выходы (все дискретные):
1 Включение насоса 1 (21)
2 Включение насоса 2 (22)
3 Авария насоса 1
4 Авария насоса 2
Алгоритм работы:
- В один момент времени работает только один насос.
- Включение насосной группы производится при размыкании датчика 11, т.е. при падении давления в
контуре.
- При поступлении сигнала включения включается насос с наименьшим временем работы до этого
момента (при первом запуске включается насос 21).
- В режиме работы насосы переключаются через заданные промежутки времени, т.е. происходит
чередование рабочего насоса для равномерного износа.
- После отключения одного насоса, перед включением следующего насоса должна выдерживаться
пауза;
- Также переключение насоса происходит при выходе из строя рабочего насоса (Аварийный ввод
резерва).
- Выход из строя насоса определяется по сигналу датчика 10.
Если после включения насоса через определенное время датчик не замкнулся, то это авария.
Если в процессе работы датчик разомкнулся на время, большее чем задано, то это тоже авария.
- При аварии насоса, он отключается и в работу включается второй насос (через заданную задержку
времени). При аварии насоса включается соответствующий выход "Авария".
- Датчик сухого хода работает следующим образом: если он разомкнулся, то насосная группа
отключается для защиты от пропадания воды. При появлении воды и замыкании датчика насосы
возвращаются в работу в прежнем режиме.
Дополнения:
Алгоритм должен быть выполнен на языке С / С++. Все временные задержки должны быть
настраиваемыми и задаваться в секундах. Проверка работоспособности алгоритма будет происходить
на контроллере, в котором есть следующие способы получения времени:
• функция, возвращающая кол-во миллисекунд с момента старта контроллера
uint32_t GetSysTicks();
• структура часов реального времени:
struct TimeStruct
{
int16_t seconds; //!< Секунды
int16_t minutes; //!< Минуты
int16_t hours;
 //!< Часы
};
