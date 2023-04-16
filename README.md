# docker_start

## przydatne komendy 

```bash
docker version
docker run hello-word
docker ps
docker images
docker container ls -a
docker rm name_container
# Sprawdzenie statusu działania dockera
sudo systemctl status docker.service 
sudo systemctl restart docker.service
```

## instalacja na ubunu 20.04

https://www.cherryservers.com/blog/how-to-install-and-start-using-docker-on-ubuntu-20-04

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```
```
sudo apt update
```
```
# install
sudo apt install docker-ce
```
```
# check status docker
# You should have 'Activate:' as 'active (running), green color
sudo systemctl status docker
```
![image](https://user-images.githubusercontent.com/4579021/232307549-dbbd94e9-2918-4e1e-852f-31935b0b42c9.png)

```
docker run hello-world
```
## Tworzenie pliku Dockerfile
```Dockerfile
FROM python:3.8-slim-buster

WORKDIR /app
ADD requirements.txt . 
RUN pip install -r requirements.txt
COPY . .
WORKDIR /app/folder_projektu  
CMD ["python", "-m" , "flask", "run", "--host=0.0.0.0"]
```
Objaśnienia:
```Dockerfile
FROM python:3.8-slim-buster

WORKDIR /app
ADD requirements.txt . 
RUN pip install -r requirements.txt
COPY . .
EXPOSE 8004
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8004" , "--reload"]
```


## PYTHON DEMO
https://docs.docker.com/language/python/build-images/

## uruchomienie repozytorium z plikiem Dockerfile.
0. Przejdź do katalogu w którym znajduje się Dockerfile
1. Zbuduj obraz kontenera 
```
# nazwa_obrazu - nazwa pod którą docker będzie widział aplikację. 
docker build -t nazwa_obrazu .
```
![image](https://user-images.githubusercontent.com/4579021/232313965-f7ce453b-0981-476d-86c1-5d6c3f70d0bd.png)
Sprawdź czy istnieje nowo powstały obraz konternera
![image](https://user-images.githubusercontent.com/4579021/232313866-6f5bfd7e-abdf-446a-99f7-99ca4804be79.png)

2. Uruchom zbudowany kontener
```
docker run -p 8000:5000 nazwa_obrazu
```
Obraz zostanie uruchomiony pod portem **8000** 

![image](https://user-images.githubusercontent.com/4579021/232314018-ee7afc83-edfc-476e-920c-e1d5691617d2.png)

Bez mapowania portów podczas uruchamiania obrazu nie będzie on działał jako lokalhost lub 0.0.0.0. Będzie dostepny pod adresem IP przydzielonym przez dockera. Poniżej test pod, którym IP udało się połączyc ze stroną po uruchomieniu obraz poleceniem 
```docker run nazwa_obrazu```


## błędy i rozwiązania: 
### case 1
```
docker run hello-world
```
![image](https://user-images.githubusercontent.com/4579021/232307907-6eb69832-b1a4-437d-b631-853649094ef6.png)
Błąd, oznacza, że brakuje Ci uprawnień do połączenia się z usługą Dockera. Rozwiązanie:
```
sudo docker run hello-world
```
lub dodaj siebie (użytkownika) do grupy docker'a przez polecenie 
```
sudo usermod -aG docker <nazwa_użytkownika>
```
i ponowne uruchomienie systemu. 

### case 2
docker lub docker-compose nie mapują dobrze portów. W każdym pliku Dockerfile dodaj przed wywołaniem serwer **EXPOSE <nr portu> **
```Dockerfile
EXPOSE 8004 
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8004" , "--reload"]
```
### case 3
Nie działają adresy IP takie jak localhost, czy 0.0.0.0 . Uruchom kontener z dodatkowymi prametrami.
  
![image](https://user-images.githubusercontent.com/4579021/232334553-0b3a466c-66d4-4521-8f87-c772387e9a3c.png)
 
```Bash
docker run -p 8000:8000 -e HOST=0.0.0.0 -e PORT=8000 nazwa_kontenera
```
  
![image](https://user-images.githubusercontent.com/4579021/232339841-2d3d9420-2484-4cc9-8aad-a2a66c2c714c.png)


