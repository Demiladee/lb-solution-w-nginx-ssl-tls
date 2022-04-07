## configuring nginx as a load balancer

created an ec2 instance for nginx, opened tcp port 80 and tcp port 443 with inbound access from anywhere

![](images/lbinbound1.png)

updating ubuntu

`$ sudo apt update -y`

![](images/lbupdate2.png)

updating /etc/hosts file for local dns with web servers and their ip address

![](images/lbetc3.png)

![](images/lbweb4.png)

installing nginx on ubuntu

`$ sudo apt install nginx -y`

![](images/lbinstnginx5.png)

editing nginx default configuration file

`$ sudo vi /etc/nginx/nginx.conf`

![](images/lbnginxvi6.png)

![](images/lbnginxconf7.png)

confirming nginx's status

`$ sudo systemctl restart nginx`

`$ sudo systemctl status nginx`

![](images/lbstatus8.png)

registered a domain name and assigned an elastic ip to my nginx server

updated A record, configured it on route 53 and on /etc/hosts

!![](images/routerecord10.png)

![](images/routerecord11.png)

![](images/lbdomain9.png)

`$ sudo systemctl restart nginx`

`$ sudo systemctl status nginx`

![](images/lbafterroute13.png)

testing that web servers can be accessed via web browser using http protocol

![](images/lbbrowsertest14.png)

confirming snapd service is active and running

`$ sudo systemctl status snapd`

![](images/lbsnapd15.png)

installing certbot to request an ssl/tls certificate

`$ sudo snap install --classic certbot`

`$ sudo ln -s /snap/bin/certbot /usr/bin/certbot`

`$ sudo certbot --nginx`

![](images/lbcertbot16.png)

testing web server via https protocol

![](images/lbhttpstest17.png)

![](images/lbhttpscert18.png)

setting up periodical renewal of ssl/tls certificate

`$ sudo certbot renew --dry-run`

![](images/lbcertrenwal19.png)

`$ crontab -e`

![](images/lbvimcron20.png)

added this line to vim

`* */12 * * *   root /usr/bin/certbot renew > /dev/null 2>&1`

![](images/lbcronvim21.png)