### Соревнование **[Sibur challange 2020](https://sibur.ai-community.com/competitions/4)**, задача 2.

Содержит два решения:
1. [Решение](https://github.com/vilka-lab/sibur_2020_2/tree/master/0.6209) в рамках соревнования на [36](https://sibur.ai-community.com/competitions/4/tasks/12/rating) место (0.6268 на привате) из 195. 
Решение приводится как есть, без правок по завершению соревнований.
2. [Решение](https://github.com/vilka-lab/sibur_2020_2/tree/master/0.8248) в рамках работы над ошибками (0.8248 место на привате), это примерно 7 место. 

Основные концепции во втором решении:
- Исправлена система валидации. Основной причиной низкого скора явилась кривая система валидации, которая не детектировала оверфит. 
Составлены словари по отрицательным и положительным классам. По отрицательным (не совпадающие пары) - общие слова в паре, по положительным - различные в парах слова.
Затем после общей предобработки (за нее спасибо https://github.com/andrwvrn/SiburChallenge2020), убираем общие слова по отрицательным парам и распределяем получившиеся
компоненты на две выборки так, чтобы они не пересекались. Такая валидация хорошо справляется с детектированием переобучения, коррелирует с паблик скором и отсекает большинство бесполезных фичей.
Словари с общими и различающимися словами затем используются для предобработки пар перед расчетом мер сходства.
- Для довольно высокого скора достаточно всего двух фичей - расстояния Левенштейна и [коэффициента Жаккара](https://en.wikipedia.org/wiki/Jaccard_index), их вариаций 
по различным вариантам предобработки строк. 
- Для более высокого скора нужно взять топ-K пар (K~1600) по предсказанной вероятности, поскольку доля положительного класса в тестовой выборке примерно соответствует доле в трейновой.
Также есть пространство для дальнейшего тюнинга модели Catboost и их микса с различным random state.
