# ansible_podman_connection

## run container

```sh
podman run -it --rm --name test_container_1 ubi8/ubi /bin/bash
```

## ping

- inventory

    ```
    test_container_1 ansible_connection=podman
    ```

### run

```sh
ansible -i hosts all -m ping 
```

## become

- inventory

    ```
    test_container_1 ansible_connection=podman ansible_become_method=su
    ```

- playbook - become.yml

    ```
    - hosts: all
      gather_facts: false
      become: yes
      tasks:
        - name: install wget
          dnf:
            name: wget
    ```

### run

```sh
ansible-playbook -i hosts become.yml
```

