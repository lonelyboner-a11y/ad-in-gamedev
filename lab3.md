# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Садовский Савелий Евгеньевич
- НМТ-233511
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * |  |
| Задание 2 | # |  |
| Задание 3 | # |  |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
установить необходимое программное обеспечение. Рассмотреть процесс установки игрового движка Unity для разработки игр.

## Задание 1
- Задание 1. Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице.
Ход работы:

Для работы были выбраны следующие переменные: скорость дракона, частота спавна яиц и количество слоёв щита.
Автоматическое заполнение таблицы:

```py
import gspread
import numpy as np
import math
import matplotlib.pyplot as plt

gc = gspread.service_account(filename='untiry-c709765052a1.json')
sh = gc.open("Workshop3")

def write_indexes():
    for i in range(1, 12):
        sh.sheet1.update_acell("A" + str(i + 1), str(i))

def change_multiplier(multiplier, parameter):
    if parameter == "speed":
        literal = "B"
    else:
        literal = "C"
        multiplier = math.ceil(1 / multiplier * 100) / 100 
    
    current_value = float(sh.sheet1.acell(literal + "2").value)
    values = []
    for i in range(3, 13):
        current_value *= multiplier  # Умножение
        current_value = math.ceil(current_value * 100) / 100  # Округление до 2 знаков после запятой
        formatted_value = str(current_value).replace(".", ",")  # Форматирование
        sh.sheet1.update_acell(literal + str(i), formatted_value)  # Запись в ячейку
        values.append(current_value)
    return values

def shield(addiction):
    shieldcount = int(sh.sheet1.acell("D2").value)
    values = []
    if round(shieldcount*((1-addiction)**(11))) == 0:
        print("shildcount cannot be changed, taken value overly high")
        return
    for i in range(3, 13):
        val = round(shieldcount*((1-addiction)**(i-2)))
        sh.sheet1.update_acell("D" + str(i), str(val))
        values.append(val)
    return values


def plot_graphs(speed_values, eggs_values, shield_values):
    x = np.arange(1, 11)
    
    plt.figure(figsize=(12, 6))
    
    plt.subplot(1, 3, 1)
    plt.plot(x, speed_values, marker='o', linestyle='-', color='b', label='Speed')
    plt.xlabel('Iteration')
    plt.ylabel('Speed')
    plt.title('Speed Growth')
    plt.legend()
    
    plt.subplot(1, 3, 2)
    plt.plot(x, eggs_values, marker='s', linestyle='-', color='g', label='Eggs')
    plt.xlabel('Iteration')
    plt.ylabel('Eggs')
    plt.title('Eggs Growth')
    plt.legend()
    
    plt.subplot(1, 3, 3)
    plt.plot(x, shield_values, marker='^', linestyle='-', color='r', label='Shield')
    plt.xlabel('Iteration')
    plt.ylabel('Shield')
    plt.title('Shield Growth')
    plt.legend()
    
    plt.tight_layout()
    plt.show()

if __name__ == '__main__':
    speed_vals = change_multiplier(1.15, "speed")
    eggs_vals = change_multiplier(1.15, "eggs")
    shield_vals = shield(0.1)
    plot_graphs(speed_vals, eggs_vals, shield_vals)
```
Скриншот таблицы

![425746280-a787397a-2e56-49d6-93ec-f7decff99a72](https://github.com/user-attachments/assets/a723b9f9-aa69-4a9c-a198-9e32fc102fff)

## Выводы

Были предложены вариант изменения найденных переменных для 10 уровней в игре. Визуализированы изменение уровня сложности в таблице.

## Powered by

Абзац умных слов о том, что было сделано и что было узнано.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

**BigDigital Team: Denisov | Fadeev | Panov**
