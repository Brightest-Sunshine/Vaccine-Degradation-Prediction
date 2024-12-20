#  Исследование стабильности мРНК-вакцины для COVID-19

Пандемия **COVID-19** стала одним из самых значительных вызовов современности, затронув здоровье, экономику и социальную стабильность во всем мире. Для эффективной борьбы с вирусом была необходима разработка вакцины, способной предотвратить дальнейшее распространение инфекции. Благодаря многолетним исследованиям в области биомедицины, учёные смогли ускорить процесс разработки, что позволило создать вакцины в рекордно короткие сроки. Однако, несмотря на это, борьба с пандемией остаётся сложной задачей.

Наиболее перспективным решением стали **вакцины на основе мРНК (матричной РНК)**. Эта технология показала свою эффективность и позволила быстро адаптировать вакцины под новые штаммы вируса. Однако **мРНК-вакцины** сталкиваются с рядом серьёзных ограничений, которые сдерживают их массовое производство и глобальное распространение. 

![Описание молекулы: структура мРНК](https://github.com/Brightest-Sunshine/Vaccine-Degradation-Prediction/blob/master/images/mRNA.png)

Главная проблема заключается в **нестабильности молекулы мРНК**. РНК обладает склонностью к спонтанному разложению, и даже одно повреждение в молекуле может сделать вакцину неэффективной. Это приводит к необходимости хранения и транспортировки вакцин при **экстремально низких температурах**, что значительно усложняет их логистику. Многие регионы с ограниченной инфраструктурой просто не имеют возможности обеспечить такие условия хранения, из-за чего доступность вакцин для людей в удалённых и бедных регионах оказывается под угрозой.

Кроме того, на данный момент известно крайне мало о том:
- Какие **участки молекулы мРНК** наиболее подвержены разрушению
- Как можно повысить её **устойчивость**

Без этих знаний вакцины остаются:
- **Дорогостоящими в производстве**
- Требующими **сложной логистики** для транспортировки
- С ограниченным сроком хранения

Эта проблема требует **междисциплинарного подхода**. Необходимы исследования, направленные на:
1. **Разработку новых молекулярных конструкций мРНК**, обеспечивающих её стабильность
2. Применение **биоинформатики и методов машинного обучения** для анализа структуры мРНК и прогнозирования её поведения в различных условиях
3. Создание **инновационных технологий упаковки и доставки вакцин**, которые позволят защитить молекулу от разрушения

Решение задачи **стабильности мРНК** откроет новые горизонты в разработке вакцин, сделает их более **доступными** и **эффективными**. Это не только ускорит борьбу с **COVID-19**, но и станет основой для будущих успехов в **биомедицине** и **терапевтических инновациях**.

## Решение

Сообщество **Eterna**, под руководством профессора Риджу Даса, вычислительного биохимика из Медицинской школы Стэнфорда, объединяет ученых для решения научных задач. На платформе Eterna они решают головоломки, связанные с проектированием молекул РНК, а решения синтезируются и тестируются учеными в лабораториях Стэнфорда.

- Сообщество Eterna внесло вклад в более чем 20 публикаций, включая разработки в области РНК-биотехнологий.
- Игроки помогли открыть новые научные принципы, разработать диагностику для борьбы с опасными заболеваниями и внести вклад в развитие общественного блага.

Теперь Eterna стремится ускорить создание устойчивых мРНК-вакцин для борьбы с COVID-19.

![Eterna](https://github.com/Brightest-Sunshine/Vaccine-Degradation-Prediction/blob/master/images/eterna.png)

## Постановка задачи

**Цель**: разработать модель, которая будет прогнозировать показатели деградации мРНК для каждой позиции последовательности. Это включает предсказание трех целевых показателей:

1. **reactivity** (реактивность),
2. **deg_Mg_pH10** (деградация при pH 10),
3. **deg_Mg_50C** (деградация при температуре 50°C).

## Метрика оценки

Модель оценивается по метрике **MCRMSE** (*Mean Columnwise Root Mean Squared Error*), которая рассчитывается следующим образом:

$$
\text{MCRMSE} = \frac{1}{N_t} \sum_{j=1}^{N_t} \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_{ij} - \hat{y}_{ij})^2}
$$

Где:
- $N_t$ — количество целевых колонок (в данном случае 3: `reactivity`, `deg_Mg_pH10`, `deg_Mg_50C`),
- $n$ — количество позиций в последовательности,
- $y_{ij}$ — истинное значение для $i$-й позиции и $j$-й колонки,
- $\hat{y}_{ij}$ — предсказанное значение для $i$-й позиции и $j$-й колонки.

## Формат представления результатов

Для каждого образца (*sample id*) в тестовом наборе необходимо предсказать значения для каждой позиции последовательности (*seqpos*).

Файл должен иметь следующий формат:
- Столбцы: `id_seqpos`, `reactivity`, `deg_Mg_pH10`, `deg_Mg_50C`.
- Каждая строка соответствует позиции последовательности.

### Пример:
```plaintext
id_seqpos,reactivity,deg_Mg_pH10,deg_Mg_50C
id_00073f8be_0,0.1,0.3,0.2
id_00073f8be_1,0.3,0.2,0.5
id_00073f8be_2,0.5,0.4,0.2
```
