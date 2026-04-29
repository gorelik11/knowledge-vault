# Taneev — Practical Rules for MIDI Composition

## Interval Numbering System

**Unit of measurement:** секунда (second/step)

Each interval = цифра на единицу меньшей общепринятого названия:
- Прима = **0**
- Секунда = **1**
- Терция = **2**
- Кварта = **3**
- Квинта = **4**
- Секста = **5**
- Септима = **6**
- Октава = **7**

---

## Two Groups of Intervals

### Ľint (первая группа): 0, 3, 4, 7
- Appear in 3 forms: чистые, увеличенные, уменьшенные
- Perfect consonances: 0 (прима), 3 (кварта), 4 (квинта), 7 (октава)

### ²int (вторая группа): 1, 2, 5, 6
- Appear in 4 forms: большие, малые, увеличенные, уменьшенные
- Imperfect consonances: 2 (терция), 5 (секста)

---

## Vertical Movable Counterpoint (Jᵥ)

### Basic Formula: **m + Jᵥ = n**
- **m** = первоначальный интервал (original interval)
- **Jᵥ** = показатель (index of transposition)
- **n** = производный интервал (resulting interval)

### Key Implications
- If m = 0, then n = Jᵥ (прима → интервал равный показателю)
- If m = -Jᵥ, then n = 0 (интервал равный показателю с обратным знаком → прима)
- In двойной контрапункт: производный становится первоначальным и обратно

---

## Types of Permutations

### Прямая перестановка (═)
- Voices retain relative position (upper remains upper)
- Always when **Jᵥ > 0**

### Противоположная перестановка (╳)
- Voices exchange position (двойной контрапункт)
- When **Jᵥ < 0** and **m < |Jᵥ|**

### Смешанная перестановка (═╳)
- Partly прямая, partly противоположная

---

## Stable Intervals (устойчивые интервалы)

### Устойчивые консонансы
- Первоначальный консонанс = производный консонанс
- Таблица для каждого Jᵥ показывает, какие консонансы сохраняются

**Best Jᵥ for maximum stability:**
- **Jᵥ = -9** (двойной контрапункт децимы): ВСЕ консонансы устойчивые
- **Jᵥ = -11** (двойной контрапункт дуодецимы): почти все консонансы устойчивые
- **Jᵥ = -7** (двойной контрапункт октавы): несколько неустойчивых консонансов

### Устойчивые диссонансы
- Первоначальный диссонанс = производный диссонанс
- Сохраняют свои правила разрешения
- При **Jᵥ = -11**: децима не может диссонировать нижней нотой
- При **Jᵥ = -9**: кварта и септима не могут быть связанными (знак ○─○)

---

## Doubling by Imperfect Consonances (Удвоения)

### Principle
- Каждое удвоение = вертикальное передвижение на терцию/сексту/дециму
- 2-голосие → 3-голосие или 4-голосие

### Notation
- **Iᵃ⁼⁻⁹** = голос I + его удвоение на -9 (дециму вниз)
- **I + IIᵃ⁼⁻⁹** = верхний на месте, нижний удвоен дециму вниз

### Additional Conditions
- **Правило ноны (B)**: нона, разрешающаяся в октаву, исключается
- **Правило кварты (C)**: кварта между верхними голосами может быть консонансом

---

## Horizontal Movable Counterpoint (Jₕ)

### Formula: **a + Jₕ = h**
- **a** = первоначальное соединение (original combination)
- **Jₕ** = показатель горизонтального передвижения (в тактах или долях)
- **h** = производное соединение (resulting combination)

### Combined Formula (Вдвойне-подвижной): **a + Jₕ + Jᵥ = h**
- Одновременное вертикальное и горизонтальное передвижение
- Максимальная вариативность материала

---

## Rules of Strict Counterpoint (Строгий стиль)

### Consonances
- **Несовершенные консонансы** (терции, сексты): без ограничений в параллельном движении
- **Совершенные консонансы** (октавы, квинты, унисоны): запрещены параллельные последования

### Dissonances
- **Проходящие и вспомогательные**: на слабых долях
- **Связанные (синкопированные)**:
  - Приготовление на слабой доле
  - Диссонирование на сильной доле
  - Разрешение на слабой доле

### Voice Movement
- Диссонирующая нота (знак ─): может быть в верхнем или нижнем голосе
- Свободная нота: движется на соседнюю ступень при разрешении

### Кварта
- В многоголосном контрапункте: между верхними голосами может быть консонансом
- **Квартсекстаккорд допустим** при правильном приготовлении и разрешении как диссонанс

---

## Triple Counterpoint (Трёхголосный)

### Voice Labels
- **I** (сопрано), **II** (альт), **III** (тенор)

### Indicators
- **Jᵥ'** (между I и II)
- **Jᵥ''** (между I и III)
- Их взаимное отношение

### Rules
- **Правило ноны**: в производном исключаются ноны, разрешающиеся в октаву
- **Правило кварты**: кварта между верхними голосами может быть консонансом при определённых условиях
- Многоголосный контрапункт = совокупность двухголосных (проверка парами)

---

## Key Formulas Summary

1. **m + Jᵥ = n** — основная формула вертикально-подвижного контрапункта
2. **a + Jₕ = h** — формула горизонтально-подвижного контрапункта
3. **Jᵥ** = алгебраическая сумма vv двух голосов
4. **Jₕ** = алгебраическая сумма hh двух голосов (в тактах/долях)

---

## MIDI Application

### Vertical Transposition
1. Write 2-voice counterpoint in one octave
2. Transpose one voice by Jᵥ (e.g., -9 for decima down)
3. Check table of stable intervals for chosen Jᵥ
4. If all intervals stable → valid permutation

### Horizontal Shift
1. Shift voice by Jₕ in time (measures or beats)
2. Results in canon/stretto effect
3. Check that intervals remain valid at new alignment

### Doubling
1. Duplicate voice at -9 (decima down) or -16 (double-octave + ninth down)
2. Creates 3-voice texture from 2-voice
3. Check Правило ноны (B) and Правило кварты (C)

### Combined (Doubly Movable)
1. Apply both Jᵥ and Jₕ simultaneously
2. Maximum variation from single 2-voice original
3. Formula: **a + Jₕ + Jᵥ = h**

---

## Popular Jᵥ Values for MIDI

- **Jᵥ = -7**: двойной контрапункт октавы (classic, straightforward)
- **Jᵥ = -9**: двойной контрапункт децимы (best stability, popular in jazz)
- **Jᵥ = -11**: двойной контрапункт дуодецимы (very stable)
- **Jᵥ = 2, -7, -9**: тройной показатель (one original → 3 permutations)

---

## Workflow in REAPER/DAW

1. Write cantus firmus (основная мелодия) in Track 1
2. Add контрапункт in Track 2
3. Duplicate Track 2 for производные
4. Transpose duplicates by Jᵥ (using DAW transpose function)
5. Time-shift duplicates by Jₕ (using DAW time-shift)
6. Verify by checking intervals against stability tables
