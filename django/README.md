
### Django

Agora o bicho vai pegar!

1. Crie um ambiente virtual com python3 dentro da pasta django e ative-o (todos os comandos abaixo é dentro da pasta django)
2. Com o ambiente ativado, rode: 
    ```bash
    pip install --upgrade pip
    pip install -r requirements.txt # instala pacotes, somente se já estiver com requirements.txt, se não, vai pro passo 3 e cria o requirements.txt
    ```
3. Só para conhecimento: se quizesse começar um novo projeto django 'crediario'
    ```bash
    django-admin startproject crediario .
    pip install django
    pip install dj-database-url
    pip install django-decouple
    pip install psycopg2
    pip freeze > requirements.txt # cria requirements.txt, tchanrã!
    ```
4. Crie um schema com seu nome no banco de dados (conexão no template abaixo)

5. Instale xclip. O que ele faz? Ele copia para o "Ctrl+V" a saída de um comando (poderia ser um "cat", um "echo"...)
    ```bash
    sudo apt install xclip
    ```

6. Pegar uma nova chave secreta (SECRET_KEY) (ainda não estamos utilizando o shell_plus) (Olha que estou copiando a saída do comando com o xclip, então não copie mais nada, pois perderemos o "Crtl+V")
    ```bash
    curl -s https://gist.githubusercontent.com/henriquebastos/11cf99c1bbc70bacf73a/raw/f3f6e190cdad1b30556916e9149eec6253f610c2/secret_gen.py | python | xclip -selection clipboard
    ```    

7. Crie um arquivo .env dentro da pasta crediario utilizando este template. No lugar de "SEU_NOME" coloque o schema que você criou e no "SUA_SECRET_KEY" cole o resultado do "Ctrl+C" gerado no comando acima
   
   ```conf
   DATABASE_URL=postgres://usr_aplicacao:aplicacao@172.16.2.222:6000/dbacam?currentSchema=SEU_NOME
   DEBUG=True
   SECRET_KEY=SUA_SECRET_KEY
   ```

8. Com ambiente ativado e dentro da pasta crediario, execute o comando para rodar o servidor do django (olhar os Tips.3 abaixo, hora mais!)

9. Se roudou tudo certinho, aplique as migrações que o django já tem para executar (Tips.5)

10. Agora, dentro da pasta crediario, criar a app 'clientes' (utilize o Tips.8)

#### Tips
1. Criar ambiente virtual
    ```bash
    cd django # pasta utilizada somente para organizar o projeto
    python3 -m venv .workshop # cria ambiente virtual na pasta .workshop
    source .workshop/bin/activate # ativa ambiente virtual
    deactivate # desativa ambiente virtual
    ```

2. Gerenciar dependencias de projeto
    ```bash
    cd django
    source .workshop/bin/activate # ativa ambiente virtual
    pip freeze # lista as libs utilizadas no projeto neste ambiente virtual
    pip freeze > requirements.txt # salva saída do 'pip freeze'
    ```

3. Rodar servidor na porta 8000
    ```bash
    cd django
    ./manage.py runserver 0.0.0.0:8000
    ```

4. Gerar migrações
    ```bash
    cd django
    ./manage.py makemigrations
    ```

5. Aplicar migrações
    ```bash
    cd django
    ./manage.py migrate
    ```

6. Como inspecionar TODO O banco legado?
    ```bash
    cd django
    ./manage.py inspectdb > models_full.py # joga a saída do comando no arquivo models_full.py
    ```

7. Como inspecionar somente uma tabela do banco legado?
    ```bash
    cd django
    ./manage.py inspectdb TABELA | xclip -selection clipboard # joga a saída do comando "Crtl+V"
    ````

8. Criar nova app dentro do projeto crediario
    ```bash
    cd django/crediario
    ../manage.py startapp NOME_DA_APP
    ```