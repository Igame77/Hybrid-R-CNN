Hybrid-R-CNN
============

Гибридная реализация Faster R-CNN для задачи детекции объектов с раздельным обучением RPN, классификатора и регрессора, а также экспортом модели в TFLite для последующего деплоя. [github](https://github.com/Igame77/Hybrid-R-CNN)

Проект использует модифицированный RPN с дополнительным плотным слоем, инициализированным весами линейной модели Ridge, что улучшает обучаемость генератора предложений боксов и согласованность с L2‑регуляризацией. [github](https://github.com/Igame77/Hybrid-R-CNN)

Возможности
-----------

- Обучение **RPN** (Region Proposal Network) для генерации кандидатов областей с добавленным Dense‑слоем, в который загружаются заранее обученные веса Ridge‑регрессии по координатам bbox. [github](https://github.com/Igame77/Hybrid-R-CNN)
- Обучение отдельного классификатора по ROI‑признакам, полученным из предложений RPN. [github](https://github.com/Igame77/Hybrid-R-CNN)
- Обучение отдельного регрессора для уточнения координат боксов поверх предложений RPN. [github](https://github.com/Igame77/Hybrid-R-CNN)
- Возможность обучать Ridge‑часть генератора bbox с MSE‑функцией потерь и L2‑регуляризацией отдельно от основной CNN‑части (Adam + CIoU), а затем переносить веса в RPN. [github](https://github.com/Igame77/Hybrid-R-CNN)
- Работа в среде Jupyter Notebook (отдельные ноутбуки под каждый этап пайплайна). [github](https://github.com/Igame77/Hybrid-R-CNN)
- Готовые сохранённые веса моделей (`*.h5`) и экспортированная TFLite‑модель (`model.tflite`) для инференса без дообучения. [github](https://github.com/Igame77/Hybrid-R-CNN)

Особенности RPN и Ridge‑инициализации
-------------------------------------

- В RPN добавлен дополнительный **Dense**‑слой над признаковым пространством, который играет роль внутреннего генератора «простых идей» о bbox и аппроксимирует линейную Ridge‑модель. [github](https://github.com/Igame77/Hybrid-R-CNN)
- Веса этого слоя инициализируются из отдельно обученного Ridge‑регрессора по координатам якорей/gt‑боксов с функцией потерь MSE и L2‑регуляризацией, а не напрямую через CIoU. [github](https://github.com/Igame77/Hybrid-R-CNN)
- Такой подход позволяет:
  - стабилизировать начальное распределение предложений RPN за счёт линейной модели, уже адаптированной к L2‑штрафу; [github](https://github.com/Igame77/Hybrid-R-CNN)
  - упростить ландшафт оптимизации для дальнейшего дообучения CNN‑части RPN на Adam с более сложной метрикой (CIoU или её вариации); [github](https://github.com/Igame77/Hybrid-R-CNN)
  - ускорить схождение и уменьшить количество деградирующих локальных минимумов при обучении энд‑ту‑энд. [github](https://github.com/Igame77/Hybrid-R-CNN)

Структура репозитория
---------------------

- `notebooks/RPN_MODEL.ipynb` — обучение и/или инференс модифицированного RPN, загрузка Ridge‑весов в Dense‑слой, генерация предложений боксов. [github](https://github.com/Igame77/Hybrid-R-CNN)
- `notebooks/Classifier.ipynb` — обучение классификатора по предложениям RPN и ROI‑фичам. [github](https://github.com/Igame77/Hybrid-R-CNN)
- `notebooks/Regressor.ipynb` — обучение регрессора для уточнения координат bbox поверх предложений RPN. [github](https://github.com/Igame77/Hybrid-R-CNN)
- `RPN_MODEL.h5` — сохранённая модель RPN. [github](https://github.com/Igame77/Hybrid-R-CNN)
- `base_classifier.h5`, `classifier.h5`, `best_base_weights.h5`, `best_classifier_weights.h5` — сохранённые веса базового и финального классификатора. [github](https://github.com/Igame77/Hybrid-R-CNN)
- `model.tflite` — TFLite‑версия итоговой модели для деплоя. [github](https://github.com/Igame77/Hybrid-R-CNN)
- `requirements.txt` — список зависимостей. [github](https://github.com/Igame77/Hybrid-R-CNN)
- `pyproject.toml` — минимальная мета‑информация о проекте и конфигурация сборки. [github](https://github.com/Igame77/Hybrid-R-CNN)

Установка
---------

Рекомендуется использовать Python 3.13 (см. `pyproject.toml`). [github](https://github.com/Igame77/Hybrid-R-CNN)

```bash
git clone https://github.com/Igame77/Hybrid-R-CNN.git
cd Hybrid-R-CNN

python -m venv .venv
source .venv/bin/activate
# Windows: .venv\Scripts\activate

pip install -r requirements.txt
```

Быстрый старт
-------------

1. Подготовьте датасет с аннотациями bbox (формат и примеры см. в ноутбуках в каталоге `notebooks`). [github](https://github.com/Igame77/Hybrid-R-CNN)
2. Обучите или обновите Ridge‑модель для координат bbox и экспортируйте её веса в формат, используемый Dense‑слоем RPN. [github](https://github.com/Igame77/Hybrid-R-CNN)
3. Запустите `RPN_MODEL.ipynb`, загрузите Ridge‑веса в Dense‑слой и дообучите RPN на выбранной функции потерь (например, CIoU‑ориентированной). [github](https://github.com/Igame77/Hybrid-R-CNN)
4. Обучите классификатор (`Classifier.ipynb`) и регрессор (`Regressor.ipynb`) на предложениях RPN. [github](https://github.com/Igame77/Hybrid-R-CNN)
5. Экспортируйте финальную модель в TFLite (`model.tflite`) и используйте её для инференса на целевом устройстве. [github](https://github.com/Igame77/Hybrid-R-CNN)