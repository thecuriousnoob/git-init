#Appendix 2 - Git vs SVN

There are many advantages to use Git rather than SVN as both appendixes 1 et 2 additional resources can show you. In this appendix we'll only see the two biggest.

##Centralized VCS vs Distributed VCS
The very first difference between Git and SVN is that Git is a distributed VCS while SVN is a centralized one.

In the case of SVN, and as you might have seen in the video featured in Appendix 1, centralization main problem is that having a single server is having a single point of failure. If your server gets down, your project gets down, your business gets down.

Git is distributed so that every contributor to a repository has its own local copy of it. So whenever a node of this distributed network of contributors gets down, there will be plenty other nodes available so your business doesn't get down !
You can see the remote server where you push your commits as a contributor hosting his own local copy of your project. Except that this contributor is a machine ! If the machine gets down, you still have your project on your computer !

##Remote commits vs Local commits
A consequence of centralization of a single server is that every time you'll need to commit you'll need a network connection, and depending on your upload capacity and other parameters, some commits might be very slow to push to your remote while if you're using a distributed VCS like Git, you will be able to commit locally as long as your work is not finished, and will only need to push once which makes it more convenient for working without networks: imagine yourself working in a train, committing locally, and once you get back on a network, boom ! you just push your changes, instead of waiting for a network connection to finally commit one big commit to your remote.

A good point with local commits is that it allows you do many atomic commits full of sense. See, the more you perform changes on a project, the harder it gets to really define what's the nature and the scope of your change. Atomic commits are the solution to that problem !


##Additional Resources
 - [Version Control Comparison](https://www.youtube.com/watch?v=eDRt9wI15mI)
 - [Centralized vs Distributed Version Control in 90 seconds](https://www.youtube.com/watch?v=_yQlKEq-Ueg)

 ---

 Go [back to the home page](../README.MD).
