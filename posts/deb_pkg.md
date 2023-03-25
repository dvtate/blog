# How To Create Debian Packages
This guide is a tldr version of [this video](https://www.youtube.com/watch?v=ep88vVfzDAo).

Note: Commands here are just for examples. They will NOT run as they are shown here. You have to adapt them to your own needs and system. 

1. Create the directory to hold the project:

    `mkdir /home/USER/debpkgs/my-program_version_architecture`

2. Create a directory called "DEBIAN" inside the project directory:

    `mkdir /home/USER/debpkgs/my-program_version_architecture/DEBIAN`

3. Copy files into project root directory and include the final paths:

    `/usr/bin/` would be `/home/USER/debpkgs/my-program_version_architecture/usr/bin/`

    `/opt/` would `/home/USER/debpkgs/my-program_version_architecture/opt/`

4. Create a control file in DEBIAN:

    `touch /home/USER/debpkgs/my-program_version_architecture/DEBIAN/control`

5. Now add the necessary metadata to the control file:
    ```
    Package: my-program
    Version: 1.0-1
    Architecture: all
    Essential: no
    Priority: optional
    Depends: packages, my-program, needs, to, run
    Recommended: other, useful, packages
    Maintainer: Your Name <me@example.com>
    Copyright: 2022 Your Name <me@example.com>
    Files: *
    Description: A short description of my-program that 
     will be displayed when the package is being selected for installation. 
    ```
6. If desired a "preinst" and/or "postinst" script can be added that execute before and/or after installation. They must be given proper execute permissions to run:

    `touch /home/USER/debpkgs/my-program_version_architecture/DEBIAN/postinst`

    Add commands you'd like to run in postinst and then set the permissions to 755.

7. Now generate package:

    `dpkg-deb --build /home/USER/debpkgs/my-program_version_architecture`

8. The package will be in `/home/USER/debpkgs`