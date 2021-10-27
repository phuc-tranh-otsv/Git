# Hotfix workflows

## "Traditional" gitflow workflow

1. Create `hotfix-branch` from `release`
2. Commit to `hotfix-branch`
3. Merge `hotfix-branch` into both `release` and `develop`

#### Pros

 * Simple; everybody understands it

#### Cons

 * `release` and `develop` have different histories due to differing merge parents (not *really* an issue if you re-branch `release` every time)
 * Potential conflicts when merging into `develop`
 * Risk of merging release-only commits (e.g. version bumps) into `develop`

## Rebase workflow

1. Create `hotfix-branch` from `develop`
2. Commit to `hotfix-branch`
3. Merge `hotfix-branch` into `develop`
4. Rebase (or cherry-pick) `hotfix-branch` onto `release`<sup>1</sup>

#### Pros

 * `release` and `develop` have the same histories (`release` is fast-forwarded)
 * No risk of merging unwanted commits into `release` or `develop`

#### Cons

 * Many people are uncomfortable with rebase (although in this case the rebase is non-destructive)

------------------

<sup>1</sup> Using something like:

```
$ git rebase --onto hotfix-branch develop release
First, rewinding head to replay your work on top of it...
Fast-forwarded release to hotfix-branch.
```