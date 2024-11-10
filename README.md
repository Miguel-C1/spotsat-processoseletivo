# spotsat-processoseletivo
## Como rodar o projeto

1. Clone o repositório de forma recursiva:
    ```sh
    git clone --recursive https://github.com/Miguel-C1/spotsat-processoseletivo.git
    ```

2. Rode o comando:
    ```sh
    docker network create --subnet=172.18.0.0/16 spotsat-processoseletivo_default
    ```

3. Verifique a rede criada:
    ```sh
    docker network ls
    ```

4. Como boa prática, na primeira vez que você rodar, entre no Docker Desktop e apague todos os contêineres, imagens e volumes anteriores que você tiver.

5. Rode o comando:
    ```sh
    docker-compose -f docker-compose-dev.yaml up -d
    ```

    - Ele irá baixar as imagens indicadas no docker-compose e irá armazená-las localmente. Vide aba "Imagens" do Docker Desktop.
    - Depois irá buildar as imagens em contêineres. Vide aba "Conteiners" no Docker Desktop.

6. Se você receber algum erro de porta, isso significa que alguma das portas que um ou mais dos contêineres quer utilizar já está sendo utilizada pelo seu computador. Ex: mysql já usa o 3606. Pare o serviço do mysql e tente novamente:
    ```sh
    docker-compose up -d
    ```

7. Se você receber algum erro de subnet, você precisa apagar sua rede e refazer:
    ```sh
    docker network create --subnet=172.18.0.0/16 spotsat-processoseletivo_default
    ```

9. Você pode clicar na porta de um dos serviços, que será aberta uma aba direto no seu navegador com o serviço funcionando.

10. Agora vamos testar a rede interna do Docker pelo navegador. Ao invés de entrar na URL: localhost, vamos usar: host.docker.internal. Ex: localhost:3001 -> host.docker.internal:3001

     - Se o serviço rodar mesmo assim, já está tudo certo com seus serviços conteinerizados.
     - Se não rodar, entre nessa pasta pelo VSCode: `C:\Windows\System32\drivers\etc`
        - Abra o arquivo `hosts`
        - Faça um BackUp dele
        - Edite as linhas:
          ```
          <ip> host.docker.internal
          <ip> gateway.docker.internal
          ```
        - Troque `<ip>` por `127.0.0.1`
        - Aperte `Control + S` para salvar. Pode ser que apareça uma mensagem para você salvar como administrador. Essa pasta requer privilégios para alterar.

11. Após a alteração, teste novamente seu endpoint no navegador. Ex: host.docker.internal:3001