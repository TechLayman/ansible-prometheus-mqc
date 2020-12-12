# prometheus_mqc
Pormetheus, Grafana, Alertmanager, MQ exporter ( Client mode connection to remote queue managers) deployment

# get ansible artifacts from github
mkdir -p ~/WorkSpace/ansible$
git clone https://github.com/TechLayman/ansible-prometheus-mqc

cd ~/WorkSpace/ansible/ansible-prometheus-mqc/

// run the playbook ( Example )

~/WorkSpace/ansible/ansible-prometheus-mqc/playbooks$ ansible-playbook promCompleteInstall.yml -e user_action=install

// Playbook sample

promCompleteInstall.yml 

---
- hosts: promservers
  user: root 
  become: yes

// Variable to get user action ( install | uninstall| stop | start )  

  vars:
    user_action:

  roles:

// installating ansible runtime - install location is /opt/insight/prometheus

    - role: ansible-prometheus 
      prometheus_activity: "{{ user_action }}"
      prometheus_version: 2.23.0 
      prometheus_listen_port: 9061 
  
// calling role to install grafana - install location /opt/insight/grafana

    - role: ansible-grafana 
      grafana_activity: "{{ user_action }}"
      grafana_version: 7.3.5
      grafana_port: 9062

// calling role to install alertmanager - location /opt/insight/alertmanager

    - role: ansible-alertmanager 
      alertmanager_activity: "{{ user_action }}"
      alertmanager_version: 0.21.0
      alertmanager_listen_port: 9063
      
// calling role to install node exporter on prometheus server - install location /opt/insight/nodexp

    - role: ansible-nodexp 
      nodexp_activity: "{{ user_action }}"
      nodexp_version: 1.0.1
      nodexp_listen_port: 8180
      
// calling role to copy mq_exporter and sample script to run the exporter which connects qmgr remotly
// location - /var/mqm/mqexporters
    
    - role: ansible-mqxp  
      mqxp_activity: "{{ user_action }}"
      mqclient_tar_location: /shares/repo/mqclient_redhat/9.2.1.0-IBM-MQC-LinuxX64.tar.gz

