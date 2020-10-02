#### How to use Github. ####

#First open a new repository using the '+' icon on the right most corner.
You can initialize your repo with a readme.md file.
If you init your repo with a readme.md file it will not show your remote git link. To find it press the 'Clone or download button'. You will find a link which redirect to your current repository.
Now to upload the source code first download the Git software for windows using this link https://git-scm.com/download/win . Install it.

  Right click on the local folder and start GitBash here.
  Write the following commands :
	git init
	git add . [Add all the files of that folder]
	git commit -m 'First Commit'
	git remote add origin <your remote git link>
	git push -u origin master
  Now you can delete your local files.

#To edit the existing repository firstly create a local folder in your computer.
  Right click on the local folder and start GitBash here.
  Write the following commands :
	git init
	git remote add origin <your remote git link>
	git pull origin master [This command will download all the files of your existing repository]
	[Edit file / Add file]
	git push origin master [Upload again] 
	

#How to setup SSH key

  Type these commands [You may need both CMD and Git]

	ssh-keygen //Generate RSA Key files. Press Enter only. Do not change dirrectory
	cd C:/Users/<username>  //Browse to ssh Username folder where you can find .ssh file. Look for id_rsa and id_rsa.pub 
	
	eval $(ssh-agent) 
	ssh-add ~/.ssh/<private_key_file>
	
  If these two commands does not work try these commands
  	
	ssh-agent bash
	ssh-add
	
	
  Go to your C:/Users/<username>/.ssh . Open id_rsa.pub with Notepad++ and press Ctrl+A to copy everything. 
  Now go to your Git accounts, it can be GitHub or BitBucket or Codemaster. Go to settings. You will find a
  button to addnew SSH key. Name it anything. Add the key in the Key Field.
  
  So everything is set up. Now you can clone, push or pull anything to your Git accounts using SSH key.
  
  
  To rest a commit 
  
  	git reset --hard <SHA COMMIT ID>
	git push origin --force
	
