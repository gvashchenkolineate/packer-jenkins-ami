# Jenkins server AMI builder

This repo is a template to build an AWS Ubuntu AMI using [Packer](https://www.packer.io/), with [Ansible](https://www.ansible.com/) used to provision Jenkins.

## Requirements

* Ansible and Packer both need to be installed on your local machine.
* An AWS account with an Access Key for your user. Instructions [here](https://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html).
* A way to authenticate with AWS when running the Packer script, see [here](https://www.packer.io/docs/builders/amazon.html#authentication). I prefer to use the [shared credentials file](https://www.packer.io/docs/builders/amazon.html#shared-credentials-file) method.

## Usage

To create the AMI:

1. Install the required Ansible-Galaxy roles: 

    `ansible-galaxy install -r requirements.yml`

2. Create `vars.json` (use `vars.json.example` as template) to customize the build

3. Run the Packer script:

    `packer build -var-file=vars.json jenkins.json`

4. Issue investigation can be performed using local Ansible playbook run in case of any problem

    ```
   ansbile-playbook jenkins.yml -vvvv \ 
        -i hosts.yml \
        -e "jenkins_admin_username=..." \
        -e "jenkins_admin_password=..."
   ```

   _Don't forget to create EC2 instace and create `hosts.yml` with its IP address_

## Credits

Big thanks to [Jeff Geerling](https://github.com/geerlingguy) for providing lots of awesome Ansible scripts. I used his [Jenkins](https://github.com/geerlingguy/ansible-role-jenkins) role for this project.