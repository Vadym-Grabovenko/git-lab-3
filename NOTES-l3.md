## Варіант          журнал, варіант, прізвище
                    11,1,Грабовенко

## 1. stash list    рядок із вашим -m
                    D:\git-lab-3>git stash list
                    stash@{0}: On lab3/variant-1-Grabovenko: чернетка контакту v1                  

## 2. cherry-pick   два хеші і чому вони різні
                    D:\git-lab-3>git commit -m "Виправити контакт групи"
                    [feature/pick-1 c2e5a7e] Виправити контакт групи
                    2 files changed, 4 insertions(+)
                    create mode 100644 draft-v1.txt

                    D:\git-lab-3>git switch lab3/variant-1-Grabovenko
                    Switched to branch 'lab3/variant-1-Grabovenko'

                    D:\git-lab-3>git cherry-pick c2e5a7e - хеш коміту до cherry-pick
                    [lab3/variant-1-Grabovenko 9a59622 - хеш коміту після cherry-pick] Виправити контакт групи
                    Date: Wed Oct 14 09:09:13 2026 +0300
                    2 files changed, 4 insertions(+)
                    create mode 100644 draft-v1.txt
                    
                    Чому так?
                    Cherry-pick копіює не коміт цілковито з хешем, а копіює його вміст (зміни), створює новий коміт на основі попередньо скопійованих змін і виходить два коміти з різними хешами - до cherry-pick та після відповідно. Коміт від cherry-pick розміщується туди, куди дивиться HEAD. 
                    
## 3. reflog        два рядки до і після amend
                    7692671 (HEAD -> lab3/variant-1-Grabovenko) HEAD@{0}: commit (amend): Уточнити контакт групи, варіант 1
                    9a59622 HEAD@{1}: cherry-pick: Виправити контакт групи

## 4. revert        log --oneline, видно обидва коміти
                    git log --oneline --graph
                    * 0f4d94b (HEAD -> lab3/variant-1-Grabovenko, origin/lab3/variant-1-Grabovenko) Revert "Commit for revert"
                    * 26d655c Commit for revert
                    * 7692671 Уточнити контакт групи, варіант 1
                    * ad98ae6 (main) Variant 1 file

## 5. тег           фрагмент git show: tag, Tagger, повідомлення
                    tag v0.1-Grabovenko
                    Tagger: Vadym-Grabovenko <vadimgrabovenko.21@gmail.com>
                    Date:   Wed Oct 14 10:00:00 2026 +0300  

                        Перший зріз варіанта 1

## 6. rebase -i     pick / squash і підсумкове повідомлення
                    D:\git-lab-3>git rebase -i HEAD~2
                    [detached HEAD f5bd64a] WIP: чернетка - <span style="color:red;"> я бачу що повідомлення не те, доелось змінити за допомогою ammend і змінився хеш коміту, вибчате</span> 
                    Date: Wed Oct 14 10:32:10 2026 +0300
                    1 file changed, 3 insertions(+), 1 deletion(-)
                    Successfully rebased and updated refs/heads/lab3/variant-1-Grabovenko.
                    
                    <span style="color:green;Змінив повідомлення на правильне</span>
                    ">D:\git-lab-3>git commit --amend
                    [lab3/variant-1-Grabovenko 8b6d439] Оновити контакт групи
                    Date: Wed Oct 14 10:32:10 2026 +0300
                    1 file changed, 3 insertions(+), 1 deletion(-)

## 7. blame         один рядок   
                D:\git-lab-3>git blame -L 1,5 CONTACT.md
                7692671c (Vadym-Grabovenko 2026-10-14 09:09:13 +0300 1) Channges for stash

## 8. fork          origin, upstream, куди push і куди PR
                    origin — це мій власний віддалений репозиторій, куди я завантажую свої гілки.
                    upstream — це оригінальний репозиторій проєкту, з якого робиться fork.
                    Зміни з оригінального репозиторія можна отримати через fetch upstream, а власні коміти надсилаються через push у свій origin.
                    Для передачі коду розробникам оригінального проєкту створюється PR в upstream/main.