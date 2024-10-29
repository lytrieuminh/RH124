#Lab: Manage Files from the Command Line
#🐱‍🚀🐱‍👤🐱‍💻🐱‍🐉🐱‍👓🐱‍🏍✨

[student@workstation ~]$ lab start files-review

#Use the ssh command to log in to the serverb machine as the student user. The system's configuration supports the use of SSH keys for authentication.
[student@workstation ~]$ ssh student@serverb

#Create a directory called project_plans in the Documents directory. The Documents directory is placed in the student user's home directory. Create two empty files in the project_plans directory called season1_project_plan.odf and season2_project_plan.odf.
#Hint: If the ~/Documents directory does not exist, then use the mkdir command -p option to create it.
[student@serverb ~]$ mkdir -p ~/Documents/project_plans
[student@serverb ~]$ touch ~/Documents/project_plans/{season1,season2}_project_plan.odf
[student@serverb ~]$ ls -lR Documents/

#Create sets of empty practice files to use in this lab. If you do not immediately recognize the intended shell expansion shortcut, then use the solution to learn and practice. Use shell tab completion to locate file path names. Create 12 files with tv_seasonX_episodeY.ogg names in the /home/student directory. Replace X with the season number and Y with that season's episode, for two seasons of six episodes each.
[student@serverb ~]$ touch tv_season1_episode1.ogg tv_season1_episode2.ogg tv_season1_episode3.ogg tv_season1_episode4.ogg tv_season1_episode5.ogg tv_season1_episode6.ogg
[student@serverb ~]$ touch tv_season2_episode1.ogg tv_season2_episode2.ogg tv_season2_episode3.ogg tv_season2_episode4.ogg tv_season2_episode5.ogg tv_season2_episode6.ogg

OR
[student@serverb ~]$ touch tv_season{1..2}_episode{1..6}.ogg
[student@serverb ~]$ ls tv*

#As the author of a successful series of mystery novels, you are editing your next bestseller's chapters for publishing. Create eight files with mystery_chapterX.odf names. Replace X with the numbers 1 through 8.
[student@serverb ~]$ touch mystery_chapter{1..8}.odf
[student@serverb ~]$ ls mys*

#Use a single command to create two subdirectories called season1 and season2 under the Videos directory to organize the TV episodes. Move the appropriate TV episodes into the season subdirectories. Use only two commands, and specify destinations with relative syntax.
    #Create two subdirectories called season1 and season2 under the Videos directory by using a single command.
    [student@serverb ~]$ mkdir -p Videos/season{1..2}
    [student@serverb ~]$ ls Videos

    #Move the appropriate TV episodes into the season subdirectories by using only two commands.
    [student@serverb ~]$ mv tv_season1* Videos/season1
    [student@serverb ~]$ mv tv_season2* Videos/season2
    [student@serverb ~]$ ls -R Videos

#Create a two-level directory hierarchy with a single command to organize the mystery book chapters. Create the my_bestseller subdirectory under the Documents directory, and create the chapters subdirectory under the new my_bestseller directory. Create three more subdirectories directly under the my_bestseller directory with a single command. Name these subdirectories editor, changes, and vacation. You do not need to use the mkdir -p command to create parents because the my_bestseller parent directory exists.
    #Create the my_bestseller directory under the Documents directory. Create the chapters directory under the my_bestseller directory.
    [student@serverb ~]$ mkdir -p Documents/my_bestseller/chapters
    [student@serverb ~]$ ls -R Documents

    #Create three directories called editor, changes, and vacation, under the my_bestseller directory by using a single command.
    [student@serverb ~]$ mkdir Documents/my_bestseller/{editor,changes,vacation}
    [student@serverb ~]$ ls -R Documents

#Change to the chapters directory. Use the tilde (~) home directory shortcut to move all book chapters to the chapters directory, which is now your current directory. Use the simplest syntax to specify the destination directory.

You want to send the first two chapters to the editor for review. Move only those two chapters to the editor directory to avoid modifying them during the review. Starting from the chapters subdirectory, use brace expansion with a range to specify the chapter file names to move and a relative path for the destination directory.

While on vacation, you intend to write chapters 7 and 8. Use a single command to move the files from the chapters directory to the vacation directory. Specify the chapter file names by using brace expansion with a list of strings and without using wildcard characters.
    #Change to the chapters directory and use the tilde (~) home directory shortcut to move all book chapters to the chapters directory.
    [student@serverb ~]$ cd Documents/my_bestseller/chapters
    [student@serverb chapters]$ mv ~/mystery_chapter* .
    [student@serverb chapters]$ ls

    #Move the first two chapters to the editor directory. Use brace expansion with a range to specify the chapter file names to move and a relative path for the destination directory.
    [student@serverb chapters]$ mv mystery_chapter{1..2}.odf ../editor
    [student@serverb chapters]$ ls

    #Use a single command to move the chapters 7 and 8 from the chapters directory to the vacation directory. Specify the chapter file names by using brace expansion with a list of strings and without using wildcard characters.
    [student@serverb chapters]$ mv mystery_chapter{7,8}.odf ../vacation
    [student@serverb chapters]$ ls

#Change your working directory to ~/Videos/season2, and then copy the first episode of the season to the vacation directory. Use a single cd command to change from your working directory to the ~/Documents/my_bestseller/vacation directory. List its files. Use the previous working directory argument to return to the season2 directory. (This argument succeeds if the last directory change with the cd command used only one command rather than several cd commands.) From the season2 directory, copy the episode 2 file into the vacation directory. Use the shortcut again to return to the vacation directory.
    #Change your working directory to ~/Videos/season2, and then copy the first episode of the season to the vacation directory.
    [student@serverb chapters]$ cd ~/Videos/season2
    [student@serverb season2]$ cp *episode1.ogg ~/Documents/my_bestseller/vacation

    #Use a single cd command to change from your working directory to the ~/Documents/my_bestseller/vacation directory, list its files, and use the - argument to return to the previous directory. Copy the episode 2 file into the vacation directory. Use the cd command with the - argument to return to the vacation directory.
    [student@serverb season2]$ cd ~/Documents/my_bestseller/vacation
    [student@serverb vacation]$ ls
    [student@serverb vacation]$ cd -
    [student@serverb season2]$ cp *episode2.ogg ~/Documents/my_bestseller/vacation
    [student@serverb season2]$ cd -
    [student@serverb vacation]$ ls

#The authors of chapters 5 and 6 want to experiment with possible changes. Copy both files from the ~/Documents/my_bestseller/chapters directory to the ~/Documents/my_bestseller/changes directory to prevent these changes from modifying original files. Navigate to the ~/Documents/my_bestseller directory. Use square-bracket pattern matching to specify which chapter numbers to match in the filename argument of the cp command.
[student@serverb vacation]$ cd ~/Documents/my_bestseller
[student@serverb my_bestseller]$ cp chapters/mystery_chapter[56].odf changes
[student@serverb my_bestseller]$ ls chapters
[student@serverb my_bestseller]$ ls changes

#Change your current directory to the changes directory and use the date +%F command with command substitution to copy the mystery_chapter5.odf file to a new file that includes the full date. Use the mystery_chapter5_YYYY-MM-DD.odf name format.

[student@serverb my_bestseller]$ cd changes
[student@serverb changes]$ cp mystery_chapter5.odf mystery_chapter5_$(date +%F).odf

#By using command substitution with the date +%s command, make another copy of mystery_chapter5.odf, and append the current time stamp (as the number of seconds since the epoch, 1970-01-01 00:00 UTC) to ensure a unique file name.
[student@serverb changes]$ cp mystery_chapter5.odf mystery_chapter5_$(date +%s).odf
[student@serverb changes]$ ls

#After further review, you decide that you do not need the plot changes. Delete the changes directory.

If it is necessary, then navigate to the changes directory and delete all the files within the directory. You cannot delete a directory when it is the current working directory.

Change to the parent directory of the changes directory. Try to delete the empty directory by using the rm command without the -r recursive option. This attempt should fail. Finally, use the rmdir command to delete the empty directory, which succeeds.

When the vacation is over, you no longer need the vacation directory. Delete it by using the rm command with the recursive option.

When finished, return to the student user's home directory.
    #Delete the changes directory. Change to the parent directory of the changes directory, and try to delete the empty directory by using the rm command without the -r recursive option, which should fail. Use the rmdir command to delete the empty directory.
    [student@serverb changes]$ rm mystery*
    [student@serverb changes]$ cd ..
    [student@serverb my_bestseller]$ rm changes
    rm: cannot remove 'changes': Is a directory
    [student@serverb my_bestseller]$ rmdir changes
    [student@serverb my_bestseller]$ ls

    #Delete the vacation directory by using the rm command with the -r option. Return to the student user's home directory.
    [student@serverb my_bestseller]$ rm -r vacation
    [student@serverb my_bestseller]$ ls

#Create a hard link to the ~/Documents/project_plans/season2_project_plan.odf file called ~/Documents/backups/season2_project_plan.odf.back. A hard link protects against accidental deletion of the original file and keeps the backup file updated as you change the original file.
Hint: If the ~/Documents/backups directory does not exist, then use the mkdir command to create it.
    #Create a hard link to the ~/Documents/project_plans/season2_project_plan.odf file called ~/Documents/backups/season2_project_plan.odf.back.
    [student@serverb ~]$ mkdir ~/Documents/backups
    [student@serverb ~]$ ln ~/Documents/project_plans/season2_project_plan.odf ~/Documents/backups/season2_project_plan.odf.back
    [student@serverb ~]$ ls -lR ~/Documents/

#Return to the workstation system as the student user.
[student@serverb ~]$ exit


✨lab grade files-review
✨lab finish files-review
