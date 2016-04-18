# ansible-mesos
bootstrap the mesos marathon cluster with ansible. 

Steps to setup
1. Update the server hosts in prod/qa/stage inventory files

2. Verify if the added hosts are reachable
    ansible -i prod -m ping all

3. Run the whole setup 
    ansible-playbook -i prod site.yml

Note - This setup will work work only on RHEL/Centos based servers.

4. To run only required role of the whole setup, use below syntax
    ansible-playbook -i prod common.yml
    ansible-playbook -i prod zookeeper.yml
    ansible-playbook -i prod mesos.yml
    ansible-playbook -i prod marathon.yml

5. To run only few steps (tags) of the role, use below syntax 
    ansible-playbook -i prod marathon.yml --tags "reconfigure" 

Things to do (Pending):

1. Use wait_for/pause module to give wait time between the Mesos installation and Marathon installation
2. Mesos Leader URI is some times blank in Marathon UI (which leads to waiting stage for all tasks) -- Analyze it
3. Include DB bootstrap also to make it complete platform bootstrap
