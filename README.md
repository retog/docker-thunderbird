# docker-thunderbird

Thunderbird and other programs used when processing email

## Usage example

Start a data-only-container for the data

    docker run -v /home/user --name user-data  busybox /bin/false

Run with

    docker run -p 2020:22 -d --volumes-from user-data --name thunderbird reto/thunderbird 

Copy your ssh public key to the container so that you can login via ssh
    
    docker exec -i thunderbird /bin/bash -c 'cat >> /home/user/.ssh/authorized_keys' < ~/.ssh/id_rsa.pub

And attach to it with
  
   xpra --ssh="ssh -o \"StrictHostKeyChecking no\" -p 2020" attach ssh:user@localhost:100
   
Start thunderbird with  

    ssh -p 2020 user@localhost thunderbird

Backup the user data from the data-only-container:

   docker run --volumes-from user-data -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /home/user
