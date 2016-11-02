# Setup Environment to Use Ansible
```
sudo apt-get install python-dev
sudo pip install boto virtualenvwrapper
mkvirtualenv databus
pip install ansible
pip install awscli
```

# Create Environment Using Ansible
```
workon databus
ansible-playbook -i localhost, site.yml --extra-vars "vpc_name=databus-dev env_name=dev"
```

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
