---
layout: post
title: "Re-setup octopress with existing github pages"
date: 2012-05-15 23:36
comments: true
categories: [Octopress, Github Pages]
---
I have setup octopress for github pages before in another labtop. Now I want to use octopress in an new labtop for the previous github pages. I tried this.  
```
git clone git://github.com/imathis/octopress.git octopress    
cd octopress     
git remote rename origin octopress   
git remote add origin git@github.com:myname/myname.github.com.git    
git config branch.master.remote origin        
git branch -m master source    
git pull origin source    
mkdir _deploy    
cd _deploy/    
git init   
git remote add origin git@github.com:myname/myname.github.com.git   
git pull origin master   
```   
Not sure it will work or not.   
Let me deploy and see. 

