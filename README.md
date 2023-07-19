# **OCR for DonorSearch**
В данном репозитории располагается ML-решение для автоматического извлечения информации с фотографий медицинских документов стандартного образца.

**Заказчик:** Сообщество доноров Крови "DonorSearch"

**Цель:** Автоматизировать перенос данных с фотографий медицинских справок донора в формат .csv.

**Задача:** Детектировать табличную часть справки, распознать текст и привести данные к требуемому шаблону.

**Модель:** В работе использовали Модель-NANONETSOCR

**Метрика:** Accuracy

### **Описание данных:**
- **Исходные данные:**
  - 16 фотографий медицинских справок с данными от доноров (унифицированная форма №405) для распознавания, 
  - 15 файлов с соответствующей инфрормцацией в формате .csv (для провыерки качества рабоы нашей модели)
- **Терминология** для итоговой распознанной таблицы:
  - **Класс крови:** Цельная кровь, Плазма, Тромбоциты. 
  - **Тип донации:** Безвозмездно.
- Колонки таблицы, которые заказчик обозначил, как самые важные и трудозатратные: 
  - Дата донации,
  - Класс крови,
  - Тип донации.

### **Описание проекта:**
Для реализации задачи использована **модель NANONETSOCR**.
- Проведено исследование модели **NANONETSOCR**,
- Разработана функция постобработки распознанных данных - распознанная таблица приводится в соответствующий формат.
  - Фрмируются рабочие колонки: 'Класс крови', 'Дата донации', 'Тип донации',
  - Все возможные сокращения преобразовываются в используемую терминологию необходимого итогового результата:
      - Цельная кровь = [кр / д]
      - Плазма = [пл / д, пп / д, п / ф]
      - Тромбоциты = [т / ф, ц / д]
      - Тип донации: Безвозмездно = [( бв )]
  - Дата донации: переводится в формат чч.мм.гггг,
  - Проводится очиства от лишних "шумов".
- Проведена оценка работоспособности полученного алгоритма, метрика **Accuracy**:
  - С помощью доработоной модели удалось получить общее **качество распознавания более 75,5%**.
  - Время полного цикла преобразований одного изображения занимает от 10 до 30 секунд.
