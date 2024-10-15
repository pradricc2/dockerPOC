# Gestione Spese POC
POC per gestione applicazioni containerizzate costituito da:
- backend in Jakarta EE
- fronent in Angular
- DB postgres

# Lista comandi utilizzati per generare la POC
- docker build -t angular-app . --> da cartella principale applicazione
- docker build -t wildfly-app . --> da cartella principale applicazione
- docker network create my-app-network
- docker run --name angular-app --network my-app-network -d -p 8081:80 angular-app
- docker run --name wildfly-app --network my-app-network -d -p 8080:8080 wildfly-app
- pg_dump -U postgres -h localhost gestione_spese > gestione_spese.sql --> dump db creato in postgres
- da cartella in cui si sono create le cartelle data e backup lanciare:
  - docker run -d
  --name postgres_container 
  --network my-app-network 
  -e POSTGRES_USER=postgres 
  -e POSTGRES_PASSWORD=postgres 
  -e POSTGRES_DB=gestione_spese 
  -v %cd%/data:/var/lib/postgresql/data 
  -v %cd%/backup:/docker-entrypoint-initdb.d 
  -p 5432:5432 
  postgres:16.2

