# Setup Guide

1. Set up docker

2. Download images from Docker Hub

```bash
docker pull xiaokang00010/image-judger
docker pull xiaokang00010/image-judger-scheduler
docker pull xiaokang00010/image-web-service
```

3. Create and start containers

```bash
docker container create --name web -p <oj port>:5914 xiaokang00010/image-web-service
docker container create --name judger-1 xiaokang00010/image-judger
docker container create --name judger-scheduler xiaokang00010/image-judger-scheduler
docker container start web
docker container start judger-1
docker container start judger-scheduler
```

4. Get IP address in logs

Now you should get IP address of each container. And memorize them, it will be used in next steps.

```bash
docker logs --tail 100 web # use ^C to exit
docker logs --tail 100 judger-1 # use ^C to exit
docker logs --tail 100 judger-scheduler # use ^C to exit
```

5. Configure Web Services

Use the following command to connect to container.

```bash
docker container -it exec web /bin/bash
```

Then, chdir to `/var/zqhf-oj-v2/backend/src/`

Edit the `config.json`, replace the `judger-server-address` with the address of container `judger-scheduler` like `<ip address>:5918`.

And, restart the `web` container.

6. Configure the Judger Scheduler

Use the following command to connect to container.

```bash
docker container -it exec judger-scheduler /bin/bash
```

Then, edit `/var/zqhf-oj-v2/judgeScheduler/config.py`, set `judger_hosts` to `["<judger-1 IP>:5917"]`, if you have not only one container for judge. You can set `judger_hosts` to `["<judger-1 IP>:5917", "<judger-2 IP>:5917", "<judger-... IP>:5917"]`

And, restart the `judger-scheduler` container.

7. Now you can open `localhost:5914` in your browser, and login with username `admin`, password `zqhf-oj-v2`.