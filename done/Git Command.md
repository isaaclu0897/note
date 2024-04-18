

1. Reset author, update commit message, and keep commit date
	```bash
	> git -c rebase.instructionFormat='%s%nexec git commit --amend --no-edit --reset-author -m "Update REPO" --date="%ai"' rebase -i d59f8b7601

	# It will show as below interactive in the vim
	pick f7520b8 Update REPO
	exec git commit --amend --no-edit --reset-author -m "Update REPO" --date="2023-08-19 21:12:47 +0800"
	pick 78fbf96 Update REPO
	exec git commit --amend --no-edit --reset-author -m "Update REPO" --date="2023-08-19 22:13:48 +0800"
	```
