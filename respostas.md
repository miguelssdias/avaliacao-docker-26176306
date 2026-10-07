Nome: Miguel Santana Dias
Matrícula: 26176306
Usuário do GitHub: https://github.com/miguelssdias
Usuário do Docker Hub: miguelsantana08

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?

Usei a imagem base oficial `nginx:1.27-alpine`. O tamanho final da imagem gerada foi de aproximadamente 42.5 MB.

2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
   conferir que o `index.html` está lá dentro.

O Nginx procura os arquivos na pasta `/usr/share/nginx/html/`. Para conferir o arquivo lá dentro, usei o comando:
`docker exec teste-portal ls -l /usr/share/nginx/html/`

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.

Nome completo da imagem: miguelsantana08/viaserra-portal:1.0-26176306
Link público: https://hub.docker.com/r/miguelsantana08/viaserra-portal

4. Se você mudar o HTML, quais comandos precisa rodar para que a versão nova chegue ao Docker Hub?

docker build -t miguelsantana08/viaserra-portal:1.0-26176306 ./portal
docker push miguelsantana08/viaserra-portal:1.0-26176306

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

| # | Instrução | O que estava errado | O que você viu acontecer | Como corrigiu |
|---|---|---|---|---|
| 1 | `WORKDIR /usr/share/nginx` | Apontava para o diretório pai em vez da pasta `html`. | O Nginx exibia a página padrão "Welcome to nginx!" em vez da página de manutenção. | Mudei a instrução para `WORKDIR /usr/share/nginx/html`. |
| 2 | Ausente (`COPY site/ .`) | Faltava copiar os arquivos estáticos do site para dentro do container. | O container não continha o `index.html` da manutenção. | Adicionei a instrução `COPY site/ .`. |
| 3 | Ausente (`EXPOSE 80`) | Faltava documentar a porta interna 80 que o serviço Nginx escuta. | Ausência de documentação explícita da porta exposta no container. | Adicionei a instrução `EXPOSE 80`. |

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?

A sintaxe é `-p <porta-do-host>:<porta-do-container>`.
- `-p 7042:80` mapeia a porta 7042 do seu computador (host) para a porta 80 dentro do container.
- `-p 80:7042` mapeia a porta 80 do seu computador para a porta 7042 do container.
O número à direita de cada par de pontos (neste caso, o `80` em `-p 7006:80`) é a porta do container.

## Parte 4 · Primeiro docker-compose

7. Escreva os dois comandos `docker run` que fariam o mesmo que o seu `docker-compose.yml`.

docker run -d --name portal -p 8006:80 --restart unless-stopped miguelsantana08/viaserra-portal:1.0-26176306
docker run -d --name manutencao -p 7006:80 --restart unless-stopped manutencao:26176306

8. Qual comando derruba os dois containers de uma vez?

docker compose down

## Verificador

9. Código de conclusão impresso pelo verificador: 'VIASERRA-26176306-3B227D22'