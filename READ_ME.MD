How to get SSL certificate using certbot:

1. Make modification to the domain.conf file based on the comment and then start the nginx container:
    
        docker compose up -d nginx

2. Start certbot using this command to start the process to get ssl certificate, replace [domain-name] with your domain:
        
        docker compose run --rm certbot certonly --webroot --webroot-path /var/www/certbot/ -d [domain-name]
    
    Check the folder ./certbot/conf to see whether the certification has been provided or not

3. Uncomment the second code block in the nginx/conf/domain.conf file and re run the nginx container
        
        docker compose up -d nginx

4. Create auto renewal job for the ssl certificate
    Run this:   
        
        crontab -e

    Add this to the file, this job will run on 1st of each 2 months:
        
        0 0 1 */2 * /usr/bin/docker compose -f [path-to-the-yml-file] run --rm certbot renew
    