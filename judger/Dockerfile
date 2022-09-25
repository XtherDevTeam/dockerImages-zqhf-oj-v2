FROM    ubuntu:20.04
LABEL   xiaokang00010="zhouyongkang4321@gmail.com"
RUN     echo 'root:zqhf-oj-v2' | chpasswd 
RUN     echo -e "LANG=\"en_US.UTF-8\"" > /etc/default/local
ENV     DEBIAN_FRONTEND=noninteractive
RUN     sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN     apt update
RUN     apt install git cmake make g++ gcc python3 python3-pip ssh libseccomp-dev -y
RUN     mkdir -p /var
RUN     git clone https://github.com/XtherDevTeam/zqhf-oj-v2 /var/zqhf-oj-v2
RUN     git clone https://github.com/QingdaoU/Judger.git /var/Judger
RUN     cd /var/Judger ; mkdir build && cd build && cmake .. && make && make install
RUN     cd /var/Judger/bindings/Python/ ; python3 setup.py install
RUN     pip3 install psutil py-cpuinfo flask flask_cors
CMD     [ "/bin/bash", "-c", "cd /var/zqhf-oj-v2/judge ; ./judgeServer.py" ]
EXPOSE  22
EXPOSE  5917