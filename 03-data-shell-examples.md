# What's in `shell-lesson-data`, and Optional Extra Examples

> **Purpose:** read this to decide if any of it is worth using. Nothing here is required. Everything uses files the lesson itself uses.
> **Caveat:** outputs marked "lesson" come straight from the lesson page. Anything else is my best description and you should run it once on your Mac before using it. Run the commands from `~/Desktop/shell-lesson-data` (or wherever yours lives).

---

## 1. The folder map

```
shell-lesson-data/
├── exercise-data/
│   ├── alkanes/         cubane.pdb ethane.pdb methane.pdb octane.pdb pentane.pdb propane.pdb
│   ├── animal-counts/   animals.csv
│   ├── creatures/       basilisk.dat minotaur.dat unicorn.dat
│   ├── numbers.txt
│   └── writing/         haiku.txt LittleWomen.txt
└── north-pacific-gyre/  NENE*A.txt  NENE*B.txt  NENE*Z.txt  goostats.sh  (plus others)
```

Which episode uses which data:

| Episode | Data used | Why |
|---|---|---|
| 2 Navigating | `exercise-data/` tree | Lots of folders to walk around |
| 3 Files & directories | `writing/`, `alkanes/` | Make/copy/move/delete; wildcard `*t??ne.pdb` |
| 4 Pipes & filters | `alkanes/*.pdb`, `animal-counts/animals.csv`, `north-pacific-gyre/` | `wc`, `sort`, `head`, `cut`, `uniq` |
| 5 Loops (not reached) | `creatures/*.dat`, `alkanes/` | `for` loops |
| 6 Scripts (not reached) | `alkanes/`, `north-pacific-gyre/` | `middle.sh`, `do-stats.sh` |
| 7 Finding things (not reached) | `writing/haiku.txt`, `LittleWomen.txt` | `grep`, `find` |

**The story:** the lesson's character, Nelle, is a researcher who must process 1520 sample files from a Pacific gyre. The simple files (alkanes, animals) are a practice playground; `north-pacific-gyre` is the "real" problem. That is relatable to your audience: "a pile of data files you need to check and process."

---

## 2. Extra examples you could slot in

### 2.1 Episode 2 (Navigating): a "get around by Tab" exercise (3 min)

Goal: practice Tab completion until it's habit.

```
cd
cd Desktop/shell-lesson-data/exercise-data/creatures
pwd
cd ../../north-pacific-gyre
pwd
ls | head
```
Ask: "How many Tab presses did you use?" (If someone typed everything, show them Tab.)
`ls | head` is a taste of Episode 4. Say "we'll learn that `|` later."

### 2.2 Episode 2: peek at a file with `ls -l`
In `exercise-data/writing`:
```
ls -lh
```
Point out: size column, date column. "Sizes in KB, because of `-h`." Good for researchers asking "how big is this file?"

### 2.3 Episode 3 (Files): `cat` and `less` to look inside
In `exercise-data/writing`:
```
cat haiku.txt
less LittleWomen.txt
```
`less`: space = next page, `q` = quit. "Don't `cat` a huge file."
(This is outside the strict lesson order, but people always ask "how do I look at a file?")

### 2.4 Episode 3: a safe "undo" demo of `rm`
```
cd ~/Desktop/shell-lesson-data/exercise-data/writing
touch scratch.txt
ls
rm scratch.txt
ls
```
Then: "Where did it go? Not in the trash. It's gone." Strong, short, memorable.

### 2.5 Episode 3: wildcard "predict first" game (5 min)
In `exercise-data/alkanes`, ask the room to **predict** before you run each:
```
ls *.pdb
ls c*
ls *ane.pdb
ls ?ethane.pdb
ls *p*
```
Reasonable expected outputs given the six file names (cubane, ethane, methane, octane, pentane, propane):
- `c*` → `cubane.pdb`
- `?ethane.pdb` → `methane.pdb`
- `*p*` → `pentane.pdb propane.pdb`
Predicting out loud keeps people engaged and reveals who's confused.

### 2.6 Episode 4 (Pipes): "which files are shortest/longest?"
In `exercise-data/alkanes`:
```
wc -l *.pdb | sort -n
wc -l *.pdb | sort -n | head -n 1
wc -l *.pdb | sort -n | tail -n 2
```
Lesson-provided facts: `cubane.pdb` is 20 lines, `methane.pdb` is 9 lines, total is 107.

### 2.7 Episode 4: the "Nelle checks her data" story (best research tie-in, 5–8 min)
```
cd ~/Desktop/shell-lesson-data/north-pacific-gyre
wc -l *.txt
wc -l *.txt | sort -n | head -n 5
wc -l *.txt | sort -n | tail -n 5
ls *Z.txt
```
From the lesson:
- One file is suspiciously short: `NENE02018B.txt` (240 lines).
- Two `Z`-named files (`NENE01971Z.txt`, `NENE02040Z.txt`) have missing depth data.
- Nelle chooses the good files with `NENE*A.txt NENE*B.txt`.

Teaching moment: "This is quality-control on data using only commands you just learned. Spreadsheet equivalents would take 10 min per file."

### 2.8 Episode 4: counting categories (maps to survey/field data)
In `exercise-data/animal-counts`:
```
head -n 5 animals.csv
cut -d , -f 2 animals.csv | sort | uniq
cut -d , -f 2 animals.csv | sort | uniq -c
```
Say: "`animals.csv` is like any CSV of observations: date, species, count. Column 2 is species. This gives you a frequency table." Researchers love this.

### 2.9 If you have 5 spare minutes at the end: loop teaser
From the lesson (Episode 5):
```
cd ~/Desktop/shell-lesson-data/exercise-data/creatures
for filename in basilisk.dat minotaur.dat unicorn.dat
do
    echo $filename
    head -n 2 $filename | tail -n 1
done
```
Lesson output: `basiliscus vulgaris`, `bos hominus`, `equus monoceros`.
Just show it, don't teach it: "That is what you'll learn next time."

---

## 3. What I would NOT add

- No new datasets or downloads. More files means more things for non-technical learners to get wrong.
- No `grep`/`find` demos unless you finish early. Those are Episode 7.
- No aliases, `.bashrc`, permissions, `chmod`. Different lesson.

---

## 4. Verification checklist (do this on your Mac tonight, ~10 min)

- [ ] Download and unzip `shell-lesson-data.zip` to your Desktop.
- [ ] `cd Desktop/shell-lesson-data/exercise-data && ls -F` matches the map above.
- [ ] Run 2.5, 2.6, 2.7, 2.8 once; make sure outputs make sense.
- [ ] `ls north-pacific-gyre | head` to see the real file names.
- [ ] Check `animals.csv` column 2 really is the species.
- [ ] Note any difference from the lesson's quoted output and adjust the script.
- [ ] Reset: delete the extracted folder and re-extract before teaching, so your Mac copy matches a fresh install.
