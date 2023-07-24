# Выбор локации для скважины
## Задача проекта
На основе данных геологической разведки выбрать район добычи нефти
## Описание данных
Данные геологоразведки трёх регионов находятся в файлах:
+ [Регион 1](https://code.s3.yandex.net/datasets/geo_data_0.csv);
+ [Регион 2](https://code.s3.yandex.net/datasets/geo_data_1.csv);
+ [Регион 3](https://code.s3.yandex.net/datasets/geo_data_2.csv);
+ id — уникальный идентификатор скважины;
+ f0, f1, f2 — три признака точек (неважно, что они означают, но сами признаки значимы);
+ product — объём запасов в скважине (тыс. баррелей).

**Условия задачи:**
+ Для обучения модели подходит только линейная регрессия (остальные — недостаточно предсказуемые).
+ При разведке региона исследуют 500 точек, из которых с помощью машинного обучения выбирают 200 лучших для разработки.
+ Бюджет на разработку скважин в регионе — 10 млрд рублей.
+ При нынешних ценах один баррель сырья приносит 450 рублей дохода. Доход с каждой единицы продукта составляет 450 тыс. рублей, поскольку объём указан в тысячах баррелей.
+ После оценки рисков нужно оставить лишь те регионы, в которых вероятность убытков меньше 2.5%. Среди них выбирают регион с наибольшей средней прибылью.

Данные синтетические: детали контрактов и характеристики месторождений не разглашаются.

## Направление деятельности
<svg width="100%"><foreignObject x="0" y="0" width="100%" height="160"><div style="display: flex; flex-wrap: wrap;"><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(110, 54, 48); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Машинное обучение</div></div><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(90, 90, 90); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Регрессия</div></div></div></foreignObject></svg>

## Навыки и инструменты
<svg width="100%"><foreignObject x="0" y="0" width="100%" height="160"><div style="display: flex; flex-wrap: wrap; padding-top: 8px; padding-bottom: 2px;"><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(137, 99, 42); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Pandas</div></div><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(137, 99, 42); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Scikit-learn</div></div><div style="display: flex; align-items: center; flex-shrink: 1; min-width: 0px; max-width: 100%; height: 20px; border-radius: 3px; padding-left: 6px; padding-right: 6px; font-size: 14px; line-height: 120%; color: rgba(255, 255, 255, 0.804); background: rgb(110, 54, 48); margin: 0px 6px 6px 0px;"><div style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; display: inline-block; height: 20px; line-height: 20px;">Бутстреп</div></div></div></foreignObject></svg>