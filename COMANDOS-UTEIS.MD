docker ps -> Lista todos os containers ativos;
docker ps -a -> Lista todos os containers que já estiveram ativos;

docker rmi -f $(docker images -aq) -> Remove todas as imagens;
docker rm $(docker ps -a -q) -f -> Remove todos os containers;

docker build -t NAME_IMAGE . -> Irá buildar um arquivo dockerfile que esteja no mesmo repositório(.);
docker build -t NAME_IMAGE [FOLDER] -f [FOLDER]/Dockerfile.prod -> Irá buildar um arquivo dockerfile especificado;

docker run -t NAME_IMG [CMD] -> Sobe uma imagem criada, se essa imagem não existir ele buca no registry do docker hub;
docker exec -it NAME_CONTAINER [CMD]-> Entra dentro de uma imagem que está rodando, é comum utilizar o bash como CMD;

-t -> tag
-it -> modo interativo

docker logs NAME_CONTAINER -> Lista o log de um container;

docker network ls -> Lista as redes;
docker network inspect NAME_NETWORK -> Inspeciona os dados de uma rede;

docker-compose up -> Sobe um container através do arquivo .yaml;
docker-compose down -> Derruba um container através do arquivo .yaml;
docker-compose up -d -> Sobe um container através do arquivo .yaml em modo desatachado(libera o terminal);
docker-compose up --build -> Sobe um container através do arquivo .yaml buildando novamente as imagens que tiveram algum tipo de alteracao no dockerfile ou no .yaml;
