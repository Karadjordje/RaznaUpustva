# -----------------------------------------------------------------
# .gitignore for WordPress
# Bare Minimum Git
#
# This file is tailored for a WordPress project
# using the default directory structure
#
# This file specifies intentionally untracked files to ignore
# http://git-scm.com/docs/gitignore
#
# NOTES:
# The purpose of gitignore files is to ensure that certain files not
# tracked by Git remain untracked.
#
# To ignore uncommitted changes in a file that is already tracked,
# use `git update-index --assume-unchanged`.
#
# To stop tracking a file that is currently tracked,
# use `git rm --cached`
# -----------------------------------------------------------------
# ignore everything in the root except the "wp-content" directory.
/*
!wp-content/
# ignore all files starting with .
.*
# track this file .gitignore (i.e. do NOT ignore it)
!.gitignore
# track .editorconfig file (i.e. do NOT ignore it)
!.editorconfig
# track readme.md in the root (i.e. do NOT ignore it)
!readme.md
# ignore all files that start with ~
~*
# ignore OS generated files
ehthumbs.db
Thumbs.db
# ignore Editor files
*.sublime-project
*.sublime-workspace
*.komodoproject
# ignore log files and databases
*.log
*.sql
*.sqlite
# ignore compiled files
*.com
*.class
*.dll
*.exe
*.o
*.so
*.map
# ignore packaged files
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip
*.map
# ignore everything in the "wp-content" directory, except:
# "mu-plugins" directory
# "plugins" directory
# "themes" directory
wp-content/*
!wp-content/mu-plugins/
!wp-content/plugins/
!wp-content/themes/
# ignore these plugins
wp-content/plugins/hello.php
# ignore specific themes
wp-content/themes/twenty*/
# ignore node/grunt dependency directories
node_modules/
bower_components