# Dependencies (coupling)

Some programs **rely** on other programs to work. These other programs are called ***dependencies***.

**e.g.** If I write a messaging app, and I want my messages to be encrypted, instead of creating a way to encrypt the messages myself, I'll use a package that someone else has written, which will the encryption for me. Now when you want to install my program, you need my program, but you also need the package I used to to encrypt the messages. My program *depends* on the other program.

Program ***X*** uses Library ***Y***.

***X*** depends on ***Y***. ***Y*** is ***X***'s dependency.

---

***Fun fact**: When Ubuntu installs new programs, it installs them from a big warehouse of programs called a repository (repo). If it notices that a program depends on another program, it will install both at the same time.*