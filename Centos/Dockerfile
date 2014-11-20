FROM centos:latest
##Install packages and set up sshd
RUN yum -y install openssh-server openssh-clients libedit sudo
##Set Up sshd
RUN ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key 
RUN ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key 
RUN sed -i "s/#UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config 
RUN sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config
##Disable Defaults requiretty in sudoers file 
RUN  sed -i "s/Defaults    requiretty.*/ #Defaults    requiretty/g" /etc/sudoers
#SET YOUR ROOT PASSWORD
RUN echo 'root:root123' | chpasswd
##ADD SCRIPTS IN DOCKER IMAGE
ADD ssh.sh /ssh.sh
RUN chmod +x /*.sh
##OPEN PORT 22 FOR ENABLING SSH 
EXPOSE 22
##START ssh services during startup
CMD ["/ssh.sh"]
##ADD epel repo to the base image 
RUN rpm -ivUh http://mirror-fpt-telecom.fpt.net/fedora/epel/6/i386/epel-release-6-8.noarch.rpm
##EDIT IN YUM REPOSITORY
RUN  sed -i "42 s/enabled=0/enabled=1/" /etc/yum.repos.d/CentOS-Base.repo
##ADD puppet package to the container 
RUN sudo rpm -ivh http://yum.puppetlabs.com/puppetlabs-release-el-6.noarch.rpm
RUN sed -i "19 s/enabled=0.*/enabled=1/" /etc/yum.repos.d/puppetlabs.repo
RUN yum -y install puppet-server puppet
###################################################################################


