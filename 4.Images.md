Entendendo imagens e DockerHub

- DockerHub é o container registry do docker. É onde ficam armazenadas as imagens do docker que foram chamadas até agora, como por exemplo o ubuntu e o nginx.

1. docker images
   - Vai listar as imagens que estão no meu computador;
   - docker pull php -> Irá baixar uma imagem do php que está no dockerHub;
   - docker pull php:rc-alpine -> Irá baixar uma imagem do php com a versão rc-alpine(tag);
   - docker rmi php:rc-alpine -> Irá remover essa imagem;
2. Criar imagens através do Dockerfile que está na pasta html desse diretório.
   - FROM nginx:latest -> Criando uma imagem a partir de outra que já existe na minha máquina;
   - RUN apt-get update -> Atualizar o repo da imagem;
   - RUN apt-get install vim -y -> o -y significa que será o yes pra ele confirmar instalacao do vim;
   - docker build -t felipeken/nginx-com-vim:latest . -> Irá rodar o Dockerfile na pasta atual (.) criando uma imagem com a tag a partir do parâmetro -t com nome nginx-com vim na última versão que ficará armazenada dentro do usuário do felipeken no dockerHub;
   - docker images vai listar essa imagem criada;
   - docker run -it felipeken/nginx-com-vim:latest bash irá rodar a imagem criada.
3. Avancando com Dockerfile
   - FROM nginx:latest;
   - WORKDIR /app -> Irá criar a pasta /app no container e vai deixar você dentro dessa pasta;
   - RUN apt-get update && apt-get install vim -y;
   - COPY html/ /usr/share/nginx/html -> Irá substituir o html do container com o do meu computador;
   - A cada linha do Dockerfile que é executada é gerado um chunky de arquivos. Ou seja, se rodar o mesmo comando novamente o comando já estará em cache e a execucao será bem mais rápida do que a primeira vez;
4. ENTRYPOINT vs CMD
   - FROM ubuntu:latest
   - CMD ["echo", "Hello World"] -> Vai executar o comando echo com a mensagem hello world assim que rodarmos a imagem do docker;
   - docker rm $(docker ps -a -q) -f -> Remove todos os containers que estão ativos/inativos;
   - o CMD pode ser substituído por um comando na hora de rodar o docker.
     Exemmplo : docker run --rm felipeken/hello echo "oi" -> O CMD será substituído pelo o que vem no final;
     Exemmplo2 : docker run --rm felipeken/hello bash -> O CMD será substituído e o comando que irá executar será o bash;
   - FROM ubuntu:latest;
   - ENTRYPOINT ["echo", "Hello"];
   - CMD ["World"];
   - O ENTRYPOINT é fixo e o CMD são parâmetros que vão para o entrypoint.
     Exemplo: docker run --rm felipeken/hello -> O CMD irá executar Hello World;
     Exemplo2: docker run --rm felipeken/hello echo "Oi"-> O CMD irá executar Hello Oi;
5. Como entender uma imagem ?
   - Através do Dockerfile dela;
   - Através do ENTRYPOINT;
   - Os arquivos de configuracao do ENTRYPOINT normalmente sao um arquivo.sh e no final tem um comando chamado exec"$@" que significa que pode ser executados comandos como parâmetros logo após sua chamada.
     Exemplo: ./docker-entrypoint.sh echo "hello"
   - docker login;
   - docker push IMAGE_NAME;
   - A imagem deve ficar durante 90 dias no dockerhub. É necessário fazer uns docker pull de vez em quando para manter a imagem ativa no registry.
