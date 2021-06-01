# Commands

- `sudo`

    A program used to execute a command as administrator (administrative privileges).

    ```bash
    sudo <command>
    ```

    To switch to root user for a limited amount of time

    ```bash
    sudo -s
    ```

    Use `exit` to exit root mode

    To be an administrator, you must be added to the "sudo" group, you can do that from a root user by typing:

    ```bash
    usermod -aG sudo <user>
    ```

    In order to execute the last command typed as root user, type:

    ```bash
    sudo !!
    ```

- `su`

    Used to switch to another user, without logging out.

    ```bash
    su <user>
    ```

    Note that the user's password is required

    You can use `su - <user>` to move to another user and load their bash settings and home folder

- `pip`
- `history`

    Prints the last 1000 commands that have been typed in the terminal

- `users`

    View who use logged in to the system

    ```bash
    users
    ```

- `id`

    Show the user id

    ```bash
    id
    ```

- `watch`

    Reruns a command every 2 seconds

    ```bash
    watch free -h
    ```

- `killall`

    Stops a process

    ```bash
    killall firefox
    ```

## System related

- `apt`
- `adduser`

    Used to add new users.

    ```bash
    adduser <user_name>
    ```

    To add a user to a group, use:

    ```bash
    adduser <user> <group>
    ```

    This should be run as root.

- `free`

    Shows how much of free memory in the system

    ```bash
    free -h
    ```

## Editing

- `tar`

    Used to extract (or "untar") files from an archive.

    ```bash
    tar -xvf <archive>
    ```

- `chown`

    Change the owner and the owner group of a directory or a file.

    ```bash
    chown <user>:<group> <dir/file>
    ```

    To change just the owner, type:

    ```bash
    chown <user> <dir/file>
    ```

- `chmod`

    Change permissions for a file or a directory

    ```bash
    chmod 755 file
    ```

    ```bash
    chmod +x file
    ```

    [Commands%20f58b8edae4e949dd98e8be4abaf5393a/permissions.webp](Commands%20f58b8edae4e949dd98e8be4abaf5393a/permissions.webp)

- `file`

    Tells you the type of the file

    ```bash
    file <file_name>
    ```

    Some terminals are color-coded, which means every type has a specific color; Lovely option

- `touch`

    Change a file's date of modification (useful for backups)

    ```bash
    touch file
    ```

    If the file doesn't exist, `touch` will create it.

- `cp`

    Copy a file or directory (useful also for backup when working on a file that you may screw it all up)

    ```bash
    cp file file.bak
    ```

- `mv`

    Moves a file from one location or another

    ```bash
    mv ~/file ~/Documents/
    ```

    `mv` can also be used to rename a file

    ```bash
    mv file1 file2
    ```

- `rm`

    Remove a file

    ```bash
    rm file
    ```

    Remove a directory

    ```bash
    rm -r dir
    ```

- `rmdir`

    Remove empty directories

    ```bash
    rmdir dir
    ```

- `cat`

    Show the content of a file

    ```bash
    cat file
    ```

    You can write the input you type in a file *(append to the bottom without erasing the whole thing)* using `cat >> file`

    You can add text to file replacing the existing one using `cat > file`

    You can also cat (concatenate) two files or more using `cat file1 file2`

## Redirection & piping

- `|`

    Give the output of the first command as an input for the second one

    ```bash
    history | less
    ```

- `>`

    Write the output of a command into a file

    ```bash
    ls -la / > lsout.txt
    ```

## Search

- `ls`

    Stands for "list storage"; It lists the files and folders contained within a specific directory

    The following example lists the home directory (tilde "~" stands for home directory)

    ```bash
    ls ~
    ```

    `ls -a` lists also hidden files and folder (their names start with a point)

    `ls -l` lists additional information (owner, group, permissions, ...)

- `which`

    Tells you the location of a command or if it's installed or not

    ```bash
    which cal
    ```

- `locate`

    Print the location of a file or a directory (it takes file names or parts of the names)

    ```bash
    locate text.txt
    ```

    The command `updatedb` updates the database to be used by `locate` and other commands

## Navigation

- `pwd`
- `cd`

    Which means "change directory"

    - Go to home directory

    ```bash
    cd
    ```

    - Go one level up

    ```bash
    cd ..
    ```

- `pushd` & `popd` & `dirs`

    Used to work with the command line directory stack

    `pushd` saves the current working directory in memory so it can be returned to at any time, optionally changing to a new directory

    ```bash
    pushd [path]
    ```

    `pushd` can be used without option and the path at the top of the directory stack is used, which has the effect of toggling between two directories

    `popd` returns to the path at the top of the directory stack

    ```bash
    popd
    ```

    `dirs` prints the stack

- `more` & `less`

    `more` shows the content of a file in pages that can be navigated with spacebar (just down; no going back)

    ```bash
    more file
    ```

    `less` shows the content of a file in pages that can be navigated with arrow keys (down & up)

    ```bash
    less file
    ```

## Getting help

- `whatis`

    Gives you a little explanation about a command

    ```bash
    whatis cal
    ```

- `apropos`

    Gives a bunch of commands related to something you want

    ```bash
    apropos time
    ```