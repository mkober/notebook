* Default Configurations
git config --global pull.rebase true
git config --global fetch.prune true
git config --global diff.colorMoved zebra

* Remove file from git history
git filter-branch --index-filter 'git rm -rf --cached --ignore-unmatch path_to_file' HEAD