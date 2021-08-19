# Making alias in the Git Bash for the Window

- Open the Git Bash
- Go the home dir
```sh
cd ~
```
- Make a file named `.bashrc`
```sh
touch .bashrc
```
- Open file with any text editor and put alias command what you want.

eg.
```sh
alias ll='ls -l'
alias pa='php artisan'
alias dcu='docker-compose up -d'
alias dcd='docker-compose down'
alias dcb='docker-compose exec php bash' 
alias dpa='docker-compose exec php php artisan
```
- Run below command to apply alias command
```sh
souce ~/.bashrc
```
- Then you can run alias command (view file lists in current directory) in the git bash. You will see file lists.

eg.
```bash
ll
```

**Note:** Whenever update the `.bashrc`, have to run `souce ~/.bashrc` command

