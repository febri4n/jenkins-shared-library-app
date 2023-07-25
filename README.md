# Repository belajar jenkins

Credit code program `belajar-spring-dasar` oleh Programmer Zaman Now

### Vagrantfile untuk create VM Jenkins
```ruby
Vagrant.configure("2") do |master|
  master.vm.box = "ubuntu/jammy64"

  master.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "4098"
    vb.cpus = 4
    vb.linked_clone = true
  end

  master.vm.define "jenkins-vm" do |jenkins|
    jenkins.vm.network :private_network, ip: "192.168.1.12"
  end

end

Vagrant.configure("2") do |slave|
  slave.vm.box = "ubuntu/jammy64"

  slave.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
    vb.cpus = 2
    vb.linked_clone = true
  end

  slave.vm.define "jenkins-vm-agent" do |agent|
    agent.vm.network :private_network, ip: "192.168.1.13"
  end

end
```

### Connect ke VM Jenkins dengan Port Forwarding ke Port 1212 
```bash
ssh -D 1212 vagrant@192.168.1.12 -p 22 -i /home/febrian/Vagrant/belajar-jenkins/.vagrant/machines/jenkins-vm/virtualbox/private_key 
```
### Agar VM bisa diakses menggunakan domain
```java
127.0.0.1	localhost
192.168.1.12	jenkins.vm

# The following lines are desirable for IPv6 capable hosts
::1	ip6-localhost	ip6-loopback
fe00::0	ip6-localnet
ff00::0	ip6-mcastprefix
ff02::1	ip6-allnodes
ff02::2	ip6-allrouters
ff02::3	ip6-allhosts
127.0.1.1	ubuntu-jammy	ubuntu-jammy
```
### Setting SSL Certificate agar Jenkins bisa diakses dengan HTTPS
```bash
openssl req -newkey rsa:2048 -nodes -keyout jenkins-vm-key.pem -x509 -days 365 -out jenkins-vm-cert.pem
openssl pkcs12 -inkey jenkins-vm-key.pem -in jenkins-vm-cert.pem -export -out jenkins-vm-cert.p12
keytool -importkeystore -srckeystore jenkins-vm-cert.p12 -srcstoretype pkcs12 -destkeystore jenkins-vm.jks -deststoretype JKS
```
### Running Jenkins dengan HTTPS 
```bash
java -jar jenkins.war --httpsPort=443 --httpPort=-1 --httpsKeyStore=jenkins-vm.jks --httpsKeyStorePassword="rahasia" &
```
### Membuat file system Jenkins running dengan HTTPS
```ruby
[Unit]
Description=Jenkins Service
After=network.target

[Service]
ExecStart=/usr/bin/java -jar /home/vagrant/jenkins.war --httpsPort=443 --httpPort=-1 --httpsKeyStore=/home/vagrant/jenkins-vm.jks --httpsKeyStorePassword="pseud0nyms"
Type=simple
Restart=always

[Install]
WantedBy=multi-user.target
```
![image](https://github.com/febri4n/jenkins-playground/assets/18482250/b8619a12-39ad-4557-85cf-4227e81d9898)

```bash
sudo systemctl enable jenkins.service
sudo systemctl start jenkins.service
sudo systemctl status jenkins.service
sudo systemctl stop jenkins.service

```
![image](https://github.com/febri4n/jenkins-playground/assets/18482250/0c8ac246-2a1a-4852-b218-da1c50477db1)

![image](https://github.com/febri4n/jenkins-playground/assets/18482250/0f98931a-12bb-40cb-b05a-82518f2f4bb6)

### Menghubungkan Jenkins agar running di 2 node (Master & Slave)

![image](https://github.com/febri4n/jenkins-playground/assets/18482250/3dec2bdf-9a9a-4409-8208-e741f058540f)

### Multiple branch Jenkins
![image](https://github.com/febri4n/jenkins-playground/assets/18482250/a4f01b26-ce20-432b-8d8f-efafee8b9536)
