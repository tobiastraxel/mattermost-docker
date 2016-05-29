
Get the certificates by running the letsencrypt script in a [docker container](http://letsencrypt.readthedocs.io/en/latest/using.html#running-with-docker)

    docker run -it --rm -p 443:443 -p 80:80 --name certbot \
            -v "/etc/letsencrypt:/etc/letsencrypt" \
            -v "/var/lib/letsencrypt:/var/lib/letsencrypt" \
            quay.io/letsencrypt/letsencrypt:latest auth
            
            

Path to the certificates

    /etc/letsencrypt/live/ozarcs.net            
    
to [configure nginx](https://www.nginx.com/blog/free-certificates-lets-encrypt-and-nginx/)

  server {
    listen 443 ssl default_server;
    server_name my-domain;

    ssl_certificate /etc/letsencrypt/live/my-domain/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/my-domain/privkey.pem;

    ...
  }    
  
  
We use docker volume mounting to get a stable path in our nginx.config

exitsing mattermost config: 

    ssl_certificate /cert/cert.pem;
    ssl_certificate_key /cert/key-no-password.pem;

