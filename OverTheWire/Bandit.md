#overthewire #challenges
## Level 0 → Level 1
creds to log in: bandit0@bandit0

'cat readme' -> ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

## Level 1 -> Level 2
"cat ./-" -> obtained password: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx


## Level 2 -> Level 3
bandit2:263JGJPfgU6LtdEvgfWU1XP5yac29mFx

cat 'spaces in this filename'  -> MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx


## Level 3 -> Level 4
bandit3:MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

cd inhere/
cat './...Hiding-From-You'
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ


## Level 4 -> Level 5
bandit4:2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

cd ./inhere
cat './-file07' 
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw


## Level 5 -> Level 6
bandit5:4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

cd maybehere07
bandit5@bandit:~/inhere$ ls -R -la | grep -i 1033
-rw-r-----  1 root bandit5 1033 Sep 19 07:08 .file2

cat maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG


## Level 6 -> Level 7
bandit6:HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

find / -type f -size 33c -group bandit6 -user bandit7 2>/dev/null
/var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

In Linux, **file descriptors** (FDs) control input and output streams for processes. The commonly used ones are:

- **0** → `stdin` (standard input)
- **1** → `stdout` (standard output)
- **2** → `stderr` (standard error)

Redirecting Different Streams

- `1>/dev/null` → Redirects **stdout** (normal output) to `/dev/null`, hiding it.
- `2>/dev/null` → Redirects **stderr** (error messages) to `/dev/null`, hiding it.
- `>/dev/null` → Same as `1>/dev/null` because `1` is the default for `>`.


## Level 7 -> Level 8
bandit7:morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

cat data.txt | sort | uniq | grep -i millionth
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc


## Level 8 -> Level 9
bandit8:dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

cat data.txt | sort | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM


## Level 9 -> Level 10
bandit9:4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

cat data.txt | strings
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey


## Level 10 -> Level 11
bandit10:FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

cat data.txt | base64 -d
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr


## Level 11 -> Level 12
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4



## Level 12 -> Level 13

**Compression** is a method of encoding that aims to reduce the original size of a file without losing information (or only losing as little as possible).

- `gzip` is a command to compress or decompress (`-d`) files. A ‘gzip’ file generally ends with `.gz`.
- `bzip2` is another command which allows for compressing and decompressing (`-d`) files. A ‘bzip2’ file generally ends with `.bz2`.

An **Archive File** is a file that contains one or multiple files and their metadata. This can allow easier portability.

- `tar` is a command that creates archive files (`-cf`). It also allows extracting these files again (`-xf`). A tar archive generally ends with `.tar`.


Password: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn


## Level 13 -> Level 14
