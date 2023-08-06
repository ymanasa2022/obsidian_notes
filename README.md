# obsidian_notes
**notes made using obsidian**

All subjects are divided into sub folders in this vault.
A new vault for each sub folder is not created.
Everything should be viewable in my git repo: obsidian_notes

## *For syncing with iPad*
I followed [these](https://gist.github.com/DannyQuah/f686c0e43b741468e12515cd79017489) instructions 
For iPad notes, I created a separate branch called ipad_notes
### Normal work cycle 
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
	
#### To merge with macbook_notes branch 
No reason to merge with main branch 
Always commit changes on ipad, pull on laptop and make changes 
Only merging README updates with main
[git cheat sheet](https://education.github.com/git-cheat-sheet-education.pdf)
1.  git checkout macbook_notes
	- WARNING: You have to commit and push changes on ipad_notes branch before checking out macbook_notes branch otherwise all changes on ipad_notes will be overwritten by whatever is in macbook_notes 
3. git merge ipad_notes

## *For syncing with MacBook* 



Testing 