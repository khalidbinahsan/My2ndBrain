## Push files in new repository
```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/khalidbinahsan/Laravel-Assignment-2.git
git push -u origin main
```
## Update the existing repository
```bash
git add .
git commit -m "some changes"
git push -u origin master
```
## Push an existing repository
```bash
git remote add origin https://github.com/khalidbinahsan/Laravel-Assignment-2.git
git branch -M main
git push -u origin main
```
## To create a new branch
```bash
git checkout -b main
```