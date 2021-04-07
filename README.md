# Ansible Role Repository

Example Ansible Role used for demo purposes to highlight best practices.

## Requirements

None

## Role Variables

It is important to understand how variables should be defined within an Ansible Role and how best to organize them.

### Proper Variable Naming

Variables should be named using only `lowercase` and `underscore` characters. This is now a rule I added to `ansible-lint` as of v5.0.7.

### Handling Required Variables

Add tasks in the `tasks/main.yml` to ensure required variables are defined. Often the `assert` module is the best for this.

### Handling Public Variables

Public variables are those that can be freely overridden by anyone, and are otherwise set to a default value. 

Create public variables in the `defaults/main.yml` area.

### Handling Private Variables

Private variables are those that are defined purely so the internal code for the Ansible Role can perform its job. They are not intended to be read or used or referenced by anyone outside of this Ansible Role. In this case `private` means `internal`.

Create private variables in the `vars/main.yml` area.

### Handling OS-specific Variables

Take a look at the following example Ansible Role that installs Java on multiple OS targets: [ansible-role-java](https://github.com/geerlingguy/ansible-role-java). Notice that it loads the OS-specific variables as one of the first steps in the `tasks/main.yml` area.

## Dependencies

Role dependencies are typically defined in the `meta/main.yml` file under the `dependencies:` section.

## Example Playbook

Include an example of how to use your role (for instance, with variables passed in as parameters):

```yaml
    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }
```

## Embedding Modules and Plugins

Roles are also a great place to put your custom modules or plugins. This allows other playbooks to use your modules/plugins. For modules, simply place your module script inside the `library` folder. For filter plugins, simply place the plugin script inside the `filter_plugins` folder. The same applies to the other plugin folders. These folders reside at the root of this repo.

When anyone wants to use your custom module/plugin, they simply write a playbook to import your role before they use it. For example:

```yaml
- hosts: webservers
  roles:
    - my_custom_modules
    - some_other_role_using_my_custom_modules
    - yet_another_role_using_my_custom_modules
```

It is important to note, you must **import** the role and not **include** the role. In the example above all roles are implicitly imported.

For more information please read [this](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html#embedding-modules-and-plugins-in-roles).

## Linting

The role uses `ansible-lint` to perform linting when you commit code locally using git. The `.pre-commit-config.yaml` configures `pre-commit` to trigger upon `git commit` command and load ansible-lint and run it against the staged files.

Below is an example of the output from `ansible-lint` on the current role. There are intended errors in this role.

```shell
$ git commit -m "Updated using ansible-lint"
[INFO] Initializing environment for https://github.com/ansible-community/ansible-lint.git:.[community,yamllint].
[INFO] Installing environment for https://github.com/ansible-community/ansible-lint.git.
[INFO] Once installed this environment will be reused.
[INFO] This may take a few minutes...
Ansible-lint.............................................................Failed
- hook id: ansible-lint
- exit code: 2

WARNING  Computed fully qualified role name of examples-repos-role-myrole does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

[WARNING]: While constructing a mapping from <unicode string>, line 3, column
1, found a duplicate dict key (password). Using last defined value only.
WARNING  Listing 22 violation(s) that are fatal
yaml: trailing spaces (trailing-spaces)
.pre-commit-config.yaml:8

yaml: too many blank lines (1 > 0) (empty-lines)
defaults/main.yml:6

unnamed-task: All tasks should be named
handlers/main.yml:3 Task/Handler: debug var=inventory_hostname

yaml: too many blank lines (1 > 0) (empty-lines)
handlers/main.yml:4

role-name: Role name ansible-examples-repos-role-myrole does not match ``^[a-z][a-z0-9_]+$`` pattern
meta/main.yml:0

yaml: too many blank lines (1 > 0) (empty-lines)
meta/main.yml:29

yaml: too many blank lines (1 > 0) (empty-lines)
tasks/debian.yml:9

unnamed-task: All tasks should be named
tasks/main.yml:25 Task/Handler: set_fact MyVar=this

unnamed-task: All tasks should be named
tasks/main.yml:29 Task/Handler: set_fact myvar=this

no-changed-when: Commands should not change things if nothing needs doing
tasks/main.yml:34 Task/Handler: shell  echo this

unnamed-task: All tasks should be named
tasks/main.yml:34 Task/Handler: shell  echo this

yaml: too few spaces before comment (comments)
tasks/main.yml:34

no-changed-when: Commands should not change things if nothing needs doing
tasks/main.yml:37 Task/Handler: shell  echo this

unnamed-task: All tasks should be named
tasks/main.yml:37 Task/Handler: shell  echo this

yaml: too few spaces before comment (comments)
tasks/main.yml:37

yaml: too many blank lines (1 > 0) (empty-lines)
tasks/main.yml:38

unnamed-task: All tasks should be named
tasks/redhat.yml:4 Task/Handler: debug msg=test

yaml: too many blank lines (1 > 0) (empty-lines)
tasks/redhat.yml:11

yaml: too many blank lines (1 > 0) (empty-lines)
tasks/windows.yml:4

yaml: no new line character at the end of file (new-line-at-end-of-file)
tests/test.yml:5

yaml: duplication of key "password" in mapping (key-duplicates)
vars/main.yml:10

yaml: too many blank lines (1 > 0) (empty-lines)
vars/main.yml:12

You can skip specific rules or tags by adding them to your configuration file:
# .ansible-lint
warn_list:  # or 'skip_list' to silence them completely
  - no-changed-when  # Commands should not change things if nothing needs doing
  - unnamed-task  # All tasks should be named
  - yaml  # Violations reported by yamllint
Finished with 21 failure(s), 1 warning(s) on 20 files.
```

## License

BSD

## Author

John Wadleigh
