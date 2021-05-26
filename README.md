# ansible_podman_connection

## run container

```sh
podman run -it --rm --name test_container_1 ubi8/ubi /bin/bash
```

## ping

- inventory - hosts

    ```
    test_container_1 ansible_connection=podman
    ```

### run

```sh
ansible -i hosts all -m ping 
```

## in different with inventory name and container name

- inventory - hosts

    ```
    test1 ansible_host=test_container_1 ansible_connection=podman
    ```

### run

```sh
ansible -i hosts all -m ping 
```

## become

- inventory - hosts

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

