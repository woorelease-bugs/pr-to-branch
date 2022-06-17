# Test repo for [woorelease](https://github.com/woocommerce/woorelease)

`woorelease` misses all PRs that were merged to a different branch that's being released.
That applies to 
- feature branches
- PRs made to other PRs
- Releasing from `release/*` branch

## Steps to reproduce

![image](https://user-images.githubusercontent.com/17435/174351562-c58f29c9-b69b-4a7e-9f35-920243ee9c77.png)


1. Release `1.0.0` from `develop` (manually, as you [cannot do that with the woorelease either](https://github.com/woorelease-bugs/initial-release))
2. Marge a PR directly to `develop`, with a changelog note

### Feature branches
3. Create a (feature) branch, like `add/foo`, with a commit
4. Create a PR to merge `add/foo` to `develop`, with a changelog note
5. Create another branch `add/bar` with a commit, and a PR to `add/foo` with a changelog note
6. Merge the PR `add/bar` to `add/foo`
7. Merge the PR `add/foo` to `develop`
8. Try releasing `1.0.1` from `develop`
	```
	woorelease cl:generate --product_version=1.0.1 https://github.com/woorelease-bugs/pr-to-branch/tree/develop
	```	
	```= 1.0.1 - 2022-06-17 =
	* Add - README description directly to develop.
	* Add - a workflow to attach label based on PR branchname directly to `develop`.
	```

9. Use https://github.com/woorelease-bugs/pr-to-branch/releases/new?tag=1.0.1&branch=develop "Generate release notes" instead 
	```
	## What's Changed
	### New Features 🎉
	* Add README description directly to develop by @tomalec in https://github.com/woorelease-bugs/pr-to-branch/pull/1
	* Add release.yml to `add/branch-labels` by @tomalec in https://github.com/woorelease-bugs/pr-to-branch/pull/3
	* Add a workflow to attach label based on PR branchname directly to `develop` by @tomalec in https://github.com/woorelease-bugs/pr-to-branch/pull/2
	```



## Release branches
3. `git checkout -b release/1.0.1` on the head of `develop`
4. `git push origin release/1.0.1`
5. Try releasing `1.0.1` from `release/1.0.1`
	```
	woorelease cl:generate --product_version=1.0.1 https://github.com/woorelease-bugs/pr-to-branch/tree/release/1.0.1
	```	
	```
	= 1.0.1 - 2022-06-16 =
	```
	
6. Use https://github.com/woorelease-bugs/pr-to-branch/releases/new?tag=1.0.1&branch=release/1.0.1 "Generate release notes" instead 
	```
	## What's Changed
	### New Features 🎉
	* Add README description directly to develop by @tomalec in https://github.com/woorelease-bugs/pr-to-branch/pull/1
	* Add release.yml to `add/branch-labels` by @tomalec in https://github.com/woorelease-bugs/pr-to-branch/pull/3
	* Add a workflow to attach label based on PR branchname directly to `develop` by @tomalec in https://github.com/woorelease-bugs/pr-to-branch/pull/2
	```

## Prerequisites

We aim to support the latest two minor versions of WordPress, WooCommerce, and PHP. (L-2 policy)

-   WordPress 5.7+
-   WooCommerce 6.0+
-   PHP 7.3+

<p align="center">
	<br/><br/>
	Made with 💜 by <a href="https://woocommerce.com/">WooCommerce</a>.<br/>
	<a href="https://woocommerce.com/careers/">We're hiring</a>! Come work with us!
</p>
