# Проект "Распознавание дорожных знаков"

Наш проект посвящён распознаванию и классификации дорожных знаков.

## Постановка бизнес-задачи

**Кому и как это может пригодиться?**

- водителю как расширение функциональности автомобиля: подаётся видео с камеры заднего/переднего вида или видеорегистратора; на выходе голосовая информация об обнаружении дорожных знаков
- расширение функциональности навигаторов и карт: наше решение нужно для ускорения работы картографов, которые наносят на карты информацию о дорожных знаках. На вход подаются кадры, заснятые видеорегистратором, нужно на них детектировать и классифицировать знаки

## ML-решение

### Общий пайплайн

Мы рассматривали 2 возможных варианта пайплайна обработки:

1. Входной кадр → Детектор (многоклассовый на все типы дорожных знаков) → Найденные знаки с координатами bbox-а и меткой

2. Входной кадр → Детектор (только 1 класс: road sign) → Кропы с дорожными знаками → Классификатор → Найденные знаки с координатами bbox-а и меткой

Идея реализации второго варианта пайплайна состоит в том, чтобы перенести борьбу с проблемой несбалансированностью классов на этап классификатора, на уровне которого её легче решать.

В рамках наших экспериментов по обучению моделей были опробованы оба варианта пайплайна.

### Используемый датасет

Для обучения, валидации и тестирования моделей мы использовали датасет с российскими дорожными знаками RTSD:

- [kaggle](https://www.kaggle.com/datasets/watchman/rtsd-dataset),
- [статья](https://computeroptics.ru/eng/KO/PDF/KO41-ENG%20-17/400221.pdf).

После проведённого нами анализа данного датасета ([eda](https://github.com/Shchetinnikov/Data_Centric_AI_course/blob/main/hw_1/notebooks/eda.ipynb)) были выявлены следующие проблемы:

- есть много редких классов,
- наблюдается несбалансированность между разными классами.

Поэтому датасет, использующийся в экспериментах, был модифицирован относительно исходного: ...

Модифицированный датасет был выложен на kaggle: [our_dataset](https://www.kaggle.com/datasets/4991145816988d062fe6bb2db9298c816cd9f63f60d325635ecb82da77c9e760).

### Экcперименты по обучению моделей

1. **Первый вариант пайплайна:** была обучена детекционная модель yolov8 на всех классах дорожных знаков.

2. **Второй вариант пайплайна:** были отдельно обучены детекционная модель yolov8 с одним классом road_sign и классификационная модель yolov8.

### Итоговый выбор модели и пайплайна

...

## Веб-сервис

Для демонстрации работы приложения был реализован веб-сервис на streamlit: [web-service](https://github.com/DL-teammm/web_service). Его можно запустить локально, загрузить тестовое видео и посмотреть, как работает на нём наше решение.

### Демо

...
