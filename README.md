Scripts to configure a working linux environment.

Content:
- bootstrap: install the main tools (inc. ansible)
- tasks: various tasks to configure my environment (to be selected in playbook.yaml)

Usage:
1. ./bootstrap
2. edit playbook.yaml to un/comment the required elements
3. ./config-test
4. ./config-apply
