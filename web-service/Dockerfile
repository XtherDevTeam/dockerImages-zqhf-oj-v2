FROM    ubuntu:20.04
LABEL   xiaokang00010="zhouyongkang4321@gmail.com"
RUN     echo 'root:zqhf-oj-v2' | chpasswd 
RUN     echo -e "LANG=\"en_US.UTF-8\"" > /etc/default/local
ENV     DEBIAN_FRONTEND=noninteractive
RUN     sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN     apt update
RUN     apt install git python3 python3-pip ssh nginx nodejs gunicorn net-tools vim -y
RUN     mkdir -p /var
RUN     git clone https://github.com/XtherDevTeam/zqhf-oj-v2 /var/zqhf-oj-v2
RUN     pip3 install flask flask_cors
RUN     apt install npm -y
RUN     cd /var/zqhf-oj-v2/frontend ; npm install
RUN     cd /var/zqhf-oj-v2/scripts ; ./daemon.py install page ; ./daemon.py install nginx
RUN     service nginx stop
RUN     cd /var/zqhf-oj-v2/backend/src ; echo 'import backend\nbackend.init_db()\nbackend.connect_db()\nbackend.register_user("admin", "zqhf-oj-v2", 2)\nexit()\n' | python3
RUN     echo "Congratulations! You've finally installed the whole Online Judge system. Now you should follow the instructions in README.md to edit configs in your Docker container.\n" > /var/ok.txt
CMD     ["/bin/bash", "-c", "ifconfig ; cat /var/ok.txt ; cd /var/zqhf-oj-v2/backend/src ; service nginx start ; python3 app.py"]
EXPOSE  22
EXPOSE  5914