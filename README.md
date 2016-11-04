# Setup Environment to Use Ansible
```
sudo apt-get install python-dev
sudo pip install boto virtualenvwrapper
mkvirtualenv databus
pip install ansible
pip install awscli
```

# Create Infrastructure
```
workon databus
ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i localhost, build-infra.yml --extra-vars "vpc_name=ubp-lab4 env_name=dev"
```

# Install Docker Engine
```shell
EC2_INI_PATH=./inventory/ec2-inventory.ini ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i ./inventory/ec2-inventory.py install-docker-engine.yml
```

# Deploy Services
```shell
EC2_INI_PATH=./inventory/ec2-inventory.ini ansible-playbook -i ./inventory/ec2-inventory.py deploy-services.yml
```

# Cleanup AWS infrastructure

- Delete instances (filter by project name)
- Delete security groups (filter by project name)
- Delete VPC (filter by project name)

# Code Organization
```
.
├── build_env.yml -> an individual play
├── group_vars
│   └── all.yml -> default values global for all groups and roles
├── roles
│   └── build-vpc
│       ├── tasks
│       │   └── main.yml -> tasks for this role
│       └── vars
│           └── main.yml -> role specific variables
└── site.yml -> playbook including all individual plays
```
