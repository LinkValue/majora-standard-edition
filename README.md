# majora-standard-edition

Standard edition of symfony project using majora librairies, patterns and dev tools



## Installation

The following steps will show you how to create a new Symfony application named `majora-standard-edition`, feel free to replace this name by **your** project name.

1. Set the name of the directory that will contain your Symfony application

    ```bash
    PROJECT_NAME=majora-standard-edition
    ```

2. Clone repository, rebuild .git directory and download Ansible roles

    ```bash
    git clone --depth=1 git@github.com:LinkValue/majora-standard-edition.git $PROJECT_NAME && cd $PROJECT_NAME
    rm -rf .git && git init
    make vm-download
    ```

3. Customize VM provisioning

    - Replace all "majora-standard-edition" occurrences by your project name in `Vagrantfile` and customize the VM IP address of the VM if needed.

    - You may want to install some custom stuff in your VM, by modifying `ansible/app.yml` (you could add `nodejs` for example or remove `sass` if you'll use pure CSS). See [this repository](https://github.com/LinkValue/majora-ansible-playbook) to know which roles and variables are available.

    - Set your private variables (such as "composer_github_token") in `ansible/vars.local.yml`.

4. Edit your `/etc/hosts` file to bind your project URL to your VM IP address

    ```
    ### majora-standard-edition ###
    192.168.100.10 majora-standard-edition.dev
    ```

5. Create VM and install project dependencies

    ```bash
    WORKSPACE=/var/www/$PROJECT_NAME
    make vm-provision vm-project-prepare
    ```

Your empty Symfony application should be accessible at http://majora-standard-edition.dev/app_dev.php/
