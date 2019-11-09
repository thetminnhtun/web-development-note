# Git Basic

```
git init
```
Git initialize ပြုလုပ်ခြင်း၊ Git repo တည်ဆောက်ခြင်းဖြစ်သည်။ တည်ဆောက်ပြီးပါက project folder ထဲတွင် `.git` အမည်ဖြင့် hidden လုပ်ထားသော folder ပေါ်လာပါလိမ့်မည်။

```
git add <directory or filename>

eg. git add .
```
Git အတွင်းသို့ file (သို့) folder ကိုထည့်သွင်းခြင်း။
မှတ်ချက်။ ။ Project အတွင်းမှ folder အပါအဝင် file အားလုံးထည့်သွင်းလိုပါက ` git add . ` command ကို အသုံးပြုပါ။

```
git commit -m "<message>"

eg. git commit -m "write a text about you have done task"
```
`git add` ပြုလုပ်ပြီးတိုင်း `commit` ပြုလုပ်ပေးရန်လိုအပ်သည်။ `commit` ပြုလုပ်တိုင်း `-m` flag ကိုအပြုပြီးနောက်မှ ပြုလုပ်ခဲ့သော အကြောင်းအရာကို ရေးပါ။

```
git status
```
လက်ရှိ git အခြေအနေ ကို ဖော်ပြပေးလိမ့်မည်။ အခြေအနေဆိုသည်မှာ git အတွင်းသို့ ထည့်ပြီးသော file များ၊ မထည့်ရသေးသော file များကိုဆိုလိုသည်။

```
git log
```
commit များကို ပြန်ကြည့်ရန်သုံးသည်။

```
git branch <branch name>

eg. git branch git_test
```
git တွင် branch တည်ဆောက်ရာတွင် သုံးသည်။

```
git branch 
```
git အတွင်းရှိ branch များကိုကြည့်ရန် သုံးသည်။

```
git checkout <branch name>

eg. git checkout git_test
```
အခြား branch သို့ ပြောင်းရန်သုံးသည်။

```
git checkout master
```
master branch သို့ ပြောင်းရန်သုံးသည်။

```
git branch -d <branch name>

eg. git branch -d git_test
```
branch ကို ဖျက်ရာတွင်သုံးသည်။

```
git remote add <name> <url>

eg. git remote add origin http://github.com/account_name/project_name.git
```
git remote connection ကို ချိတ်ဆက်ရာတွင်သုံးသည်။ `<url>` တွင် git repo path ကိုထည့်ပါ။ `<name>` တွင် `<url>` အစားအသုံးပြုလိုသည့် အမည်ကို ရေးပါ။

```
git push origin master
```
git repo ပေါ်သို့ `commit` ပြုလုပ်ပြီးသော `stage` ကိုတင်ရန်သုံးသည်။ `origin` သည် `git repo path` ပင်ဖြစ်သည်။

```
git clone <repo>

eg. git clone https://github.com/account_name/project_name.git 
```
git repo တွင် တင်ထားသော project ကို clone လုပ်ရန် သုံးသည်။

```
git pull origin master
```
git repo ပေါ်မှ master branch ကို pull လုပ်ရတွင်သုံးသည်။

More Detail -> [atlassian-git-cheatsheet](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)