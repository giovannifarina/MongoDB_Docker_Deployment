# MongoDB Docker Deployment

Ambiente Docker Compose per MongoDB e Jupyter Notebook/Lab per esercitazioni pratiche con Python e PyMongo.

## Servizi Disponibili

- **MongoDB (`mongo:latest`)**:
  - Container: `mongodb`
  - Porta esposta: `27017`
  - Credenziali: `root` / `example`
  - Volume persistente: `mongodb_data` (montato su `/data/db`)

- **Jupyter Notebook / Lab**:
  - Servizio: `jupyter`
  - Porta Web: `8888` (accessibile su [http://localhost:8888](http://localhost:8888))
  - Autenticazione: Token e password disabilitati per facilitare lo sviluppo locale
  - Volume `./datasets` montato su `/app/datasets`
  - Volume `./notebooks` montato su `/app/notebooks`
  - Librerie preinstallate: `pymongo`, `pandas`

## Struttura del Progetto

```text
MongoDB_Docker_Deployment/
├── datasets/
│   └── netflix_titles.csv
├── notebooks/
│   ├── notebook.ipynb
│   └── netflix_mongodb_tutorial.ipynb
├── Dockerfile.jupyter
├── docker-compose.yml
└── README.md
```

## Gestione del laboratorio

### 1. Avvio dei container
Costruisce l'immagine Jupyter (se necessario) e avvia i container in background:
```bash
docker compose up -d
```
Una volta avviato, Jupyter Lab sarà raggiungibile su [http://localhost:8888](http://localhost:8888).

### 2. Arresto temporaneo (mantenendo i dati)
Ferma i container senza cancellarli. Alla successiva esecuzione di `docker compose start` o `docker compose up -d`, i database MongoDB e i file creati saranno conservati:
```bash
docker compose stop
```

### 3. Rimozione dei container
Rimuove i container e la rete Docker. I dati del database MongoDB rimangono salvati nel volume Docker `mongodb_data`:
```bash
docker compose down
```

Se si desidera reimpostare completamente il database MongoDB da zero:
```bash
docker compose down -v
```

## Notebook Disponibili

All'interno della cartella `notebooks/` sono disponibili:
- [`notebook.ipynb`](notebooks/notebook.ipynb): Connessione di base a MongoDB, inserimento e lettura di un documento di prova.
- [`netflix_mongodb_tutorial.ipynb`](notebooks/netflix_mongodb_tutorial.ipynb): Tutorial completo su MongoDB che carica il dataset `netflix_titles.csv` ed esegue query, aggregazioni, update, delete e indicizzazione.
