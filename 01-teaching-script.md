# Unix Shell: Teaching Script

**Class:** 9:00–12:00 | University researchers, mostly Windows (Git Bash), a few Macs | You + 1 helper
**Lesson:** https://swcarpentry.github.io/shell-novice/ (this script follows the current version, which uses `shell-lesson-data` on the Desktop)

> **Read this first**
> - Target: finish **Episode 3** cleanly and get **through pipes (`|`) in Episode 4**. Loops will NOT happen. That's fine.
> - Setup eats the first ~45 min. **Hard stop at 9:45**: anyone not working goes to the helper and follows along on a neighbor's screen.
> - The answer to "where is my Desktop?" on Windows may be inside OneDrive. See **OneDrive check** below.
> - Output shown below came from the lesson page. Windows paths will look different (`/c/Users/name`, not `/Users/nelle`). Say this out loud once.

---

## CLOCK

| Time | Block | Hard stop / cut rule |
|---|---|---|
| 9:00 | Welcome, expectations, helper intro | 9:10 |
| 9:10 | **Setup**: Git Bash, unzip, OneDrive check | **9:45 hard stop** |
| 9:45 | Ep 1: Introducing the Shell | 9:55 |
| 9:55 | Ep 2: Navigating Files and Directories | 10:35 |
| 10:35 | **Break** (10 min) | 10:45 |
| 10:45 | Ep 3: Working With Files and Directories | 11:25 |
| 11:25 | Ep 4: Pipes and Filters | 11:55 |
| 11:55 | Wrap-up, where to go next | 12:00 |

**If you're behind:** skip challenges first (do 1 per episode), then skip `man`/`help` demos, then skip wildcards `?`.
**If you're ahead:** do more challenges, then do the Ep 4 `animals.csv` pipe work, then show a loop as a teaser.

---

## 9:00 WELCOME (10 min)

- [ ] Introduce yourself and the helper.
- [ ] Say: "Typing is how we learn this. If you fall behind, **put up a sticky/raise a hand**. Falling behind is normal."
- [ ] Say: "**Don't type the `$`.** It's the prompt." (Say this again at 9:50.)
- [ ] Say: "Capitalization and spaces matter. Typos are normal. We'll all make them."
- [ ] Set up the help signal: sticky note on the laptop lid (red = stuck, green = done), or hand up.
- [ ] Ask: "Who has Git Bash already open?" Those people can start the data download early.

---

## 9:10 SETUP (35 min, hard stop 9:45)

### Windows: install Git Bash
1. Go to **https://gitforwindows.org** → Download.
2. Run installer. **Click Next through everything** (defaults are fine). Only exception: if a "default editor" screen offers it, pick **Nano** (we use nano in Ep 3). Default Vim is the common trap.
3. Finish. Start menu → type **Git Bash** → open.
4. Tell them: "If you can't install, hands up. The helper will come."

### Mac: open Terminal
- Cmd+Space → "Terminal".
- Macs use **zsh**, not bash. The lesson works either way. If asked: `echo $SHELL`. Typing `bash` switches (a warning about zsh may print; ignore it).

### Everyone: get the data
1. Download **shell-lesson-data.zip** from the lesson page (Setup section): https://swcarpentry.github.io/shell-novice/data/shell-lesson-data.zip
2. **Windows: right-click the zip → Extract All…**, then in the dialog **delete the trailing `\shell-lesson-data` from the destination so it ends at `...\Desktop`**. (The zip already contains a `shell-lesson-data` folder; the default destination adds a second one, giving `shell-lesson-data/shell-lesson-data`. Verified on the instructor's Windows laptop: with the destination ending at `...\Desktop`, the folder lands in `~/Desktop`.)
3. Target: a folder named `shell-lesson-data` on the **Desktop**.

### ⚠ DESKTOP CHECK (Windows, 2 min) — no new folders needed
They extract with **Right-click → Extract All…** on the Desktop they normally see in Explorer. Then, in Git Bash:

```
cd
ls ~/Desktop
```

| What they see | Meaning | Action |
|---|---|---|
| `shell-lesson-data` is listed (maybe also `desktop.ini`, `Git Bash.lnk`: ignore those) | Normal case. Your own laptop is like this. | Continue. Lesson paths work as written. |
| `No such file or directory`, or the folder isn't listed | Desktop is redirected into OneDrive | Run the next two lines |

```
ls -d ~/OneDrive*
ls ~/OneDrive*/Desktop
```

- If the second command lists `shell-lesson-data`: their "Desktop" is `~/OneDrive*/Desktop`. Have them run this once:
```
cd ~/OneDrive*/Desktop
pwd
```
  Say: "This is your Desktop for today." Wherever the lesson says `cd ~/Desktop/shell-lesson-data/...`, they type `cd ~/OneDrive<Tab>/Desktop/shell-lesson-data/...` (Tab fills in the long name).
- If the first command prints **two** OneDrive folders, `cd` will complain about too many arguments. Use Tab: `cd ~/OneDrive<Tab>`.
- Neither works: **Plan B**. `cd`, then `explorer .` opens the home folder in Explorer. Extract the zip there; the lesson path becomes `~/shell-lesson-data` (drop `Desktop/` from every path).

> Tested on your Windows laptop: the normal case only. The OneDrive-redirected case is untested.
> Don't use `explorer Desktop`: Explorer silently opens Downloads if the path isn't found.

### Setup done check (say to the room)
Everyone type:

```
cd
ls Desktop/shell-lesson-data
```

Expected: `exercise-data  north-pacific-gyre` (maybe with `/` marks).
**Green sticky when done.**

### Also settle now (2 min)
- [ ] Font size: Git Bash → right-click title bar → Options → Text → Font → size 14+. Mac: Cmd+`+`.
- [ ] Copy/paste in Git Bash: **Ctrl+Insert / Shift+Insert** (or Ctrl+Shift+V in newer versions). Plain Ctrl+C **stops a program**.
- [ ] Your projector: font large, white-on-black is fine.

---

## 9:45 EPISODE 1: INTRODUCING THE SHELL (10 min)

**Goal:** What is the shell, and why bother?

SAY:
- "The shell is a program that takes typed commands and runs other programs."
- "A GUI is easy to discover. A command line is easy to repeat and automate."
- "Example: running a 30-second program 1520 times by hand takes over 12 hours. A shell does it while you sleep." (Nelle's story, runs through the lesson.)
- "We're using **bash**. Mac default is zsh; it behaves the same for today."

TYPE:

```
ls
```
Lists what's in the current directory.

```
ks
```
Output: `ks: command not found`. "Typos happen. Nothing is broken."

**Do not teach more here. Move on.**

---

## 9:55 EPISODE 2: NAVIGATING FILES AND DIRECTORIES (40 min)

**Goals:** file vs directory, absolute vs relative paths, options & arguments, tab completion.

### Where am I?

```
pwd
```
"Print working directory." Windows will show `/c/Users/<name>`; Mac `/Users/<name>`. Lesson shows `/Users/nelle`. **Say: your path is different, that's fine.**

```
ls
ls -F
```
- `-F` adds `/` to directories. "ls is the command, `-F` is the **option**."
- ⚠ **Git Bash aliases `ls` to `ls -F --color=auto`**, so on Windows plain `ls` ALREADY shows `name/`. Both commands look the same there. Say: "Git Bash adds `-F` for you. On a Mac, plain `ls` has no slashes." To show the real difference on Windows: `\ls` (backslash bypasses the alias). Check with `type ls`.
- Your Mac: `alias ls='ls -F'` makes your projected screen match Windows. Say out loud that you set it.

### Getting help

| System | Command |
|---|---|
| Git Bash | `ls --help` |
| Mac | `man ls` (q to quit). `ls --help` does NOT work on macOS |
| Both | `help cd` works for built-ins |

SAY: "Git Bash has no `man`. Mac has no `--help` for ls. Both are fine."
(Skip if behind.)

### Moving around

```
ls -F Desktop
ls -F Desktop/shell-lesson-data
```
Output: `shell-lesson-data/`, then `exercise-data/ north-pacific-gyre/`

```
cd Desktop
cd shell-lesson-data
cd exercise-data
pwd
```
Ends in `.../Desktop/shell-lesson-data/exercise-data`

```
ls -F
```
Output: `alkanes/ animal-counts/ creatures/ numbers.txt writing/`

**Deliberate mistake (do it, it teaches):**

```
cd shell-lesson-data
```
Error: `No such file or directory`. SAY: "`cd` only sees what's inside where you are right now."

### Going up and home

```
cd ..
pwd
ls -F -a
```
- `..` = parent. `.` = here. `-a` = show hidden. Output includes `./ ../`.
- "Options combine: `ls -F -a` = `ls -Fa`."

```
cd
pwd
```
Bare `cd` = go home.

### Absolute vs relative

```
cd Desktop/shell-lesson-data/exercise-data
```
**Relative**: starts from where you are.

```
cd ~/Desktop/shell-lesson-data
```
**Absolute-ish**: `~` is home. A path starting with `/` is truly absolute.

SAY: "Leading `/` = start from the root. No leading `/` = start from here."

### Tab completion (the most important habit)
Type `cd ~/Desk` then press **Tab**. Press Tab twice to list options.
SAY: "Press Tab constantly. It prevents typos and saves time."

### cd -
```
cd exercise-data/creatures
cd -
cd -
```
Toggles between the last two places.

### Challenges (do 1–2, skip the rest if behind)
- **`ls` options:** `ls -l`, `ls -l -h` (sizes human-readable)
- **Reverse chronological:** `ls -rt` (newest last)
- **Absolute vs relative:** from `/Users/nelle/data`, to reach `/Users/nelle`: `cd ~`, `cd ..`, `cd`, `cd ~/data/..` all work; `cd .`, `cd /`, `cd ../..` don't.
- **Relative path:** `pwd` = `/Users/thing`, `ls -F ../backup` → `original/ pnas_final/ pnas_sub/`

> ✅ By 10:35 everyone should be able to: `pwd`, `ls -F`, `cd` into/out of a folder, and use Tab.

---

## 10:35 BREAK (10 min)

- [ ] Helper circulates to anyone behind.
- [ ] Remind: when we return, `cd ~/Desktop/shell-lesson-data/exercise-data/writing`
- [ ] You: drink water. Check clock. Decide which Ep 4 pieces to cut.

---

## 10:45 EPISODE 3: WORKING WITH FILES AND DIRECTORIES (40 min)

**Goals:** create, copy, move, delete files and dirs; wildcards.

### Setup
```
cd ~/Desktop/shell-lesson-data/exercise-data/writing
ls -F
```
Output: `haiku.txt  LittleWomen.txt`

### mkdir
```
mkdir thesis
ls -F
```
Output now includes `thesis/`. "No output on success. Silence means it worked."

```
mkdir -p ../project/data ../project/results
ls -F ../project
```
Output: `data/ results/`. `-p` = make the parent folders too.

SAY: "Naming: avoid spaces, use lowercase, `-`, `_`. Spaces cause pain later."

### nano
```
cd thesis
nano draft.txt
```
- Type any text.
- **Ctrl+O** (save) → Enter. **Ctrl+X** (exit).
- Reminder: `^` in nano means Ctrl.
- Mac note: nano may look slightly different. Same keys.

```
ls
```
Shows `draft.txt`.

### touch & rm
```
touch my_file.txt
ls -l
rm my_file.txt
```
`touch` = empty 0-byte file. "**No trash can in the shell. `rm` is forever.**"

### mv (move & rename)
```
cd ~/Desktop/shell-lesson-data/exercise-data/writing
mv thesis/draft.txt thesis/quotes.txt
ls thesis
```
Output: `quotes.txt`. "mv with a name in the same folder = **rename**."

```
mv thesis/quotes.txt .
ls thesis
ls thesis/quotes.txt
ls quotes.txt
```
`ls thesis` is empty; `ls thesis/quotes.txt` errors; `ls quotes.txt` works. "`.` = here."

SAY: "`mv` silently overwrites. `mv -i` asks first."

### cp
```
cp quotes.txt thesis/quotations.txt
ls quotes.txt thesis/quotations.txt
cp -r thesis thesis_backup
ls thesis thesis_backup
```
`-r` = recursive, needed for folders.

### rm
```
rm quotes.txt
ls quotes.txt
rm -i thesis_backup/quotations.txt
rm thesis
rm -r thesis
```
- `rm thesis` fails ("Is a directory"). `rm -r` removes a folder and everything inside with **no prompts**.
- **Dangerous: never `rm -r` unless you're sure.**

### Wildcards (cut `?` if behind)
```
cd ../alkanes
ls *.pdb
ls *t??ne.pdb
```
- `*` = zero or more characters. `?` = exactly one.
- `*t??ne.pdb` should list `ethane.pdb  methane.pdb`.

### Challenges (do 2)
- **Renaming:** fix `statstics.txt` → `mv statstics.txt statistics.txt`
- **Using `rm` safely:** what does `rm -i` do? Prompts; `y` deletes.
- **Moving files:** `mv sucrose.dat maltose.dat ../raw`
- **List filenames matching pattern** (want `ethane.pdb methane.pdb`): `ls *t??ne.pdb`
- **Reproduce a folder structure:** `mkdir -p` approach.

> ✅ By 11:25 everyone should be able to: make a folder, make a file in nano, copy, move/rename, delete, use `*`.

---

## 11:25 EPISODE 4: PIPES AND FILTERS (30 min)

**Goal:** chain small commands. This is the "aha" moment, so protect it. Skip challenges to get to the pipe.

```
cd ~/Desktop/shell-lesson-data/exercise-data/alkanes
ls
wc cubane.pdb
```
Output: `20  156  1158 cubane.pdb` (lines, words, characters).

```
wc *.pdb
wc -l *.pdb
```
`-l` lines only. Ends with `107 total`.

### Redirect `>`
```
wc -l *.pdb > lengths.txt
ls lengths.txt
cat lengths.txt
```
"`>` sends output to a file. It overwrites. `>>` appends."

### sort & head
```
sort -n lengths.txt
sort -n lengths.txt > sorted-lengths.txt
head -n 1 sorted-lengths.txt
```
Output: `9 methane.pdb` — shortest file. `-n` = sort as numbers.

### THE PIPE (the main point)
```
sort -n lengths.txt | head -n 1
wc -l *.pdb | sort -n | head -n 1
```
SAY: "`|` hands the output of one command to the next. No temp files. Small tools, chained."
**Ask the room:** "What do you think happens if I change `head` to `tail`?" Then run it.

### If time remains
```
echo hello > testfile01.txt
echo hello >> testfile02.txt
```
Overwrite vs append.

Then, from `exercise-data/animal-counts`:

```
cut -d , -f 2 animals.csv | sort | uniq
cut -d , -f 2 animals.csv | sort | uniq -c
```
Unique animal names, then counts.

**Danger to mention:** `sort -n lengths.txt > lengths.txt` **destroys** the file (redirect empties it first).

### Challenges (only if time)
- **What does `sort -n` do?** Numeric rather than alphabetical.
- **Piping commands together:** three shortest files → `wc -l * | sort -n | head -n 3`
- **Which pipe?** (count per animal) → `cut -d, -f 2 animals.csv | sort | uniq -c`

---

## 11:55 WRAP-UP (5 min)

- [ ] Recap with the room: `pwd ls cd mkdir nano touch cp mv rm wc sort head |  >`
- [ ] "We didn't get to **loops, scripts, grep, find**. That's the next session / next steps."
- [ ] Point to the lesson: https://swcarpentry.github.io/shell-novice/
- [ ] Mention `cd ~/Desktop/shell-lesson-data` is where to restart.
- [ ] Ask for feedback on a sticky: one thing that worked, one that didn't.
- [ ] Thank the helper.

---

## SURVIVAL CHEAT SHEET (keep visible)

| Problem | Say |
|---|---|
| Someone types the `$` | "Don't type the dollar sign." |
| `command not found` | "Typo — check the spelling. Press Up and edit." |
| `No such file or directory` | "Wrong place. `pwd`, then `ls`." |
| Stuck, command won't end | "**Ctrl+C**." |
| Stuck in nano | "Ctrl+X." |
| Stuck in `man` / `less` | "`q`." |
| Prompt shows `>` | "Unfinished command. Ctrl+C." |
| Lost | "`cd` then `pwd`" (go home, see where you are) |
| Up arrow | "Brings back the last command." |
