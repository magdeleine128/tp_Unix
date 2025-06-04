#!/bin/bash 
#!/bin/bash 
# Run server with ./nc-server.sh 
# Connect client with "nc localhost 12345" 
rm -f ./fifo 
mkfifo ./fifo 

function handle_connection() { 
    echo "Connexion reçue le : $(date)" 
    echo "Bienvenue sur le serveur !" 
    
    while read line; do 
        if [ "$line" == "exit" ]; then 
            echo "Déconnexion." 
            exit 

        fi 
        result=$(bash -c "$line" 2>&1) 
        echo "$result" 
    done
} 
while true; do 
    nc -l localhost 12345 < ./fifo | handle_connection > ./fifo 
Done 
