# Classical Four-Part Voice Leading

## Fundamental Principles

### Four Voices
- **S** (Soprano) — highest, melody carrier
- **A** (Alto) — inner voice
- **T** (Tenor) — inner voice
- **B** (Bass) — lowest, harmonic foundation

### Movement Types
1. **Прямое движение** (parallel) — voices move in same direction
2. **Противоположное движение** (contrary) — voices move in opposite directions
3. **Косвенное движение** (oblique) — one voice holds, other moves

---

## Voice Movement Restrictions

### Forbidden Parallels
- **Параллельные квинты** (parallel fifths) — categorically forbidden
- **Параллельные октавы** (parallel octaves) — categorically forbidden
- **Параллельные унисоны** (parallel unisons) — forbidden
- Exception: скрытые (hidden) fifths/octaves допустимы при плавном движении верхнего голоса

### Resolution Rules
- **Вводный тон** (leading tone, VII) — resolves UP by semitone to tonic
- **Септима** (seventh) — resolves DOWN by step
- **Нона** (ninth) — resolves DOWN by step
- At **прерванный каданс** (deceptive cadence V → VI): третья VI ступени удваивается

---

## Cadence Types

### Полная совершенная каденция (Perfect Authentic Cadence)
- S → D → T (IV → V → I)
- Bass on tonic root, melody on tonic root
- Strongest closure

### Полная несовершенная каденция (Imperfect Authentic Cadence)
- D → T (V → I)
- Bass or melody NOT on root
- Weaker closure

### Половинная каденция (Half Cadence)
- Ends on D (V)
- No resolution, creates tension

### Плагальная каденция (Plagal Cadence)
- S → T (IV → I)
- "Amen" cadence

### Прерванная каденция (Deceptive Cadence)
- D → VI (V → VI instead of expected V → I)
- Терция VI ступени удваивается (third of VI chord is doubled)

---

## Modulation Principles

### Диатоническая модуляция
- Through **посредствующий аккорд** (common chord) of both keys
- Then **модулирующий аккорд** (modulating chord) — usually dominant of new key
- Smooth voice leading in upper 3 voices

### Хроматическая модуляция
- Through altered/chromatic chords
- More dramatic

### Энгармоническая модуляция
- Through enharmonic reinterpretation
- **Уменьшённый септаккорд** (dim7) = 3 different dim7 chords enharmonically
- Each can resolve to **4 different keys** (each interval as seventh)
- Мощнейшее средство далёких модуляций (most powerful for distant modulations)

---

## Triads and Main Functions

### Трезвучия главных ступеней (I, IV, V)
- **T** (тоника) — tonic, I degree
- **S** (субдоминанта) — subdominant, IV degree
- **D** (доминанта) — dominant, V degree
- Form the foundation of tonality

### Трезвучия побочных ступеней (II, III, VI, VII)
- **II ступень** — subdominant function (often replaces IV)
- **VI ступень** — tonic group (used in deceptive cadence)
- **III ступень** — connector between T and D
- **VII ступень** — уменьшённое трезвучие (diminished triad), dominant function (D7 without root)

---

## Voice Connection Rules

### Гармоническое соединение (Common Tone Connection)
- When chords share a common tone
- Common tone stays in the same voice
- Other voices move to nearest chord tones

### Мелодическое соединение (Stepwise Connection)
- When chords have no common tone (e.g., IV → V, V → VI)
- Upper voices move **противоположно** басу (contrary to bass)
- Special rule for V → VI: double the third of VI chord

---

## Doubling Guidelines

### Трезвучия (Triads)
- Most often: double **прима** (root)
- In секстаккорд (first inversion): free doubling except leading tone
- Never double leading tone (вводный тон)

### Квартсекстаккорд (Second Inversion)
- Least stable position
- Used in specific contexts:
  - **Кадансовый** (cadential 6/4): I6/4 before V
  - **Проходящий** (passing 6/4)

---

## Practical Application to MIDI

### Voice Leading Checker Algorithm
1. Check for parallel fifths/octaves between all voice pairs
2. Verify leading tone resolution (VII → I)
3. Verify seventh resolution (down by step)
4. Check for proper doubling in triads

### Cadence Templates
- Store MIDI patterns for all 5 cadence types
- Transpose to any key
- Auto-insert at phrase endings

### Modulation Algorithm
1. Analyze current key
2. Find common chord with target key
3. Generate modulating dominant
4. Verify smooth voice leading in upper voices
