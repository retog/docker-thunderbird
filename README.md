# docker-thunderbird



## Usage example

Start a data-only-container for the data

    docker run -v /home/user --name user-data  busybox /bin/false

Run with

    docker run -p 2020:22 -d --volumes-from user-data --name thunderbird reto/thunderbird 

Copy public key
    
    docker exec -i thunderbird /bin/bash -c 'cat >> /home/user/.ssh/authorized_keys' < ~/.ssh/id_rsa.pub

Start thunderbird without xpra

   ssh -X -p 2020 user@localhost thunderbird

Or start thunderbird as xpra process 100

   ssh -p 2020 user@localhost xpra start :100 --start-child=thunderbird

And attach to it with
  
   xpra --ssh="ssh -p 2020" attach ssh:user@localhost:100
