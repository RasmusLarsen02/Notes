## Introduction 
 Expectation are to use 20-25 hours on the course per week. Make sure to read the documentation and project descriptions to make sure you understand the entirety of the work expectations. 
We will work iteratively and continuously on the chirp twitter-clone to learn how to do running improvements. 


### Git
Git is used as a version control system (VCS) to keep track of the current version and changes in the code. 

**Git Data Model** 
Each git commit is structured as the image below shows 
![[Pasted image 20240828124346.png]]

The git data structure is constructed out of trees that each points to "blobs" or binary files that are stores in the git database. The trees are linked together via hashing.
When commits are made, git first makes a new blob, which points to a tree and then a new commit. Each blob object only touches its specific content, which helps mitigate, such that more people are not editing the same objects. 
Data data structure is a Merkle tree of hashing of hashing of hashing, it means that it is very hard to change the history, because of the complexity of the hashing. 
Git only stores complete copies of files. When you commit it creates a binary files with a hash and sees that a hash of that file already exists and then it creates a new blob of with the contents of the file. 
![[Pasted image 20240828132013.png]]

**Git commit recommendations 50/72 Rule** 
* Write summaries that are no more than 50 characters. 
* If you add text leave the next line blank 
* You can add as much text as needed but make the lines no more than 72 characters
	* Explain why a change, not what was changed, because people can see what was changed but understanding why it was changed is what matters.  