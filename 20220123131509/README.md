# Getting Started With `gh`

My current distro is Ubuntu 20.04 LTS, so the installation steps are as
follows.

```BASH
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null

sudo apt update
sudo apt install gh
```

Follow whatever option you want for configuration.

Related:

* Installing `gh` on Linux and BSD
	<https://github.com/cli/cli/blob/trunk/docs/install_linux.md>
* `gh` manual
	<https://cli.github.com/manual/>
