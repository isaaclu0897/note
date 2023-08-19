#inProgress , #how-to, #pulp, #repository

# How to use PuLP

sudo yum update
sudo yum install epel-release
sudo yum install pulp-server pulp-rpm-plugins # pulp-rpm-plugins先不要裝
sudo pulp-manage-db createuser
sudo pulp-manage-db populate

yum install http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

wget http://repos.fedorapeople.org/repos/pulp/pulp/rhel-pulp.repo