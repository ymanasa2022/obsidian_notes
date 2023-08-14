
# obsidian_notes
**notes made using obsidian**

All subjects are divided into sub folders in this vault.
A new vault for each sub folder is not created.
Everything should be viewable in my git repo: obsidian_notes

## **For syncing with iPad**
I followed [these](https://gist.github.com/DannyQuah/f686c0e43b741468e12515cd79017489) instructions 
For iPad notes, I created a separate branch called ipad_notes
### *Normal work cycle* 
1. Go to iPad > iSH
2. cd /mnt/ymanasa/Obsidian/obsidian_notes
	- Obsidian/ is not a git repo. obsidian_notes/ is the git repo 
3. `git pull` if needed (will need to if I make changes on laptop and git commit to main branch)
4. Work on iPad > Obsidian 
5. When done iPad > iSH, **`git add`, `git commit -m ‘commit msg’`, `git push`** to push to ipad_notes branch 
	- Issue: need to create new personal access token on GitHub every time I push
		- Workaround: 
			- run `git config --global credential.helper store` while in /root via iPad > iSH 
			- Add the following lines to /root/.git-credentials 
				- machine ***username*** 
				   password ***personal access token*** 
		will not need to put in token and username to push from iPad ever again 
1. (First time) Username and password:
	- ymanasa2022
	- use personal access token generated on GitHub under developer settings (ipad_token)
	
### *To merge with main branch*
Always commit changes on ipad, pull on laptop and make changes on the same ipad_notes branch 

[git cheat sheet](https://education.github.com/git-cheat-sheet-education.pdf)
1.  `git checkout main`
	- WARNING: You have to commit and push changes on ipad_notes branch before checking out macbook_notes branch otherwise all changes on ipad_notes will be overwritten by whatever is in macbook_notes 
2. `git commit -m ‘merging ipad_notes with laptop’ `
3. `git merge ipad_notes`
4. `git push`

## For syncing with MacBook 
### ***Cloning the obisidian_notes repo*** 
1. Navigate to directory where you want your repo 
2. `git clone https://github.com/ymanasa2022/obsidian_notes`

### *Normal work cycle* 
1. Go to terminal
2. Navigate to the repo (/Users/manasayadavalli/Desktop/obsidian_notes)
3. `git pull` if needed 
4. make changes in obisidian 
5. `git commit -m 'msg'`
6. `git push`