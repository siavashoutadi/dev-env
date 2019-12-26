# Setup a development environment

Download the delivery artifact from release tab and untar it. For example:

```shell
wget https://github.com/siavashoutadi/dev-env/releases/download/1.1.0/dev-env-1.1.0.tar.gz
tar -xvzf dev-env-*.tar.gz
```

Modify the inventory file to include the hostname of the machine you want to run this playbook towards and create the extra_vars.yaml to customize the playbook and finally run the playbook:

```shell
ansible-playbook site.yml -K --extra-vars="@extra_vars.yaml"
```

If you want to install it on your local machine then you can simply use the inventory as is and make ansible-playbook to use the local connection:

```shell
ansible-playbook site.yml --connection local -K --extra-vars="@extra_vars.yaml"
```

**Note**: extra_vars.yaml is optional. It is used to customize the playbook and can be omitted. Below there is an example for extra_vars.yaml that shows how the playbook can be customized:

```yaml
git_user: user1
git_config:
  - name: user.name
    value: User1
  - name: user.email
    value: user1@mail.com
  - name: alias.co
    value: "checkout"
  - name: alias.st
    value: "status"
visual_studio_code_users:
  - username: user1
    visual_studio_code_extensions:
      - vscoss.vscode-ansible
      - oderwat.indent-rainbow
      - ms-python.python
      - 2gua.rainbow-brackets
      - redhat.vscode-yaml
    visual_studio_code_settings:
      {
        "editor.formatOnSave": true,
        "editor.formatOnPaste": true,
        "files.trimTrailingWhitespace": true,
        "[yaml]":
          {
            "editor.insertSpaces": true,
            "editor.tabSize": 2,
            "editor.detectIndentation": false,
          },
        "python.linting.flake8Args": ["--ignore=E24,W504", "--verbose"],
      }
intellij_users:
  - username: user1
    intellij_jdks:
      - name: "{{ ansible_local.java.general.version }}"
        home: "{{ ansible_local.java.general.home }}"
    intellij_default_jdk: "{{ ansible_local.java.general.version }}"
pip_install_packages:
  - name: setuptools
  - name: molecule
  - name: ansible
  - name: testinfra
  - name: docker
  - name: libvirt-python
ruby_install_gems:
  - jekyll
ruby_install_gems_user: user1
dev_env_packages:
  - clipit
  - terminator
```
