# Terraform Beginner Bootcamp 2023

## Semantic Versioning :mage:

This project is going utilize semantic versioning for its tagging. 

[semver.org](https://semver.org/)

The general format : 

**MAJOR.MINOR.PATCH**, eg `1.0.1`

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes

## Install the Terraform CLI 

### Considerations with the Terraform CLI Changes 

The Terraform CLI installation instructions have changed due to GPG keyring updates. Therefore, we needed to refer to the latest Terraform Documentation for CLI installation instructions and update our installation scripts accordingly.


[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

### Considerations for Linux Distrubtion 

This project is built for Ubuntu. Please ensure that your Linux distribution is compatible and make any necessary changes according to your distribution's requirements.

[How To Check OS Version in Linux](https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/)

Example of checking OS Version :

```
$ cat /etc/os-release

PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```


### Refactoring into Bash Scripts  

While fixing the Terraform CLI GPG depreciation issue, we noticed that the bash script steps involved a considerable amount of code. Therefore, we decided to create a bash script for installing the Terraform CLI.

This bash scripte is located here : [./bin/install_terraform_cli](.bin/install_terraform_cli)

- This will help keep the Gitpod Task File ([.gitpod.yml](.gitpod.yml)) tidy.

- This will allow for easier debugging and manual execution of Terraform CLI installation.

- This will enhance portability for other projects that require Terraform CLI installation.



### Shebang Considerations 

A Shebang (pronounced Sha-bang) informs a bash script about the program that will interpret the script, e.g., ` #!/bin/bash`

ChatGPT recommends using this format for bash: `#!/usr/bin/env bash`

- This format is beneficial for portability across different OS distributions.
- It searches the user's PATH for the bash executable.
 

https://en.wikipedia.org/wiki/Shebang_(Unix)


#### Execution Considerations


When executing the bash script, we can use the `./` shorthand notation to execute the bash script.

eg  `./bin/install_terraform_cli `

If we are using a script in .gitpod.yml, we need to specify the program to interpret it.

eg `source ./bin/install_terraform_cli`




#### Linux Permissions Considerations
 
To make our bash scripts executable, we needed to change the Linux permissions so that the fix can be executed in user mode.



```sh
chomd u+x ./bin/install_terraform_cli
```

 Alternatively: 

```sh
chomd 744 ./bin/install_terraform_cli
```

https://en.wikipedia.org/wiki/Chmod


### GitHub Lifecycle (Before, Init, Command)


We need to exercise caution when using "Init" because it will not rerun if we restart in an existing workspace.



https://www.gitpod.io/docs/configure/workspaces/tasks


### Working Env Vars

### Env Command 

We can list all Environment Variables (Env Vars) using the 'env' command.

To filter out specific env vars, you can use grep, e.g., `env | grep AWS_`


### Setting and Unsetting Env Vars 

In the terminal, we can set an environment variable using export `HELLO='world'`

In the terminal, we can unset an environment variable using `unset HELLO`

We can set an environment variable temporarily when just running a command:


```sh 
HELLO='world' ./bin/print_message
```

Within a bash script, we can set an environment variable without writing 'export,' e.g.:

```sh
#!/usr/bin/env bash

HELLO='world'

echo $HELLO
```

#### Printing Vars

We can print an env var using eg. `echo $HELLO`


#### Scoping of Env Vars

When you open new bash terminals in VSCode, they will not be aware of environment variables (env vars) that you have set in another window.

If you want environment variables to persist across all future bash terminals that are opened, you need to set environment variables in your bash profile, 
e.g `bash_profile`


#### Persisting Env Vars in Gitpod

We can persist environment variables in Gitpod by storing them in the Gitpod Secrets Stage:

```
gp env HELLO='world'
```

All future workspaces launched will set the environment variables for all bash terminals opened in those workspaces.

You can also set environment variables in the `.gitpod.yml` , but this can only contain non-sensitive environment variables.

