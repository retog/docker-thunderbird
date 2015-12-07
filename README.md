# docker-thubnderbird



## Usage example

Run with

    docker run -p 2020:22 -d --name thubnderbird reto/thubnderbird 

Copy public key
    
    docker exec -i thubnderbird /bin/bash -c 'cat > /root/.ssh/authorized_keys' < ~/.ssh/id_rsa.pub

Start xclok vithout xpra

   ssh -X -p 2020 root@localhost xclock

Or start xclock as xpra process 100

   ssh -X -p 2020 root@localhost xpra start :100 --start-child=xclock

And attach to it with
  
   xpra --ssh="ssh -p 2020" attach ssh:root@localhost:100

Or start Xnest as display 200 on a new xpra display 111

   ssh -X -p 2020 root@localhost xpra start :111 --start-child=\"Xnest :200 -ac -geometry 800x600+24\"

Start ratpoison as display manager

   ssh -X -p 2020 root@localhost DISPLAY=:200 ratpoison & 

And thubnderbird

   ssh -X -p 2020 root@localhost DISPLAY=:200 xclock &

And attach to it with
  
   xpra --ssh="ssh -p 2020" attach ssh:root@localhost:111

You may need to adapt the keyboard layout

    ssh -X -p 2020 root@localhost DISPLAY=:200 setxkbmap -layout ch

