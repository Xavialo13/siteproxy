SiteProxy is a powerful online proxy tool that utilizes the latest technology to enhance proxy stability and compatibility. We are committed to providing simple, efficient, and secure proxy services, offering users the best internet access experience.

**Ultra-fast Performance:** Utilizing Hono instead of traditional Express servers, performance is improved by 4x, resulting in a smoother user experience.

**Cloud Deployment:** Perfectly supports Cloudflare Worker deployment, fast and efficient.

**AI Intelligent Chat:** Integrates DuckDuckGo AI Chat, providing free GPT-3.5 and Claude 3, making your proxy service smarter.

**Advanced Security Protection:** Supports password-controlled proxy access, allowing only authorized users to access, significantly improving security.

**Zero Configuration:** Users do not need to perform any client configuration; simply access the proxy URL to browse the global internet.

**Convenient Login:** Fully supports GitHub and Telegram Web login, simple and quick operation.

**Strong Encryption:** Employs RSA + AES dual encryption technology to protect user login passwords and prevent man-in-the-middle attacks.

Privacy Protection: Access the global internet through a proxy URL while hiding the user's real IP address, protecting privacy.

Seamless Experience: No software installation or browser configuration required; ready to use immediately, providing an extremely convenient user experience.

See Principles

Caution

This project is strictly prohibited from being used for any illegal purposes; otherwise, you will be solely responsible for the consequences.

Warning

Due to support login from multiple websites, to reduce phishing risks, Siteproxy has obfuscated its code in version 2.0 and prohibits modification of the default homepage URL.

Notes

VPS or Docker deployment is recommended. Cloudflare deployment may cause some websites to be inaccessible because CF IPs have been restricted by some websites.

DuckDuckGo is recommended for searching, as Google Search and YouTube have implemented anti-ad and anti-bot mechanisms, which may restrict access.

Deploying to Cloudflare Pages

Ensure Domain Management:
Ensure your domain is already managed under Cloudflare.

Clone Repository, Install Dependencies:
Ensure Node.js v22 or later is installed, and ensure Git is installed.

Execute the following commands:

`git clone https://github.com/netptop/siteproxy.git`

`cd siteproxy`

`npm install`

Log in to Cloudflare and create a page. If you've already created one, skip this step:

Go to the Workers & Pages section and select "Create a Page using direct upload." Upload the cloned `siteproxy/build/cf_page` directory for deployment.

Configure a custom domain. If you've already configured one, skip this step:

On the Workers & Pages page, open the deployed page.

Click "Custom Domain" at the top, then select "Add Custom Domain," set it to your proxy domain, and activate the domain.

Edit the configuration file: Open the `siteproxy/wrangler.jsonc` file using a text editor, modify the following fields, and save:

"name": "xxx", // Replace with your Cloudflare page name

"proxy_url": "https://your-proxy-domain.com", // Replace with your proxy server domain name, which must be https

"token_prefix": "/default/" // Replace with your desired access password. The leading and trailing forward slashes must be retained. If the password is empty, it means access is possible without a password.

Redeploy the page: Go to the cloned `siteproxy` directory and execute: `npm run wrangler-login`. If it's a non-GUI VPS environment, please refer to the non-GUI environment wrangler login instructions.

Execute: `npm run deploy-cf-page`

Access the proxy service: Now you can access the proxy service via `https://your-proxy-domain.com/your-password/` (make sure the trailing forward slash is present). Remember to replace the domain name and password with your own.

Deploying to Cloudflare Workers

Ensure Domain Management:
Ensure your domain is already managed under Cloudflare.

Clone the repository and install dependencies:
Ensure Node.js v22 or later is installed, and ensure Git is installed.

Execute the command: `git clone https://github.com/netptop/siteproxy.git`
Execute the command: `cd siteproxy`
Execute the command: `npm install`

Create a Worker (skip this step if already created):
Log in to Cloudflare, go to the Workers & Pages section, and create a 'hello world' Worker (name it as you like).

Configure a Custom Domain (skip this step if already created):
On the Workers & Pages page, open the Worker you just saved.

Click Settings -> Custom Domain at the top, and set it to your proxy domain. Configure and activate the custom domain.

Edit the configuration file: Open the `siteproxy/wrangler.worker.jsonc` file using a text editor, modify the following fields, and save:

"name": "xxx", // Replace with your Cloudflare worker's name

"proxy_url": "https://your-proxy-domain.com", // Replace with your proxy server domain name, which must be https

"token_prefix": "/xxx/" // Replace with your desired access password. The leading and trailing forward slashes must be retained. If the password is empty, it means access is possible without a password.

Redeploy the worker: Navigate to the cloned `siteproxy` directory and execute: `npm run wrangler-login`. For non-GUI VPS environments, please refer to the non-GUI environment wrangler login documentation.

Execute: `npm run deploy-cf-worker`

Access the proxy service: Now you can access the proxy service via `https://your-proxy-domain.com/your-password/` (ensure the trailing forward slash is present). Remember to replace the domain name and password with your own.

Deploying to a VPS or cloud server

Creating an SSL website: Use certbot and nginx to create an SSL website. You can search on Google for specific usage instructions.

Configure nginx. Ensure the `/etc/nginx/conf.d/default.conf` file contains the following:

server {
server_name your-proxy.domain.name; # Replace with your actual domain name

location / {
proxy_pass http://localhost:5006;

}
}
Restart nginx:

Execute the command: `sudo systemctl restart nginx`
Install Node.js v22 or later:

Execute the following commands:

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

source ~/.bashrc

nvm install v22
Clone the repository:

Execute the command: `git clone https://github.com/netptop/siteproxy.git`
Enter the project directory:

Execute the command: `cd siteproxy`
Test run:

Execute the command: `node bundle.cjs`
If there are no errors, press Ctrl+C to exit the program.

Configuration file modification: Open and modify the `config.json` file as follows:

{
"proxy_url": "https://your-proxy.domain.name", // Replace with HTTPS plus your proxy server domain name, ensuring https is used

"token_prefix": "/user-SetYourPasswordHere/", // Set the website password to prevent unauthorized access. The leading and trailing forward slashes must be retained. Empty indicates no password is set

"local_listen_port": 5006, // Do not modify to ensure consistency with nginx configuration

"description": "Note: token_prefix is ​​equivalent to the website password; please set it carefully. proxy_url and token_prefix together form the access URL."

} Install Forever:
Execute the command: `npm install -g forever`
Start the application:
Execute the command: `forever stopall && forever start bundle.cjs`
Access the proxy service: Now you can access the proxy service via https://your-proxy-domain.com/user-your-password/ Please replace the domain name and password with your own.

Use Cloudflare for acceleration (optional):
Refer to Cloudflare's official documentation for setup.

Now, your proxy service is successfully deployed and accessible via a browser.

Docker Deployment
Configure SSL Certificate and Nginx:
Configure the SSL certificate and Nginx for the domain name, pointing them to local port 5006.

Cloning the repository:

Execute the command: `git clone https://github.com/netptop/siteproxy.git`

Editing the configuration file:

Open and modify the `config.json` file as follows:

{
"proxy_url": "https://your-proxy-domain.com", // Replace with your obtained proxy server domain

"token_prefix": "/user-SetYourPasswordHere/", // Set the website password to prevent unauthorized access; keep the leading and trailing forward slashes

"description": "Note: `token_prefix` is equivalent to the website password; please set it carefully. `proxy_url` and `token_prefix` together form the access URL."

} Save the file.

Starting the Docker container:

Enter the `docker-node` subdirectory.

Execute the command: `sudo docker compose up`

Accessing the proxy service:

Now you can access the proxy service via `https://your-proxy-domain.com/user-your-password/`. Please replace the domain name and password with your own domain name and password.

Thanks to Telgram user SenZyo for designing the default homepage for netptop.com!

Document written by LAGSNES

Contact Information
Telegram Group: https://siteproxy.t.me E-mail: netptop@gmail.com
