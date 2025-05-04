## Описание проекта

Программа создает графическое окно с сеткой клеток, моделирующих игру "Жизнь". Пользователь может:
- Запускать и останавливать симуляцию
- Выполнять симуляцию пошагово
- Генерировать случайное начальное состояние

## Основные компоненты программы

### 1. Окно программы
- Создание главного окна с помощью `tkinter.Tk()`
- Установка заголовка окна

### 2. Холст для рисования (Canvas)
- Создание виджета `tkinter.Canvas` для отображения сетки
- Настройка размеров холста (например, 600x400 пикселей)

### 3. Сетка (логическая и визуальная)
- **Логическая сетка**: список списков `[[0, 1, ...], ...]` для хранения состояния клеток
- **Визуальная сетка**: прямоугольники на холсте Canvas с сохранением их идентификаторов
- Размер клетки в пикселях (например, `CELL_SIZE = 10`)
- Автоматический расчет размеров сетки на основе размеров холста

### 4. Начальное состояние
- Функция для случайного заполнения сетки
- Обновление отображения в соответствии с логической сеткой

### 5. Логика игры
- Подсчет соседей для каждой клетки
- Правила перехода к следующему поколению:
  - Живая клетка с менее чем 2 живыми соседями умирает (одиночество)
  - Живая клетка с 2 или 3 живыми соседями выживает
  - Живая клетка с более чем 3 живыми соседями умирает (перенаселение)
  - Мертвая клетка с ровно 3 живыми соседями оживает (размножение)

### 6. Управление и анимация
- Кнопки "Start/Stop", "Randomize", "Step"
- Логика запуска и остановки симуляции
- Пошаговое выполнение симуляции
- Генерация случайного состояния

## Примеры кода

### функции, которые нужно реализовать

```python
def count_neighbors(grid, row, col):
    """Подсчитывает количество живых соседей для клетки (row, col)."""
```

```python
def calculate_next_generation(current_grid):
    """Вычисляет следующее поколение логической сетки."""
```


```python
def create_grids():
    """Создает логическую сетку и сетку ID для холста."""
```


```python
def draw_grid_on_canvas():
    """Рисует сетку из прямоугольников на холсте."""
```


```python
def update_visuals():
    """Обновляет цвета клеток на холсте в соответствии с логической сеткой."""
```

```python
def randomize_grid():
    """Заполняет логическую сетку случайно и обновляет холст."""
```

```python
def clear_grid():
    """Очищает сетку (делает все клетки мертвыми)."""
```

```python
def handle_cell_click(event, row, col):
    """Обрабатывает клик по клетке (только если симуляция остановлена)."""
```

```python
def simulation_step():
    """Выполняет один шаг симуляции и планирует следующий."""
```

```python
def perform_single_step():
    """Выполняет только один шаг симуляции (для кнопки Step)."""
```

```python
def toggle_simulation():
    """Запускает или останавливает симуляцию."""
```

```python
# --- Настройка GUI ---
def setup_gui():
    global root, canvas, start_stop_button

    root = tk.Tk()
    root.title("Игра 'Жизнь' на Python/Tkinter")

    # Создаем холст
    canvas = tk.Canvas(root, width=CANVAS_WIDTH, height=CANVAS_HEIGHT, bg=COLOR_DEAD)
    canvas.pack(pady=10) # pack размещает виджет, pady добавляет отступ

    # Создаем логическую и визуальную сетки
    create_grids()
    draw_grid_on_canvas() # Рисуем клетки на холсте

    # Создаем фрейм для кнопок
    button_frame = tk.Frame(root)
    button_frame.pack(pady=5)

    # Кнопка Start/Stop
    start_stop_button = tk.Button(button_frame, text="Start", width=10, command=toggle_simulation)
    start_stop_button.pack(side=tk.LEFT, padx=5)

    # Кнопка Step
    step_button = tk.Button(button_frame, text="Step", width=10, command=perform_single_step)
    step_button.pack(side=tk.LEFT, padx=5)

    # Кнопка Randomize
    random_button = tk.Button(button_frame, text="Randomize", width=10, command=randomize_grid)
    random_button.pack(side=tk.LEFT, padx=5)

    # Кнопка Clear
    clear_button = tk.Button(button_frame, text="Clear", width=10, command=clear_grid)
    clear_button.pack(side=tk.LEFT, padx=5)

# --- Запуск ---
if __name__ == "__main__":
    setup_gui()
    root.mainloop() # Запускаем главный цикл Tkinter
```
