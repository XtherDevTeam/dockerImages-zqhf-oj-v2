FROM    ubuntu:20.04
LABEL   xiaokang00010="zhouyongkang4321@gmail.com"
RUN     echo 'root:zqhf-oj-v2' | chpasswd 
RUN     echo -e "LANG=\"en_US.UTF-8\"" > /etc/default/local
ENV     DEBIAN_FRONTEND=noninteractive
RUN     sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN     apt update
RUN     apt install git python3 python3-pip ssh -y
RUN     mkdir -p /var
RUN     git clone https://github.com/XtherDevTeam/zqhf-oj-v2 /var/zqhf-oj-v2
RUN     pip3 install psutil py-cpuinfo flask flask_cors
RUN     cd /var/zqhf-oj-v2/judgeScheduler
EXPOSE  22
EXPOSE  5918