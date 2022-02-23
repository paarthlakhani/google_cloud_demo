Google cloud walkthrough:

1.	Why Cloud?
    a.	Back in time, on premise. Everything is on premise. A server is managed by one person. But it goes more, 1000 users, so more servers. This lead to cloud.
    b.	Big companies, they can buy million computers and now they have more than needed, so they rented out to other companies. So they make passive income. This became a norm and lead to cloud.
    c.	More services are now provided in addition to just renting out servers. A suite of services on top of infrastructure that they are selling. This is what is called as Cloud.
    d.	They provide services as infrastructure, run code, store data.
Run code, deploy web application and have code run on cloud, store data (dbs), file storage. Fully managed and fully scaled. Tools for data migration. Tools for networking, tools for monitoring, tools to build your own API, help build security into your platform, ML platform like: tensorflow, Kubernetes, etc
2.	Different stack used: MEAN, MERN, LAMP
    MEAN: mongo, express, angular and node
    MERN: mongo, express, react, node
    LAMP: Linux, Apache, MySQL, PHP
    This is something depends on use case and the team itself
3.	Talk about LAMP
    a.	LAMP is something fundamental to web development
    b.	https://tedium.co/2021/09/01/lamp-stack-php-mysql-apache-history/ 
    c.	Facebook, Wikipedia, Slack
    d.	Linux, Apache, MySQL, PHP
    e.	One way to get the website up and running
4.	I can from the google console also but I have the links
5.	Talk about the google cloud free program: https://cloud.google.com/free/docs/gcp-free-tier#always-free
6.	Create a new project: 
    https://console.cloud.google.com/cloud-resource-manager?_ga=2.63268591.1566425885.1645587535-1762070450.1644399339 
    If free user, skip the organization option and create one
7.	Go to Project selector to select your project: https://console.cloud.google.com/projectselector2/home/dashboard?_ga=2.62326508.1566425885.1645587535-1762070450.1644399339 
8.	Home > Dashboard
9.	Free trial status icon on top right corner
10.	There are different products within google cloud itself: compute engine, network security, setup DNS, etc
11.	Enable Compute Engine API (Compute > Compute Engine)
    What does it mean by enabling the engine API
12.	What is Compute Engine API?
    Compute Engine within the google cloud is an infrastructure as a service (IAAS) offering. We will use it to create the VMs that serve as large compute clusters. It is also used to monitor VMs and set up firewall rules
13.	First we will create a VM instance
    a.	Create using the three lines: Compute – Compute Engine
    b.	https://console.cloud.google.com/compute/instancesAdd?_ga=2.167186174.1566425885.1645587535-1762070450.1644399339 
    c.	Create using ubuntu-2004
    d.	Region – SLC
    e.	Zone – Zone is an isolated location within the region
    f.	Go through other valid values and create the instance.
    g.	I have already created mine as: vm-1
14.	Go to Compute Engine – VM instances – Show the dets there
15.	You can delete the VM instance, by going on the portal and deleting the instance
16.	Linux part is done: Start the VM from the instances page and open command line
    gcloud config set project cs-4000-1 >> Don’t need this now
17.	I use emacs, easy to download: sudo apt install emacs
18.	Apache/PHP: 
    a.	sudo apt update / sudo apt-get update 
    b.	sudo apt install apache2 / sudo apt-get install apache2 php libapache2-mod-php
    c.	Check apache running properly? Run only one command above and then do this sudo systemctl status apache2 <Yes>
        See if second command in 14.b <Yes>
    d.	http://[IP_ADDRESS]
    e.	echo '<!doctype html><html><body><h1>Hello World!</h1></body></html>' | sudo tee /var/www/html/index.html >>> Might not need this Don’t need this
    f.	Test by going: http://[YOUR_EXTERNAL_IP_ADDRESS]
        http will only work, https not configured yet. External IP address will find from the instances page
    g.	Simplest file in PHP:
        i.	sudo sh -c 'echo "[YOUR_PHP_CODE]" > /var/www/html/phpinfo.php'
        ii.	We will replace YOUR_PHP_CODE with what we want to write
        iii.	Let’s write the php_info like so:
            sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php'
        iv.	http://[YOUR_EXTERNAL_IP_ADDRESS]/phpinfo.php
    h.	Custom file in HTML: https://www.php.net/manual/en/tutorial.firstpage.php
    i.	After the above, go to link: http://[IP_ADDRESS]/
19.	Install MySql:
    a.	sudo apt install mysql-server
    b.	Status: sudo service mysql status. Output would show sql is up and running
    c.	sudo mysql_secure_installation
        this sets up things like: root user password, removing anonymous users, removing test db, restricting root to local machine (VM that we created)
    d.	Use phpMyAdmin for db administration
        sudo apt-get install php-bz2 php-gd php-curl
        sudo apt-get install phpmyadmin
    e.	During installation, do the following:
        i.	Spacebar to select apache2 and tab key to move the cursor
        ii.	Select yes to use dbconfig-common for database setup
        iii.	Enter password and make a note of it: hello / phpmyadmin
        iv.	/etc/php/7.2/apache2/
            Go to server’s php.ini, remove ; of line: 
            ;extension=mysqli
        v.	/etc/apache2: Include phpadmin by including the following line in apache2.conf:
            Include /etc/phpmyadmin/apache.conf
        vi.	Restart Apache:
            sudo systemctl restart apache2
        vii.	Browse to phpMyAdmin
        viii.	http://[EXTERNAL_IP]/phpmyadmin
            login using phpMyAdmin username and password that you created when you installed phpMyAdmin
20.	Setting up DNS:
    a.	What we want to do here, is to create a domain name of our choice and point the IP address of this VM to this domain name
    b.	Register a domain: I used cloud domains - https://cloud.google.com/domains/docs/register-domain 
    c.	https://console.cloud.google.com/net-services/domains/registrations/list?_ga=2.71593683.1566425885.1645587535-1762070450.1644399339&project=cs-4000-lamp
        Cloud domains page – register a domain name – register domain. Prices are listed for each domain
    d.	Then enable the cloud DNS API to point the external IP address to the domain name that you have created above.
    e.	Network Services – Cloud DNS
    f.	After you create the domain, it is linked to that project. In order for me to use that domain in another project, I exported the domain name to google domains by export option
    g.	There I linked the domain name with the IP address, by creating a A resource:
        https://domains.google.com/registrar/ 
        Domain > DNS > Add record
    h.	You could also do it with Cloud DNS itself
    i.	Create zone
        i.	Public
        ii.	Zone name: paarthnn-me
        iii.	DNSSEX off setting is selected
        iv.	DNS name: domain name: paarthnn.me
        v.	Description: DNS zone for domain: paarthnn.me
    j.	Next we point IP address to this domain name as: 
        i.	Create an A resource record type and set the value to this IP address. The DNS name is: www. TTL: 5, TTL Unit: 5 minutes. Routing: Default. IP address is the external IP address of VM.
        ii.	Create a CNAME record, set the name to www, and set the value to @ or host name followed by period: paarthnn.me. >> Might not need this.
            You can have www for A resource type or www for cname
        iii.	This takes some time to reflect for the domain name to point to the new IP address
21.	To delete the VM instance, we go to Compute Engine – VM instances: delete when clicked on three dots
22.	To delete the project, go to
    https://console.cloud.google.com/iam-admin/settings?_ga=2.58999533.1566425885.1645587535-1762070450.1644399339 and shut down. This will free the resources

Resources:
https://cloud.google.com/compute/docs/quickstart-linux 
https://cloud.google.com/compute/docs/tutorials/basic-webserver-apache
https://cloud.google.com/community/tutorials/setting-up-lamp
https://www.cloudbooklet.com/how-to-install-lamp-apache-mysql-php-in-ubuntu-20-04/ 	
https://cloud.google.com/domains/docs/register-domain#console 
https://cloud.google.com/dns/docs/set-up-dns-records-domain-name 


