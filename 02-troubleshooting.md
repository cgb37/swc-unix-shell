# Troubleshooting Sheet (find your symptom → fix)

> Written from the lesson text and general Git Bash / macOS knowledge. I could not test on a OneDrive-managed Windows laptop, so items marked **(unverified)** need a quick check on the first affected machine.

Quick triage: **Which OS? What do they see on screen? What does `pwd` say?**

---

## A. INSTALL (Windows)

| Symptom | Likely cause | Fix |
|---|---|---|
| Installer asks for admin password / "Run as administrator" blocked | No local admin rights | Ask: IT-managed laptop? Check Software Center / Company Portal for "Git" first. Else pair them with a neighbor. |
| Installer runs but no "Git Bash" in Start menu | Install didn't finish, or search is slow | Search "Git Bash" again; or right-click Desktop → "Open Git Bash here" (if available); or open `C:\Program Files\Git\git-bash.exe` |
| Can't download (blocked) | University firewall/proxy | Use phone hotspot or USB stick from you/helper. Keep the installer + `shell-lesson-data.zip` on a USB stick. |
| Opens "Git CMD" or "Git GUI" instead of Git Bash | Wrong app | Close; open **Git Bash** (black window, `$` prompt) |
| Opens PowerShell / Command Prompt | Wrong app | Prompt shows `C:\>` or `PS C:\>` → close, open Git Bash |
| WSL / Ubuntu already installed and they open it | They're in WSL, not Git Bash | **Organizer said avoid WSL.** Use Git Bash instead. If they are already in WSL, paths differ (`/mnt/c/...`); just switch to Git Bash. |
| Installer asked about editor, user picked Vim | Default | Don't reinstall. For nano: see **E. nano / editor**. |

**Plan if install is impossible for someone:** they pair with a neighbor and type along there; or use the helper's laptop for the break.

---

## B. WHERE IS MY DESKTOP? (OneDrive)

**Symptom:** `ls Desktop` → `No such file or directory`, or `ls` shows a folder like `OneDrive - University of …`, or `shell-lesson-data` "isn't there" even though it's on their desktop.

**Why:** Windows redirects Desktop/Documents into OneDrive. Git Bash's `~` is `C:\Users\<name>`, which is **not** the OneDrive location. (unverified on their setup)

**Diagnose (no new folders):**
```
cd
pwd
ls ~/Desktop
ls -d ~/OneDrive*
ls ~/OneDrive*/Desktop
```
- `ls ~/Desktop` shows `shell-lesson-data` → normal, nothing to fix (tested on the instructor's Windows laptop; `desktop.ini` and `Git Bash.lnk` in the listing are harmless).
- `ls ~/OneDrive*/Desktop` shows `shell-lesson-data` → redirected.

**Fix 1:** use the OneDrive Desktop as "the Desktop"
```
cd ~/OneDrive*/Desktop
pwd
```
Lesson paths `~/Desktop/...` become `~/OneDrive<Tab>/Desktop/...` (Tab completes it). If `~/OneDrive*` matches two folders, `cd` fails with "too many arguments"; complete with Tab instead. Folder names with spaces must be Tab-completed or quoted: `cd "OneDrive - University/Desktop"`.

**Fix 2 (Plan B):** extract into the home folder and drop `Desktop/` from every path
```
cd
explorer .
```
Drop the zip into that window and Extract All. The lesson path becomes `~/shell-lesson-data`.

**Don't use `explorer Desktop`**: if the path isn't found, Explorer silently opens Downloads instead.

**Warning:** OneDrive may start syncing the folder and show "sync pending". Harmless for today, but files in OneDrive can be slow or "online-only" placeholders. If `ls` shows files but `cat` hangs, right-click the folder → "Always keep on this device".

---

## C. ZIP / DATA PROBLEMS

| Symptom | Fix |
|---|---|
| `ls Desktop/shell-lesson-data` shows `shell-lesson-data` again | Doubled folder from double-click extract. Either `cd` one level deeper and use that, or re-extract with **right-click → Extract All…** |
| Can't find the downloaded zip | Check Downloads: `ls ~/Downloads`. Or Explorer → Downloads. |
| Zip opens as a "folder" in Explorer but contents don't show in Git Bash | It's not extracted. Right-click → Extract All. |
| Mac: Safari auto-unzipped into Downloads | Just move the `shell-lesson-data` folder to Desktop in Finder |
| Mac: Desktop prompts "Terminal would like to access files in your Desktop folder" | Click **OK/Allow**. If they clicked Don't Allow: System Settings → Privacy & Security → Files and Folders → Terminal → Desktop on |
| Mac: `ls Desktop` → `Operation not permitted` | Same permission issue as above |

---

## D. SHELL BASICS (during the lesson)

| What they see | What it means | Fix |
|---|---|---|
| `bash: ks: command not found` | Typo, or command doesn't exist here | Check spelling. Up-arrow and edit. |
| `No such file or directory` | Wrong directory or typo | `pwd` then `ls` to see where they are |
| `cd: too many arguments` | Path with a space unquoted | Use quotes or Tab-completion |
| Prompt shows `>` instead of `$` | Unclosed quote or unfinished command | **Ctrl+C**, then retype |
| Nothing happens after a command | Waiting for input (e.g. `wc -l` alone) | **Ctrl+C** |
| Screen filled with text / weird characters | Binary file `cat`ted | Type `reset` + Enter, or close the window |
| Pasting doesn't work | Windows Git Bash | **Shift+Insert** (or Ctrl+Insert to copy). Right-click may paste too. |
| Pasted text with weird characters / smart quotes | Copied from Word/web | Retype the quote characters |
| Ctrl+C doesn't paste | Ctrl+C = interrupt | Use Shift+Insert / Cmd+V |
| Up arrow prints `^[[A` | Not in a proper shell | Make sure they're in Git Bash / Terminal, not a different app |
| Prompt shows `C:\Users\name>` | Windows Command Prompt, not bash | Open Git Bash |
| `ls` colors hard to read on projector | Terminal theme | Right-click title → Options → Looks / Colours, or use a high-contrast theme |
| Text too small | | Git Bash: Options → Text → Font. Mac: Cmd+`+` |

---

## E. nano / editor

| Symptom | Fix |
|---|---|
| `nano: command not found` (older Git Bash) | Have them use Notepad to create the file in Explorer (`explorer .`), save it into the folder as `draft.txt`; or skip nano and use `echo "some text" > draft.txt` |
| Opened vim by accident (`~` all down the screen) | Press **Esc**, type `:q!` and Enter |
| Stuck in nano | **Ctrl+X**; if asked to save, press `N` |
| Ctrl+O doesn't work (Mac Terminal key mapping) | Try Esc then O; or use Terminal → Settings → Profiles → Keyboard → "Use Option as Meta" off/on |
| Ctrl+S froze the terminal | Press **Ctrl+Q** |
| Mac `nano` shows `pico` header | Same program, same keys |

---

## F. OS DIFFERENCES THAT WILL COME UP

| Topic | Git Bash (Windows) | macOS Terminal |
|---|---|---|
| Home path | `/c/Users/<name>` | `/Users/<name>` |
| Default shell | bash | zsh (prompt may end in `%`) |
| `man ls` | not installed | works |
| `ls --help` | works | doesn't (BSD `ls`) |
| `help cd` | works | works only in bash; in zsh it may be `command not found`. Type `bash` first. |
| `wc` output spacing | normal | padded with extra leading spaces; same numbers |
| `cp thesis thesis_backup` error text | GNU wording (`-r not specified; omitting directory`) | macOS: `cp: thesis is a directory (not copied).` |
| `rm thesis` error | `Is a directory` | `is a directory` (same idea) |
| `ls -F` | same | same |
| Hidden file `.DS_Store` | n/a | May appear in `ls -a`. Ignore. |
| Line endings | CRLF vs LF may affect `wc` slightly in some files (unverified) | n/a |
| Tab completion | works | works |
| File path separators | use `/` always | use `/` |

If a Mac user has the zsh prompt and the lesson looks off, just type:
```
bash
```
(ignore the "default interactive shell is now zsh" notice).

---

## G. CHALLENGE ANSWERS AT A GLANCE

| Episode | Challenge | Answer |
|---|---|---|
| 2 | Reverse chronological | `ls -rt` |
| 2 | Long listing human-readable | `ls -l -h` |
| 2 | From `/Users/nelle/data` to `/Users/nelle` | `cd ~`, `cd ..`, `cd`, `cd ~/data/..` |
| 2 | `ls -F ../backup` from `/Users/thing` | `original/ pnas_final/ pnas_sub/` |
| 3 | Rename `statstics.txt` | `mv statstics.txt statistics.txt` |
| 3 | Move to new folder | `mv sucrose.dat maltose.dat ../raw` |
| 3 | `ls` pattern for ethane + methane | `ls *t??ne.pdb` |
| 3 | `cp` with 3+ args | last arg must be a directory |
| 3 | Move all `.dat` to `analyzed` | `mv *.dat analyzed` |
| 3 | Make `data/raw` and `data/processed` | `mkdir -p data/raw data/processed` |
| 4 | `sort -n` | numeric sort |
| 4 | 3 shortest files | `wc -l * \| sort -n \| head -n 3` |
| 4 | Count per animal | `cut -d, -f 2 animals.csv \| sort \| uniq -c` |
| 4 | Unique animals | `cut -d , -f 2 animals.csv \| sort \| uniq` |
| 4 | Remove unneeded files | `rm *.txt` (not `rm * .txt`!) |

---

## H. WHEN SOMEONE IS HOPELESSLY BEHIND

1. Helper takes them aside **at the break**, not mid-lesson.
2. They follow on a neighbor's screen and type later.
3. Reset command that gets anyone back to a known place:
```
cd ~/Desktop/shell-lesson-data/exercise-data
```
4. Wiped something by accident? The lesson data is re-extractable from the zip.

---

## I. YOUR OWN SAFETY NET

- [ ] Keep `Git-*-64-bit.exe` and `shell-lesson-data.zip` on a USB stick and on your own laptop.
- [ ] Have the lesson page open on the second laptop: https://swcarpentry.github.io/shell-novice/
- [ ] If the projector dies: share your screen / have people follow the page.
- [ ] Whiteboard: write the "Ctrl+C stops everything" rule early.
