# Исследование технологического процесса очистки золота
## Задача проекта
Спрогнозировать концентрацию золота при проведении процесса очистки золота
## Описание данных
Данные находятся в трёх файлах:
+ [Обучающая выборка](https://code.s3.yandex.net/datasets/geo_data_0.csv);
+ [Тестовая выборка](https://code.s3.yandex.net/datasets/geo_data_1.csv);
+ [Исходные данные](https://code.s3.yandex.net/datasets/geo_data_2.csv).

Данные индексируются датой и временем получения информации (признак `date`). Соседние по времени параметры часто похожи.

Некоторые параметры недоступны, потому что замеряются и/или рассчитываются значительно позже. Из-за этого в тестовой выборке отсутствуют некоторые признаки, которые могут быть в обучающей. Также в тестовом наборе нет целевых признаков.

Исходный датасет содержит обучающую и тестовую выборки со всеми признаками.

**Технологический процесс**
+ Rougher feed — исходное сырье
+ Rougher additions (или reagent additions) — флотационные реагенты: Xanthate, Sulphate, Depressant
    + Xanthate — ксантогенат (промотер, или активатор флотации);
    + Sulphate — сульфат (на данном производстве сульфид натрия);
    + Depressant — депрессант (силикат натрия).
+ Rougher process (англ. «грубый процесс») — флотация
+ Rougher tails — отвальные хвосты
+ Float banks — флотационная установка
+ Cleaner process — очистка
+ Rougher Au — черновой концентрат золота
+ Final Au — финальный концентрат золота

**Параметры этапов**
+ air amount — объём воздуха
+ fluid levels — уровень жидкости
+ feed size — размер гранул сырья
+ feed rate — скорость подачи

## Наименование признаков
Наименование признаков строится следующим образом:

`[этап].[тип_параметра].[название_параметра]`

Возможные значения для блока `[этап]`:
+ rougher — флотация
+ primary_cleaner — первичная очистка
+ secondary_cleaner — вторичная очистка
+ final — финальные характеристики

Возможные значения для блока `[тип_параметра]`:
+ input — параметры сырья
+ output — параметры продукта
+ state — параметры, характеризующие текущее состояние этапа
+ calculation — расчётные характеристики

## Технологический процесс
Как золото получают из руды?

Когда добытая руда проходит первичную обработку, получается дроблёная смесь. Её отправляют на флотацию (обогащение) и двухэтапную очистку.

<img src="https://pictures.s3.yandex.net/resources/viruchka_1576238830.jpg">

Описание каждой стадии:

1. **Флотация**

Во флотационную установку подаётся смесь золотосодержащей руды. После обогащения получается черновой концентрат и «отвальные хвосты», то есть остатки продукта с низкой концентрацией ценных металлов.

На стабильность этого процесса влияет непостоянное и неоптимальное физико-химическое состояние флотационной пульпы (смеси твёрдых частиц и жидкости).

2. **Очистка**

Черновой концентрат проходит две очистки. На выходе получается финальный концентрат и новые отвальные хвосты.

### Расчёт эффективности
Эффективность обогащения рассчитывается по формуле

<img src="https://pictures.s3.yandex.net/resources/Recovery_1576238822.jpg">

где:
+ C — доля золота в концентрате после флотации/очистки;
+ F — доля золота в сырье/концентрате до флотации/очистки;
+ T — доля золота в отвальных хвостах после флотации/очистки.

Для прогноза коэффициента нужно найти долю золота в концентратах и хвостах. Причём важен не только финальный продукт, но и черновой концентрат.

## Метрика качества
Для решения задачи вводится метрика качества sMAPE.

<img src="https://pictures.s3.yandex.net/resources/smape_1576238825.jpg">

Нужно спрогнозировать сразу две величины:
+ эффективность обогащения чернового концентрата `rougher.output.recovery`;
+ эффективность обогащения финального концентрата `final.output.recovery`.

Итоговая метрика складывается из двух величин:

<img src="https://pictures.s3.yandex.net/resources/_smape_1576238814.jpg">

## Направление деятельности
<svg width="100%"><foreignObject x="0" y="0" width="100%" height="160"><div style="display: flex; flex-wrap: wrap; padding-top: 8px; padding-bottom: 2px;"><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(110, 54, 48); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Машинное обучение</div></div><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(40, 69, 108); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Аналитика</div></div><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(90, 90, 90); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Регрессия</div></div></div></foreignObject></svg>

## Навыки и инструменты
<svg width="100%"><foreignObject x="0" y="0" width="100%" height="160"><div style="display: flex; flex-wrap: wrap; padding-top: 8px; padding-bottom: 2px;"><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(96, 59, 44); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Python</div></div><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(137, 99, 42); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Pandas</div></div><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(105, 49, 76); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Matplotlib</div></div><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(133, 76, 29); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">NumPy</div></div><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(137, 99, 42); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Scikit-learn</div></div><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(73, 47, 100); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Исследовательский анализ данных</div></div></div></foreignObject></svg>