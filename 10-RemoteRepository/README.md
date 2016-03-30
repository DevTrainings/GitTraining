# Working with remote repository

## Introduction

## Commands

## Comments

* Your repository can have multiple remotes.
  * This is used for example on _Github_ when you fork a repository and you
    run _clone_ repository using desktop client.
    * _origin_ remote usually points to your fork.
    * _upstream_ remote points to the main repository.
    * Different versions of the Github Desktop can map repositories differently.
    * You can use ```git remote --verbose``` to see details about mappings.
* If you move the repository to another _git_ server you can re-map your
  remotes easily.
  * Let's consider standard setup with remote named ```origin``` pointing to
    obsolete server.
  * Let's remove the current mapping:

```
git remote remove origin
```

  * Now let's add the mapping with new location:

```
git remote add origin https://server.com/MyRepo.git
```

  * Here ```origin``` defines the name of remote.
