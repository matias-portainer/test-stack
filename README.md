# Notes:

###to start the container run:

<code>
  docker-compose up -d
</code>

### to stop the service run:

<code>
  docker-compose down
</code>

This as to be runned from with in the same path as the docker-compose.yml file.

### What needs to be changed for a different project ?

Inside the docker-compose.yml you will find a line:

<code>
  container_name: 	&lt;example-name&gt;
</code>

This as to be the same name we will use later to point on candy. On the same file you will see 

An other line about the expose port which by default for http is port 80 .

<code>
        expose:
            - "80/tcp"
</code>

So in Caddyfile you will find : 

<code>

https://somename.outware.pt {

     reverse_proxy example-name:80
}

</code>

The FQDN name on the URL (https://somename.outware.pt) has to be a domain record already
 pointing to the office ip which is forwarded to this host running the docker , which later
targets the candy and then candy redirects to the correct container. The response then will come back
from the container to candy which will insert the SSL certificate and will respond back to the client.