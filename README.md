# Git Merge and Conflict Example

For full guide, please refer on : 
1. [http://githowto.com/creating_a_conflict](http://githowto.com/creating_a_conflict) 
2. [http://githowto.com/resolving_conflicts](http://githowto.com/resolving_conflicts)

Credit on original author

## Case study

In this repo there is three branch 
- `master`
- `branch_a` (fork from master)
- `branch_b` (fork from master)

## Starting the Chaos : Conflict and Merge
```
# Clone this repo
git clone https://github.com/todiadiyatmo/resolve_conflict/

# checkout branch_a
git checkout -b local origin/branch_a 

# to merge branch_b
git merge origin/branch_b 
```

When you merge branch a and b there will be conflict. 

![](http://todiadiyatmo.com/img/Selection_343.png "Conflict message")


Now examine the `home.html`, which is in conflict

![](http://todiadiyatmo.com/img/Selection_338.png "Home HTML")

Line 7 (`<<<<<<<`) is a special code from git to mark the begining of the conflict
Line 9 (`=======`) is the separator between the code from local and remote branch
Line 11 (`>>>>>>`) ending of merge conflict

The code from `branch_a` is between line 7 and 9. Code from `branch_b` is between line 9 and 11.

## Manualy Resolving Merge Conflict

You can resolve the conflict without tool, just pick the line you want to keep. and delete the : 

```
<<<<<<< HEAD
```
and
```
=======
```
and
```
>>>>>>> branch_b
```

For example if we want to use code from `branch_b` instead of `branch_a` :

![](http://todiadiyatmo.com/img/Selection_342.png "using branch_b")

Remove line 7,8,9 + line 11.

To finish the merging process, issue a merge command

```
git add .
git commit -m "fixed merge conflict,using branch_b"
```

## Resolving Merge Conflict Using Merge Tool 

### Preparing the merge tool
To easily merge a conflict you will need a good merge tool. Some options in ubuntu/linux is : 

- meld
- kdiff3 

No make your prefered merge tool as the default merge tool using this command

```
git config --global merge.tool kdiff3
```

You can run merge tool by using this command : 
```
git mergetool -t kdiff3
```
**OR**
```
# Assuming you already set the mergetool using global config
git mergetool
```

This message will appear if you are running `git mergetool` command :

![](http://todiadiyatmo.com/img/Selection_344.png "mergetool command")

### Merging Using KDiff3

KDiff 3 is my preference mergetool because it has 4 pane 
1. Base -> Before Conflict
2. Local -> Your Current Branch
3. Remote -> Remote Branch that you want to merge
4. Combined File 

![](http://todiadiyatmo.com/img/Selection_339.png "KDiff3 Pane")

To merge using kdiff3

![](http://todiadiyatmo.com/img/Selection_340.png "KDiff3 Merging")

After you satistfied with your merged file, don't forget issue a save command on the kdiff3

Finnaly, issue a commit command 
```
git add .
git commit -m "fixed merge conflict,using"
```

