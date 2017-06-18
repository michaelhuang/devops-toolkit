[The DevOps 2.0 Toolkit: Automating the Continuous Deployment Pipeline with Containerized Microservices](https://www.amazon.com/dp/B01BJ4V66M)

[The DevOps 2.1 Toolkit: Docker Swarm: Building, testing, deploying, and monitoring services inside Docker Swarm clusters](https://www.amazon.com/DevOps-2-1-Toolkit-deploying-monitoring-ebook/dp/B01N25BVHX/ref=pd_sim_351_1?_encoding=UTF8&psc=1&refRID=TECVAMXPARN16F7R3ZMR)

非常好的关于DevOps书籍！
-----------

代码更新
-----------
- docker/ubuntu repo改为阿里云mirror, 方便国内玩家

Vagrant
============

Set up
-----------

```bash
git clone https://github.com/michaelhuang/devops-toolkit.git
cd devops-toolkit
git checkout dev
```

```bash
vagrant plugin install vagrant-cachier
vagrant up dev
```

Login
-----------

```bash
vagrant ssh dev
ansible --version
docker --version
docker-compose --version
cd /vagrant
ll
```

Docker
============

Build Tests
-----------

```bash
sudo docker build -t vfarcic/books-ms-tests -f Dockerfile.test .

sudo docker push vfarcic/books-ms-tests
```

Test and Build
--------------

```bash
sudo docker-compose -f docker-compose-dev.yml run testsLocal

sudo docker build -t vfarcic/books-ms .

sudo docker push vfarcic/books-ms
```

Run Front-End Tests Watcher
---------------------------

```bash
sudo docker-compose -f docker-compose-dev.yml up feTests
```

Run Integration Tests
---------------------

```bash
sudo docker-compose -f docker-compose-dev.yml up integ
```
