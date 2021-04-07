# Ansible Role Repository

Example Ansible Role used for demo purposes to highlight best practices.

## Requirements

None

## Role Variables

It is important to understand how variables should be defined within an Ansible Role and how best to organize them.

### Proper Naming


### Handling Required Variables

### Handling Public Variables

Create public variables in the `defaults/main.yml` area.

### Handling Private Variables

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

## License

BSD

## Author

John Wadleigh
