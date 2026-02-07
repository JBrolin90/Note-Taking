file:: [progit_1767792997749_0.pdf](../assets/progit_1767792997749_0.pdf)
file-path:: ../assets/progit_1767792997749_0.pdf

- #ProGit #PDF  #Git #Bare #Sparse #[[Git remote]]
-
- ![progit.pdf](../assets/progit_1767807943444_0.pdf)
-
- ![progit.pdf](../assets/progit_1767792997749_0.pdf)
- In order to initially set up any Git server, you have to export an existing repository into a new bare repository — a repository that doesn’t contain a working directory. This is generally straightforward to do. In order to clone your repository to create a new bare repository, you run the clone command with the --bare option. By convention, bare repository directory names end with the suffix .git, like so:
  hl-page:: 116
  ls-type:: annotation
  id:: 695e61c8-3832-472d-8394-97ee2bff99e8
  hl-color:: yellow
- ```bash
  $ git clone --bare my_project my_project.git
  ```
- Cloning into bare repository 'my_project.git'... done. You should now have a copy of the Git directory data in your my_project.git directory.
-
-
-
-
-