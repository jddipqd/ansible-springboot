# Ansible Spring boot
[![Build Status](https://travis-ci.org/remyma/ansible-springboot.svg?branch=master)](https://travis-ci.org/remyma/ansible-springboot)

Deploy spring boot applications as linux services.

## Requirements

Your spring boot application should be previously packaged as a fully executable jar as explained here :

https://docs.spring.io/spring-boot/docs/current/reference/html/deployment-install.html#deployment-script-customization-conf-file

## Role Variables

| Variable     | Default       | Description    |
| ------------ | ------------- | -------------- |
| springboot_java_install | true | If you want this role to install java. Use false if java is already installed |
| springboot_src_file  |  | Mandatory or use ```springboot_src_url```. Path of the springboot jar to deploy.  |
| springboot_src_url |  | Mandatory or use ```springboot_src_file```. Url of the springboot jar to deploy. |
| springboot_application_name |  | Mandatory. Spring application name. Use to name jar to be deployed, systemd service, ... |
| springboot_propertyfile_template | | Optional. Path towards a template to manage your app properties (eg : application.properties, application.yml). You can also pass a list if you need multiple property files (eg. for different profiles) |
| springboot_configuration_template | | Optional. Path towards a template to manage your app config (see : https://docs.spring.io/spring-boot/docs/current/reference/html/deployment-install.html#deployment-script-customization-when-it-runs).  |
| springboot_service_install | true | Use false if you don't want this role to register system service for the application.
| springboot_logging_template | | Optional. Path towards a template to manage your logging configuration (eg : logback.xml).  |
| springboot_deploy_folder | /opt/{{ springboot_application_name }} | Folder where application jar is deployed |
| springboot_user | springboot | Linux user to run spring boot application |
| springboot_group | springboot | Linux group to run spring boot application |


## Example Playbook

Minimal playbook :

    - hosts: all
      vars:
        springboot_application_name: spring-boot-sample
        springboot_src: tests/spring-boot-sample.jar
      roles:
        - role: ansible-springboot
  
If you want to deploy also configuration and/or properties for you application :    
    
    - hosts: all
      vars:
        springboot_application_name: spring-boot-sample
        springboot_src: spring-boot-sample.jar
        springboot_propertyfile_template: /path/to/your/template/application.yml
        springboot_configuration_template: /path/to/your/template/spring-boot-sample.conf
      roles:
        - role: ansible-springboot

## License

BSD

