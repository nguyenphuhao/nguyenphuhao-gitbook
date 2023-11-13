# How to change local url from Gitlab to Github

**If you want to use both GitHub and GitLab:**

```
git remote add github <your-github-url>  # create a remote for GitHub
git remote add gitlab <your-gitlab-url>  # create another remote for GitLab
git push -u github <local_branch_name>   # set the default upstream to GitHub
```

**If you want to change your remote URL from GitLab to GitHub**:

```
git remote set-url origin <your-github-url>  # use GitHub as your (only) origin
```

\
