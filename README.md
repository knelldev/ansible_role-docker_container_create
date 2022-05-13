# docker.container.create

This include_role creates a docker container. The user id for docker container mapping is automatically computed.

## Requirements
- knelldev.docker_install

## Variables
| Name | Default | Type | Description |
| --- | --- | --- | --- |
| app_user | "{{ os_user }}" | str | The user name for docker container mapping |
| app_name | app | str | The name of the docker container |
| app_hostname | app | str | The hostname of the docker container |
| app_network_name | "{{ docker_network_name }}" | str | The name of the network the container belongs to |
| app_imagename | hello-world | str | Repository path used to create the container |
| app_version | latest | str | Repository tag used to create the container |
| app_volumes | [] | List[str] | The volumes of the container. Time zone volumes are automatically added to this list. |
| app_ports | [] | List[str] | List of ports to publish from the container to the host. |
| app_env | [] | dict | The environment variables of the container. Time zone environment variable is automatically added to this dict. |
| app_state | started | enum[absent, present, started, stopped] | The state of the container. |
| app_restart | yes | boolean | Use with started state to force a matching container to be stopped and restarted. |
| app_pull | yes | boolean | If yes, always pull the latest version of an image. Otherwise, will only pull an image when missing. |
| app_recreate | yes | boolean | Force the recreation of an existing container. |
| app_networks | - name: "{{ app_network_name }}" | dict | (optional) List of networks the container belongs to. Defaults to the single network {{ app_network_name }}. |
| app_network_ipam | {{ omit }} | dict | (optional) IPAM config blocks list. |
| app_labels | {} | Dict[str] | (optional) Dict of labels to be assigned to the new docker container. |
| app_command | {{ omit }} | str | The command that should be executed in the docker container. |

## Dependencies
None

## Minimal example
```yaml
- name: "({{ task_filename }}) Create an app container"
  include_role:
      name: docker.container.create
  vars:
      app_user: app
      app_name: app
      app_hostname: app
      app_network_name: app
      app_imagename: hello-world
      app_version: latest
      app_volumes: []
      app_ports: 
        - "8080:80"
      app_env: 
        USER: app
```

## Full example
```yaml
- name: "({{ task_filename }}) Create an app container"
  include_role:
      name: docker.container.create
  vars:
      app_user: app
      app_name: app
      app_hostname: app
      app_network_name: app
      app_imagename: hello-world
      app_version: latest
      app_volumes: []
      app_ports: 
        - "8080:80"
      app_env: 
        USER: app
      app_state: started
      app_restart: yes
      app_pull: yes
      app_recreate: yes
      app_networks:
        - name: "{{ app_network_name }}"
      app_network_ipam:
        - subnet: "192.168.61.1/24"
      app_labels: {}
      app_command: /bin/bash
```

## License
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Contributors
- [knelldev](https://github.com/knelldev)
- [CSteinmetz15](https://github.com/CSteinmetz15)