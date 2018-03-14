---
layout: post
title: npm permission denied
categories: linux
---

`Error: EACCES: permission denied`  

lol, I used to see this alert a few times while I was starting my node learning and it has not confused me in quite a long time. yersterday, I realize some friend fell in the same mire just like what I did. In this post, I'll list 4 situation below, and introduce how to fix it.  


__sudo__

usually, we'd better confirm if we run the command with sudo, try:

`sudo -g npm install gatsby-cli`

> if your platform dont' instal sudo default like centos, try `yum install sudo`, and add your info to `/etc/sudoers`

__yarn__

if sudo doesn't work. And you want to add packages as soon as possible. I recommend you try `yarn` or `cnpm`.

```
npm -g install yarn
yarn global add gatsby-cli
```
and 
```
npm -g install cnpm
npm -g install gatsby-cli
```

> Some global packages needs to write files in root directory, it might be obstruct by our npm dir, and npm authority; however, yarn global packages is located at your users' file. checkout `~.yarn`

__npm authority__

What caused npm can't install packages? Scan the global node_modules dir. try `usr/local/lib/node_modules` if your install node/npm by apt-get, yum, or brew dir whiling use MacOS.  
Well, if you still can't find them, try: 

annotations below is the ouput from my mac,

```shell
which npm 
# /usr/local/bin/npm
```
`/usr/local/bin/npm` means current npm executable locate here, and is might be a mirror. Let's find the real direactory of npm.  

```
cd /usr/local/bin && ls -l | grep npm
# lrwxr-xr-x   1 mercurio  admin        38 Oct 22 15:19 npm -> ../lib/node_modules/npm/bin/npm-cli.js
```

what does `lrwxr-xr-x` means?

+ `l` represent file type, 
+ `rwx` represent the auth of owner, r(read)w(write)x(execute), 7
+ `r-x` represent the auth of the file group, r-x, 3
+ `r-x` ... other users, r-x, 3

> I've chown npm myself, so it print my user name, if you didn't do it, it might be root

Look out, nobody have the authority of using npm to write, but the owner. that's why we need sudo to root, the owner.

you also can `sudo chmod o=r+w+x /usr/local/lib/node_modules/npm/bin/npm-cli.js` and try `npm install gatsby-cli -g` again.

__node_modules reserved__

We've got the npm write authority, but, what should we do if it doesn't work at all?  
the problem based the lack of our file authority, we want to write into `/usr/local/lib/node_modules`, don't we ?

make the `node_modules` ourselves! 
// it's a danger behaviour. Recomend give it back to root after all.

```
sudo chown /usr/local/lib/node_modules ${whoami}
npm install -g gatsby-cli
```

It works.
