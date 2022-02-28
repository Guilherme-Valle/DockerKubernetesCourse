# Exemplo básico de um projeto Node

1. Nesta seção iremos, pela primeira vez, entender melhor 
como escrever num arquivo `Dockerfile`

2. O primeiro comando é o comando FROM, que designa a imagem base que utilizaremos nos comandos subsequentes

3. Lembre-se: uma imagem Docker precisa possuir todos os seus arquivos de código dentro dela...

4. ... por isso, utilizamos o comando `COPY`, em que o primeiro argumento é o caminho dos arquivos na máquina local, e o segundo é o caminho dentro do container sendo executado.

5. Utilizamos o comando `WORKDIR` para definir que os comandos executados na imagem serão dentro do diretório /app, que utilizamos também no comando `COPY`. Nota: Poderíamos utilizar COPY . . por termos definido o WORKDIR [iria tudo ser executado dentro de /app mesmo sem especificar no comando COPY], mas para ter mais clareza
utilizamos o caminho absoluto no comando COPY.

6. O comando `RUN` executa comandos no momento da instalação da imagem. No nosso caso, executaremos o `npm install` para
instalar as dependências do nosso projeto NodeJS.

7. Utilizamos o comando `EXPOSE 80` para permitir acesso à porta 80
do container ao "mundo exterior" ao container, i.e, para nossa máquina poder acessar a porta 80 servida pelo app NodeJS sendo executado pelo Docker.

8. Por fim utilizamos o comando `CMD` para definir os comandos que serão executados *QUANDO O CONTAINER FOR INICIADO*. Importante sublinhar que o comando `RUN` executa comandos na instalação da imagem, e a imagem contém o ambiente da aplicação, não a executa em si. O comando CMD define o que será executado quando um container BASEADO na imagem for executado. No nosso caso, rodamos o comando node server.js para iniciar o nosso servidor NodeJS, que será executado na porta 80, que iremos expôr utilizando o `EXPOSE` supramencionado. 