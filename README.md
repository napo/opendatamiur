# Gli opendata delle scuole italiane
## attraverso python: jupyter notebook e pandas

- preparare l'ambiente
  - su windows 
  ```bash 
     conda create -n env python=3.7 anaconda
  ```
  - su linux
  ```bash
     virtualenv -p /usr/bin/python3 env
   ```
- entrare nell'ambiente
  - su windows
  ```bash
    source activate env
  ```
  - su linux
  ```bash
     source env/bin/activate
  ``` 
- installare i pacchetti necessari
  ```bash
     pip install -r requirements.txt
  ```
- avviare jupyter notebook
  ```bash
     jupyter notebook
  ```
