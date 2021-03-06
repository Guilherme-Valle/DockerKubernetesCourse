# Exemplo básico de um projeto Node

1. Nesta seção iremos, pela primeira vez, entender melhor 
como escrever num arquivo `Dockerfile`

2. O primeiro comando é o comando `FROM`, que designa a imagem base que utilizaremos nos comandos subsequentes

3. Lembre-se: uma imagem Docker precisa possuir todos os seus arquivos de código dentro dela...

4. ... por isso, utilizamos o comando `COPY`, em que o primeiro argumento é o caminho dos arquivos na máquina local, e o segundo é o caminho dentro do container sendo executado.

5. Utilizamos o comando `WORKDIR` para definir que os comandos executados na imagem serão dentro do diretório /app, que utilizamos também no comando `COPY`. Nota: Poderíamos utilizar `COPY . .` por termos definido o `WORKDIR` [iria tudo ser executado dentro de /app mesmo sem especificar no comando `COPY`], mas para ter mais clareza
utilizamos o caminho absoluto no comando `COPY`.

6. O comando `RUN` executa comandos no momento da instalação da imagem. No nosso caso, executaremos o `npm install` para
instalar as dependências do nosso projeto NodeJS.

7. Utilizamos o comando `EXPOSE 80` para permitir acesso à porta 80
do container ao "mundo exterior" ao container, i.e, para nossa máquina poder acessar a porta 80 servida pelo app NodeJS sendo executado pelo Docker.

8. Por fim utilizamos o comando `CMD` para definir os comandos que serão executados *QUANDO O CONTAINER FOR INICIADO*. Importante sublinhar que o comando `RUN` executa comandos na instalação da imagem, e a imagem contém o ambiente da aplicação, não a executa em si. O comando `CMD` define o que será executado quando um container BASEADO na imagem for executado. No nosso caso, rodamos o comando node server.js para iniciar o nosso servidor NodeJS, que será executado na porta 80, que iremos expôr utilizando o `EXPOSE` supramencionado. 

9. Primeiro, para executar o container, devemos criar a imagem, o que será realizado com base no nosso `Dockerfile`, utilizando `docker build .`

10. Para executar o container, utilizamos `docker run -p 3000:80 $idDaImagem`. Uma questão poderia surgir: por que, se usamos o comando `EXPOSE 80` no `Dockerfile`, ainda precisamos usar a flag `-p`? Porque, em verdade, o comando `EXPOSE` é opcional e *não faz realmente nada*, é apenas uma boa prática, para sabermos a porta que será utilizada pelo container. Precisamos utilizar a flag para especificar e expôr a porta do container. No caso, antes do `:` utilizamos a porta que utilizaremos externamente, na nossa máquina, em nosso caso, a porta 3000, e após o sinal utilizamos a porta do docker, no caso, a porta 80.

11. Para otimizar a imagem, utilizamos o comando `COPY package.json /app` e o `RUN npm install` antes do `COPY /app`, para que, ao buildar a imagem novamente após alterar o código, o Docker utilize o cache proveniente do npm install anteriormente executado. Antes, quando utilizávamos simplesmente o `COPY /app` antes do npm install, o Docker verificava que um arquivo havia sido modificado dentro do diretório, e por isso reexecutava o npm install novamente, devido ao modo de funcionamento dos Docker Layers (uma vez que uma layer anterior continha modificação de código, o Docker não utilizava o cache em comandos posteriores, i.e no npm instal, que é o que consome mais tempo). 


# "Every instruction in an image creates a cacheable layer - layers help with image re-building and sharing."

## Attached and detached containers

 - Um container, quando executado utilizando o comando `docker run $idDaImagem`, é executado, por padrão, no modo "attached", i.e, todas as mensagens, logs etc serão exibidas no terminal em que foi executado o comando; este terminal fica "preso" ao container. Se, porém, queremos executar no modo "detached", ou seja, rodar no background o container, podemos utilizar tanto o comando `docker run -d $idDaImagem` quando o `docker start $idDoContainer`, ou, caso tenhamos um container já em modo detached, podemos utilizar o comando `docker attach $container` para vincular ele ao nosso terminal, ou mesmo utilizar o comando `docker logs $container` para ver as mensagens já exibidas nele. 

 Sempre é possível utilizar o comando `docker $command --help` para saber mais detalhes e opções dos comandos!