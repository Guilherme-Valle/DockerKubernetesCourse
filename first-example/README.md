# Primeiro exemplo do curso

1. Exemplo simples de um servidor NodeJS (na verdade emulado) que 
vai rodar na porta 3000.
2. Simplesmente criamos o `Dockerfile` e, dentro do arquivo contendo-o,
executamos o comando `docker build .` no terminal
3. Após terminar de baixar as dependências, é construída uma imagem, e o id da imagem é retornado.
4. Então, basta copiarmos o id da imagem e executarmos no terminal
`docker run -p 3000:3000 $idDaImagem`, então rodaremos um container à partir da imagem
5. Entrando em `localhost:3000` podemos ver o app rodando.
6. Para pararmos o container, basta abrirmos outro terminal, rodar
`docker ps`, copiar o name auto-gerado do container e executarmos 
`docker stop $nomeDoContainer`.