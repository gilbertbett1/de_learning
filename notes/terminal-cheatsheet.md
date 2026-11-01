# Terminal Cheatsheet

Personal reference for the shell commands I use while learning data engineering.

## Navigation

```bash
pwd                  # where am I?
ls -la               # list all files, including hidden ones
cd <folder>          # go into a folder
cd ..                # up one level
cd -                 # back to the previous folder
cd ~                 # go home
```

- **Tab** autocompletes names; **Up arrow** recalls earlier commands; **Ctrl+R** searches command history.
- Absolute paths start with `/`; relative paths start from where I am.

## Files and folders

```bash
mkdir -p data/raw data/clean   # create nested folders
touch file.txt                 # create an empty file
cp file.txt backup.txt         # copy
mv file.txt data/raw/          # move (also renames)
rm file.txt                    # delete a file (permanent!)
rm -r <folder>                 # delete a folder and its contents (permanent!)
```

## Viewing files

```bash
cat file.txt           # print everything
head -n 5 file.txt     # first 5 lines
tail -n 5 file.txt     # last 5 lines
less file.txt          # scroll (q to quit)
wc -l file.txt         # count lines
```

## Pipes and redirection

- A pipe (`|`) sends the output of one command into the next, so small tools combine into powerful ones.
- `>` writes output to a file and **overwrites** it.
- `>>` **appends** output to a file.

```bash
grep Nairobi sales.csv                              # lines containing "Nairobi"
grep -c Laptop sales.csv                            # count matching lines
cut -d',' -f2 sales.csv                             # extract column 2
sort -t',' -k4 -nr sales.csv | head -n 3            # top 3 rows by column 4
cut -d',' -f2 sales.csv | tail -n +2 | sort | uniq -c   # count rows per value
head -n 1 sales.csv > out.csv                       # write the header first
grep Mombasa sales.csv >> out.csv                   # then append matching rows
awk -F',' '$3=="Laptop" {sum += $4} END {print sum}' sales.csv   # sum a column with a filter
```

## Environment variables

Environment variables are named values that programs can read. They let pipelines receive configuration and secrets (database passwords, API keys) without writing them in code.

```bash
echo $HOME                         # read a variable
export MY_VAR="value"              # set for this terminal session only
printenv MY_VAR                    # confirm it is set
env | grep MY_VAR                  # search all variables
set -a; source .env; set +a        # load every line of a .env file
python3 -c "import os; print(os.environ.get('MY_VAR'))"   # read it from Python
```

- Keep secrets in `.env` and make sure `.env` is in `.gitignore`.

## Virtual environment

```bash
source .venv/bin/activate    # activate
which python                 # should point inside .venv
deactivate
```

## Getting help

```bash
man ls          # manual for a command (q to quit)
ls --help       # quick usage summary
```

## Rules I follow

- Run `ls` before `rm`, and never run `rm -rf` on a path I haven't double-checked.
- Use `>>` when I want to keep existing content; `>` wipes the file.
- Never commit `.env` files or secrets.

## Lessons learned

### Nov 1, 2026

- `grep` only returns matching lines, so a header row is lost unless I write it first with `head -n 1` and `>`.
- `grep Laptop` matches the word anywhere on the line; filter the exact column when precision matters.