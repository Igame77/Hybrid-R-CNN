<<<<<<< HEAD
# Hybrid-R-CNN

Гибридная реализация Faster R-CNN для задачи детекции объектов с раздельным обучением RPN, классификатора и регрессора, а также экспортом модели в TFLite для последующего деплоя.

## Возможности

- Обучение **RPN** (Region Proposal Network) для генерации кандидатов областей.
- Обучение отдельного классификатора по ROI-признакам.
- Обучение отдельного регрессора для уточнения координат боксов.
- Работа в среде Jupyter Notebook (отдельные ноутбуки под каждый этап).
- Готовые сохранённые веса моделей (`*.h5`) и экспортированная TFLite-модель (`model.tflite`) для инференса без дообучения.[page:1]

## Структура репозитория

- `RPN_MODEL.ipynb` — обучение и/или инференс RPN.
- `Classifier.ipynb` — обучение классификатора по предложениям RPN.
- `Regressor.ipynb` — обучение регрессора для уточнения bbox.
- `RPN_MODEL.h5` — сохранённая модель RPN.
- `base_classifier.h5`, `classifier.h5`, `best_base_weights.h5`, `best_classifier_weights.h5` — сохранённые веса базового и финального классификатора.
- `model.tflite` — TFLite-версия итоговой модели для деплоя.
- `requirements.txt` — список зависимостей.
- `pyproject.toml` — минимальная мета‑информация о проекте и конфигурация сборки.[page:1][page:2]

## Установка

Рекомендуется использовать Python 3.13 (см. `pyproject.toml`).[page:2]

```bash
git clone https://github.com/Igame77/Hybrid-R-CNN.git
cd Hybrid-R-CNN
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
=======
# Hybrid-R-CNN

Гибридная реализация Faster R-CNN для задачи детекции объектов с раздельным обучением RPN, классификатора и регрессора, а также экспортом модели в TFLite для последующего деплоя.

## Возможности

- Обучение **RPN** (Region Proposal Network) для генерации кандидатов областей.
- Обучение отдельного классификатора по ROI-признакам.
- Обучение отдельного регрессора для уточнения координат боксов.
- Работа в среде Jupyter Notebook (отдельные ноутбуки под каждый этап).
- Готовые сохранённые веса моделей (`*.h5`) и экспортированная TFLite-модель (`model.tflite`) для инференса без дообучения.[page:1]

## Структура репозитория

- `RPN_MODEL.ipynb` — обучение и/или инференс RPN.
- `Classifier.ipynb` — обучение классификатора по предложениям RPN.
- `Regressor.ipynb` — обучение регрессора для уточнения bbox.
- `RPN_MODEL.h5` — сохранённая модель RPN.
- `base_classifier.h5`, `classifier.h5`, `best_base_weights.h5`, `best_classifier_weights.h5` — сохранённые веса базового и финального классификатора.
- `model.tflite` — TFLite-версия итоговой модели для деплоя.
- `requirements.txt` — список зависимостей.
- `pyproject.toml` — минимальная мета‑информация о проекте и конфигурация сборки.[page:1][page:2]

## Установка

Рекомендуется использовать Python 3.13 (см. `pyproject.toml`).[page:2]

```bash
git clone https://github.com/Igame77/Hybrid-R-CNN.git
cd Hybrid-R-CNN
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
>>>>>>> 8c4d5f0aab539793ea203898703091917b87405c
