#!/bin/bash 
# Run server with ./nc-server.sh 
# Connect client with "nc localhost 54321" 

rm -f ./fifo 
mkfifo ./fifo 

function handle_connection() { 
    echo "Connexion reçue le : $(date)" 
    echo "Bienvenue sur le serveur !" }
  while true; do 
    nc -l localhost 54321 < ./fifo | handle_connection > ./fifo 
Done 
