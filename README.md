# Ansible Role archive-to-s3

Library of Ansible plugins and roles for deploying various services.
See [ansible-roles](https://github.com/davidfischer-ch/ansible-roles) for additional documentation.

This repository hosts the role archive-to-s3 and may depend of other roles and plugins of the library.

See the project [archive-to-s3](https://github.com/davidfischer-ch/archive-to-s3).

## Dependencies

See [meta](meta/main.yml).

## Variables

TODO

### PlayBook

```
- hosts:
    - aws
  pre_tasks:
    - ec2_metadata_facts:
      tags: always

    - debug:
        var: ansible_ec2_instance_id
  roles:
    - archive-to-s3
    # - cloudwatch-mon-scripts
    # - cloudwatch-logs-agent
  vars:
    archive_to_s3_execute_at: 1  # 1 AM
    archive_to_s3_config:
      enabled: yes
      transfers:
        - name: Logs
          bucket: my-own-bucket-name
          delete: yes
          directory: /var/log
          patterns: '.*\.gz'
          prefix: logs/{{ inventory_hostname }}/{{ ansible_ec2_instance_id }}
```

## License

See [LICENSE.rst](LICENSE.rst).

## Authors

See [AUTHORS](AUTHORS).

2014-2022 - David Fischer
