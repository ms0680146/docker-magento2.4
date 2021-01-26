# docker-magento2.4
Install Magento 2.4 + mariadb:10.4 + elasticsearch:7.8.1 using docker  

step1. Install Docker  
step2. Install Compose  
step3. Download Magento 2.4  
- Log in or create an account on Magento marketplace. Navigate to Access Keys and create new access keys.  
- Open terminal and create a folder to store Magento project.
```
cd ~/Desktop
mkdir magento2.4
cd magento2.4
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .
```
- Choose a domain name you would like to use to access the site and add it to your hosts file. 
```
sudo -- sh -c "echo '127.0.0.1 magento-test.com' >> /etc/hosts"
```
step4. Create a docker-compose.yml file and copy and past code form ms0680146/docker-magento2.4/docker-compose.yml  
```
cd magento2.4
touch docker-compose.yml
```
step5. Build images and up containers
```
cd magento2.4
docker-compose up -d --build
```
step6. Access your Docker web container’s command line
```
docker exec -it web bash
cd /app
```
step7. Install Magento, replace the values amdin-xxx with your own details, and replace the domain with your own domain. Finally, you can copy and past the command shown below into the Docker web container.
```
php bin/magento setup:install \
--admin-firstname='magento firstname' \
--admin-lastname='magento lastname' \
--admin-email=xxxxx \
--admin-user=xxxxx \
--admin-password='xxx' \
--base-url=https://magento-test.com \
--base-url-secure=https://magento-test.com \
--backend-frontname=admin \
--db-host=mysql \
--db-name=magento \
--db-user=root \
--db-password=root \
--use-rewrites=1 \
--language=en_US \
--currency=USD \
--timezone=America/New_York \
--use-secure-admin=1 \
--admin-use-security-key=1 \
--session-save=files \
--use-sample-data \
--elasticsearch-host=elasticsearch \
--elasticsearch-port=9200
```
step8. Visit your website at https://magento-test.com or whatever domain you chose. The first time you go to access the site, it might take a couple of minutes for the page to load. Additionally, because the web container uses a self-signed SSL certificate, the browser will likely present you with a security alert the first time you visit the URL. Just follow any prompts to add an exception so that you can proceed to the local website.


Ref: https://www.magemodule.com/all-things-magento/magento-2-tutorials/docker-magento-2-development/  
Ref: https://www.endpoint.com/blog/2020/08/27/containerizing-magento-with-docker-compose-elasticsearch-mysql-and-magento
