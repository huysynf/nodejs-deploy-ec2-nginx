# nodejs-deploy-ec2-nginx
# Install NodeJS and NPM using nvm
```bash 
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
. ~/.nvm/nvm.sh
```

# Install Git and clone repository from GitHub
```bash 
# ubutu
sudo apt update -y
sudo apt install git -y
# amazon linux
sudo yum update -y
sudo yum install git -y

# install yarn

npm install -g yarn
```
# clone code
```bash
# check repository
ll /var/www/html

# if not exits create
mkdir /var
mkdir /var/www
mkdir /var/www/html

# cd to html folder
cd /var/www/html
# clone code

git clone <repository url>

```

# Install dependencies
```bash 
# in the repo folder
npm install
# or use yarn
yarn install

```
# Step 2 — Installing PM2
```bash
npm install pm2@latest -g
pm2 start <url to file server.js>
pm2 startup systemd
sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u <user_name> --hp /home/<user_name>
pm2 save
sudo systemctl start pm2-<user_name>
systemctl status pm2-<user_name>

# stop
pm2 stop app_name_or_id
# restart
pm2 restart app_name_or_id
# list
pm2 list

```
# Setting Up Nginx as a Reverse Proxy Server
```bash 
vi /etc/nginx/sites-available/example.com
 ```
 
 ```
 server {
...
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
...
}
 
 ```

# check config nginx
```bash
sudo nginx -t
```
# restart nginx
```
sudo systemctl restart nginx
```


















