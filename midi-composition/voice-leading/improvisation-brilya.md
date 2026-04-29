# Brilya (Bril) — Practical Rules for MIDI Composition

## Five Types of 7th Chords on Scale Degrees

### Notation
- **M** (заглавная) = большой мажорный 7-аккорд (maj7)
- **m** (строчная) = минорный 7-аккорд (m7)
- **x** = малый мажорный 7-аккорд (доминантовый, 7)
- **o** = уменьшённый 7-аккорд (dim7)
- **ø** = малый вводный 7-аккорд (полууменьшённый, m7b5)

### Diatonic 7th Chords in Major
- **I и IV ступени** → IM, IVM (большой мажорный)
- **II, III, VI ступени** → IIm, IIIm, VIm (малый минорный)
- **V ступень** → Vx (малый мажорный/доминантовый)
- **VII ступень** → VIIø (малый вводный), VIIo in harmonic major (уменьшённый)

---

## Voicing Forms A, B, C

### Form A
- **Терция внизу, септима наверху**
- Example: Dm7 → D (bass), F-A-C (3rd bottom, 7th top)

### Form B
- **Септима внизу, терция наверху**
- Example: Dm7 → D (bass), C-F-A (7th bottom, 3rd top)

### Form C
- **Комбинированная**
- Mixed positions for voice leading

### Voice Leading Principle
- **Минимальное движение голосов** (minimal voice movement)
- Формы A, B, C чередуются для плавного голосоведения
- Общие звуки остаются на месте

---

## ii-V-I Progression (Fundamental Oborot)

### Major: IIm - Vx - IM
- Example in C major: Dm7 - G7 - Cmaj7
- Form sequence: B → A → B (or A → B → A depending on register)

### Minor: IIø - Vx - Im
- Example in A minor: Bm7b5 - E7 - Am7
- Dorian mode on IIø, harmonic minor on Vx

### Alteration
- Альтерация квинты (b5, #5) в Vx → **целотонная гамма**
- Example: G7b5, G7#5 → whole-tone scale (G-A-B-C#-D#-F)

---

## Mode-to-Chord Correspondence Table

| Аккорд | Лад |
|--------|-----|
| IM | Ионийский (Ionian, натуральный мажор) |
| IIm | Дорийский (Dorian) |
| IIIm | Фригийский (Phrygian) |
| IVM | Лидийский (Lydian) |
| Vx | Миксолидийский (Mixolydian) |
| VIm | Эолийский (Aeolian, натуральный минор) |
| VIIø | Локрийский (Locrian) |
| VIIo | Уменьшённый (Diminished, тон-полутон) |

---

## Diminished Scale (Уменьшённый лад)

### Structure
- **Тон-полутон чередование** (tone-semitone alternation, octatonic)
- Example from C: C-D-Eb-F-Gb-Ab-A-B-C

### Three Positions
- From C, Db, D → все остальные звуки повторяются

### Usage
- Для **уменьшённого (o)** аккорда
- Для **доминантового (x)** с альтерацией (b5, b9, #9, #11)

---

## Whole-Tone Scale (Целотонная гамма)

### Usage
- При альтерации квинты (b5, #5) в x-аккорде
- Example: G7b5 → G-A-B-C#-Eb-F

---

## 3rd/7th Alternation (Left Hand Comping)

### Fast Tempo Technique (Bud Powell style)
- В левой руке: чередование терции и септимы
- **Терция** → малый мажорный или большой мажорный 7-аккорд
- **Септима** → малый минорный или малый мажорный 7-аккорд
- Экономичный аккомпанемент для быстрых темпов

### Example: Dm7 - G7 - Cmaj7
- Dm7: play F (3rd)
- G7: play F (7th)
- Cmaj7: play E (3rd)

---

## Form AABA (32-bar standard)

### Structure
- **A** (8 bars) + **A** (8 bars) + **B** (bridge, 8 bars) + **A** (8 bars)
- Total: 32 bars
- B section usually modulates or introduces contrasting harmony

### Example: Oleo (Sonny Rollins)
- A: I-VI-II-V progression in Bb major
- A: repeat
- B: modulation to IV, different harmonic rhythm
- A: return to I

---

## Harmonic Enrichment

### Проходящие 7-аккорды (Passing Chords)
- Между септаккордами на расстоянии тона → **уменьшённый вводный (o)** при восходящем движении
- Хроматический проходящий при нисходящем движении

### Tritone Substitution
- Замена Vx → bIIx
- Example: G7 → Db7 (in C major)
- Shares 3rd and 7th (enharmonically)

### Subdominant Tritone Substitution
- Замена IIm → bIIx
- Example: Dm7 → Db7 (approaching Cmaj7)

---

## Six Basic Progressions (Урок 1 — играть в 12 тональностях)

1. **IM - IVM**
2. **IIm - IIIm - VIm**
3. **Vx - VIIø - VIIo - IM**
4. **IIm - Vx - IM** (core ii-V-I)
5. **IM - VIm - IIm - Vx - IM** (circle progression)
6. **IM - IVM - IIIm - IIm - IM - IVM - VIIø - VIIo - IM** (full diatonic sequence)

---

## MIDI Workflow Application

### Voicing Templates for REAPER
1. Create MIDI template for Form A voicings (3-7 structure)
2. Create MIDI template for Form B voicings (7-3 structure)
3. Lua script: auto-select form based on previous chord to minimize movement

### Mode Selection Algorithm
1. Read chord symbol from MIDI track
2. Look up mode in correspondence table
3. Generate scale notes for improvisation
4. Filter to match chord tones + tensions

### ii-V-I Generator
1. Input: target key
2. Output: MIDI notes for IIm7 → V7 → Imaj7
3. Apply Form B → A → B voicings
4. Transpose to all 12 keys for practice

### 3rd/7th Comping
1. Analyze chord progression
2. Extract 3rd and 7th of each chord
3. Alternate them in left-hand MIDI part
4. Quantize to quarter notes for walking feel

---

## Practical Exercises for MIDI

### Exercise 1: Transpose 6 Progressions
- Create MIDI file with 6 basic progressions
- Transpose each to all 12 keys
- Practice voice leading (forms A/B/C)

### Exercise 2: Oleo Analysis
- Input "Oleo" chord changes to MIDI track
- Mark form sections (A-A-B-A)
- Analyze each ii-V-I unit
- Generate voicings using minimal movement

### Exercise 3: Modal Improvisation
- Set up MIDI looper with single chord (e.g., Dm7)
- Generate Dorian scale notes
- Improvise melody using scale notes + chord tones
