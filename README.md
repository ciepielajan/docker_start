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


## uruchomienie repozytorium z plikiem Dockerfile.
0. Przejdź do katalogu w którym znajduje się Dockerfile
1. Zbuduj obraz kontenera 
```
# nazwa_obrazu - nazwa pod którą docker będzie widział aplikację. 
docker build -t nazwa_obrazu .
```
2. Uruchom zbudowany kontener
```
docker run nazwa_obrazu
```


## błędy i rozwiązania: 

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


