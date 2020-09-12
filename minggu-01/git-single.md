Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git clone https://github.com/nikhwanbs/tekn-cloud-computing
Cloning into 'tekn-cloud-computing'...
remote: Enumerating objects: 34, done.
remote: Counting objects: 100% (34/34), done.
remote: Compressing objects: 100% (26/26), done.
remote: Total 34 (delta 2), reused 20 (delta 0), pack-reused 0
Unpacking objects: 100% (34/34), 8.93 KiB | 106.00 KiB/s, done.

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ vim README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ cat README.md
Hello worldd

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing1 (master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md
        ../tekn-cloud-computing/

nothing added to commit but untracked files present (use "git add" to track)

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git add -A

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git commit -m "Add: README.md"
[master 50ce86a] Add: README.md
 2 files changed, 2 insertions(+)
 create mode 100644 minggu-01/README.md
 create mode 160000 tekn-cloud-computing

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git push origin
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 471 bytes | 471.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/nikhwanbs/tekn-cloud-computing
   e034dac..50ce86a  master -> master

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git checkout -b edit-readme-1
Switched to a new branch 'edit-readme-1'

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (edit-readme-1)
$ vim README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (edit-readme-1)
$ cat README.md
Hello worldd

ini isi proyek

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (edit-readme-1)
$ git status
On branch edit-readme-1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (edit-readme-1)
$ git add -A
warning: LF will be replaced by CRLF in minggu-01/README.md.
The file will have its original line endings in your working directory

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (edit-readme-1)
$ git commit -m "Add: isi README.md"
[edit-readme-1 e0ac86d] Add: isi README.md
 1 file changed, 2 insertions(+)

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (edit-readme-1)
$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git merge edit-readme-1
Updating ef96cda..288fab9
Fast-forward
 README.md | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git branch -D edit-readme-1
Deleted branch edit-readme-1 (was 288fab9).

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git branch
* master

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git pull
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), 630 bytes | 210.00 KiB/s, done.
From https://github.com/nikhwanbs/tekn-cloud-computing
   ef96cda..05ffecb  master     -> origin/master
Updating 288fab9..05ffecb
Fast-forward

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git checkout -b edit-readme-2
Switched to a new branch 'edit-readme-2'

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (edit-readme-2)
$ vim README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (edit-readme-2)
$ var README.md
bash: var: command not found

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (edit-readme-2)
$ cat README.md
you'll say wasn't that hard

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (edit-readme-2)
$ git checkout master
Switched to branch 'master'
M       README.md
Your branch is up to date with 'origin/master'.

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ car README.md
bash: car: command not found

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ cat README.md
you'll say wasn't that hard

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git branch -D edit-readme-2
Deleted branch edit-readme-2 (was 05ffecb).

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git branch
* master

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ cat README.md
you'll say wasn't that hard

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git reset --hard
HEAD is now at 05ffecb Merge pull request #1 from nikhwanbs/edit-readme-1

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ cat README.md
Hai Dunia

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git log --online
fatal: unrecognized argument: --online

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ cat README.md
Hai Dunia

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git log --oneline
05ffecb (HEAD -> master, origin/master, origin/HEAD) Merge pull request #1 from nikhwanbs/edit-readme-1
288fab9 (origin/edit-readme-1) Add: isi README.md
ef96cda Add: README.md
51941bd Initial commit

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ vim README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git add -A

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git commit -m "Add: contents"
[master 3447a3d] Add: contents
 1 file changed, 1 insertion(+)

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git push origin master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 294 bytes | 294.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/nikhwanbs/tekn-cloud-computing
   05ffecb..3447a3d  master -> master

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ vim README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git add -A

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git commit -m "Add: contents - 2"
[master 59f9605] Add: contents - 2
 1 file changed, 1 insertion(+)

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git push origin master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 298 bytes | 298.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/nikhwanbs/tekn-cloud-computing
   3447a3d..59f9605  master -> master

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git revert HEAD
[master 5102a87] Revert "Add: contents - 2"
 1 file changed, 1 deletion(-)

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git push origin master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 326 bytes | 326.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/nikhwanbs/tekn-cloud-computing
   59f9605..5102a87  master -> master

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ cat README.md
Hai Dunia
ini isi 1

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ vim README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ cat README.md
Hai Dunia
ini isi 1
ini isi tambahan 1

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git add -A

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git commit -m "Add: isi tambahan 1"
[master 8182470] Add: isi tambahan 1
 1 file changed, 1 insertion(+)

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git log --oneline
8182470 (HEAD -> master) Add: isi tambahan 1
5102a87 (origin/master, origin/HEAD) Revert "Add: contents - 2"
59f9605 Add: contents - 2
3447a3d Add: contents
05ffecb Merge pull request #1 from nikhwanbs/edit-readme-1
288fab9 (origin/edit-readme-1) Add: isi README.md
ef96cda Add: README.md
51941bd Initial commit

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git reset --hard HEAD^
HEAD is now at 5102a87 Revert "Add: contents - 2"

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ cat README.md
Hai Dunia
ini isi 1

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ vim README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ vim README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ cat README.md
Hai Dunia
ini isi 1
ini isi 2
ini isi 3

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git log --oneline
5102a87 (HEAD -> master, origin/master, origin/HEAD) Revert "Add: contents - 2"
59f9605 Add: contents - 2
3447a3d Add: contents
05ffecb Merge pull request #1 from nikhwanbs/edit-readme-1
288fab9 (origin/edit-readme-1) Add: isi README.md
ef96cda Add: README.md
51941bd Initial commit

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git log --oneline
5102a87 (HEAD -> master, origin/master, origin/HEAD) Revert "Add: contents - 2"
59f9605 Add: contents - 2
3447a3d Add: contents
05ffecb Merge pull request #1 from nikhwanbs/edit-readme-1
288fab9 (origin/edit-readme-1) Add: isi README.md
ef96cda Add: README.md
51941bd Initial commit

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ vim README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ vim README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git add -a
error: unknown switch `a'
usage: git add [<options>] [--] <pathspec>...

    -n, --dry-run         dry run
    -v, --verbose         be verbose

    -i, --interactive     interactive picking
    -p, --patch           select hunks interactively
    -e, --edit            edit current diff and apply
    -f, --force           allow adding otherwise ignored files
    -u, --update          update tracked files
    --renormalize         renormalize EOL of tracked files (implies -u)
    -N, --intent-to-add   record only the fact that the path will be added later
    -A, --all             add changes from all tracked and untracked files
    --ignore-removal      ignore paths removed in the working tree (same as --no-all)
    --refresh             don't add, only refresh the index
    --ignore-errors       just skip files which cannot be added because of errors
    --ignore-missing      check if - even missing - files are ignored in dry run
    --chmod (+|-)x        override the executable bit of the listed files
    --pathspec-from-file <file>
                          read pathspec from file
    --pathspec-file-nul   with --pathspec-from-file, pathspec elements are separated with NUL character


Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git add -A

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git commit -m "Add: contents - 2"
[master 08fe485] Add: contents - 2
 1 file changed, 2 insertions(+)

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git log --oneline
08fe485 (HEAD -> master) Add: contents - 2
5102a87 (origin/master, origin/HEAD) Revert "Add: contents - 2"
59f9605 Add: contents - 2
3447a3d Add: contents
05ffecb Merge pull request #1 from nikhwanbs/edit-readme-1
288fab9 (origin/edit-readme-1) Add: isi README.md
ef96cda Add: README.md
51941bd Initial commit

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ vim README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git add -A

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git commit -m "Add: contents - 3"
[master 94cecd9] Add: contents - 3
 1 file changed, 2 insertions(+)

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ cat README.md
Hai Dunia
ini isi 1

ini isi 2

ini isi 3

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git log --oneline
94cecd9 (HEAD -> master) Add: contents - 3
08fe485 Add: contents - 2
5102a87 (origin/master, origin/HEAD) Revert "Add: contents - 2"
59f9605 Add: contents - 2
3447a3d Add: contents
05ffecb Merge pull request #1 from nikhwanbs/edit-readme-1
288fab9 (origin/edit-readme-1) Add: isi README.md
ef96cda Add: README.md
51941bd Initial commit

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git revert 08fe485
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
error: could not revert 08fe485... Add: contents - 2
hint: after resolving the conflicts, mark the corrected paths
hint: with 'git add <paths>' or 'git rm <paths>'
hint: and commit the result with 'git commit'

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master|REVERTING)
$ cat README.md
Hai Dunia
ini isi 1
<<<<<<< HEAD

ini isi 2

ini isi 3
=======
>>>>>>> parent of 08fe485... Add: contents - 2

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master|REVERTING)
$ vim README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master|REVERTING)
$ cat README.md
Hai Dunia
ini isi 1

ini isi 2 setelah revert

ini isi 3

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master|REVERTING)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)

You are currently reverting commit 08fe485.
  (fix conflicts and run "git revert --continue")
  (use "git revert --skip" to skip this patch)
  (use "git revert --abort" to cancel the revert operation)

Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
        both modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master|REVERTING)
$ git add README.md

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master|REVERTING)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)

You are currently reverting commit 08fe485.
  (all conflicts fixed: run "git revert --continue")
  (use "git revert --skip" to skip this patch)
  (use "git revert --abort" to cancel the revert operation)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md


Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master|REVERTING)
$ git revert --continue
[master 1be9025] Revert "Add: contents - 2"
 1 file changed, 1 insertion(+), 1 deletion(-)

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git push origin master
Enumerating objects: 11, done.
Counting objects: 100% (11/11), done.
Delta compression using up to 8 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (9/9), 906 bytes | 302.00 KiB/s, done.
Total 9 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/nikhwanbs/tekn-cloud-computing
   5102a87..1be9025  master -> master

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ cat README.md
Hai Dunia
ini isi 1

ini isi 2 setelah revert

ini isi 3

Ikhwan@DESKTOP-RN4MJOC MINGW64 ~/tekn-cloud-computing (master)
$ git pull
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 8 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (8/8), 5.23 KiB | 297.00 KiB/s, done.
From https://github.com/nikhwanbs/tekn-cloud-computing
   1be9025..e034dac  master     -> origin/master
Updating 1be9025..e034dac
Fast-forward
 minggu-01/rangkuman-cloud-computing.md | 39 ++++++++++++++++++++++++++++++++++
 1 file changed, 39 insertions(+)
 create mode 100644 minggu-01/rangkuman-cloud-computing.md
