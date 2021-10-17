<h1>Rodando PostgreSQL com a ferramenta PgAdmin no Docker.</h1>

- Para seguir esse tutoria se faz necessário realizar o cadastro no sie do docker,
     usuário do sistema operacional Windows devem instalar o docker desktope.
    -   Site para realizar o cadastro:
          https://hub.docker.com
          
          <img src=/Users/alexoliveira/Postegre/Docker_PostgreSQL_PgAdmin/img/Site Docker.png>

    -  Site para baixar o docker desktope:
          https://www.docker.com/products/docker-desktop


<h2> Primeiro passo: </h2>

    - Definir as imagens para serem utilizadas no projeto.

        Para o PostgreSQL foi utilizado a imagem oficial que esta no repositório:
            https://hub.docker.com/_/postgres?tab=description

         Para o Gerenciador do banco foi utilizado a imagem do PgAdmini que esta no repositório:
            https://hub.docker.com/r/fenglc/pgadmin4

<h2> Segundo passo: </h2>

    - Criando a NetWork

    - Criar a rede para interligar os dois serviços, devido ao docker trabalhar com cada container 
        de forma individual, se faz necessário a criração de uma rede para a comunicação interna 
        entre os dois servições.

    - Comando:
       
       docker network create NetPostgre 
       
    
<h2> Terceiro passo: </h2>

    - Criar o Volume:

    - Este processo se faz necessário para que mesmo matando o container os dados da base 
        permaneçam armazenados na sua maquina, caso não tenha necessidde de manter os dados 
        armazenados pode pular apara o próximo passo.

    - Comando:    
        docker volume create Base_Postegre


<h2> Quarto Passo: </h2>

    - Criar os containeres:

        - Criação do container do PostgreSQL
        docker container run -d --name postgre --network NetPostgre -e POSTGRES_PASSWORD=defina_uma_senha 
        -e POSTGRES_USER=defina_um_usuario -v Base_Postegre:/vol/postgresql/data postgres:latest

        OBS.: Por se tratar de um estudo estou utilizando a ultima versão da imagem, indicada pelo 
              versão "lateste" após o nome da imagem.
              Caso não tenhs decidico trabalhar com volume a opção: 
                -v Base_Postegre:/vol/postgresql/data deve ser retirada.

        - Criação do container do PgAdmin
        docker container run -d --network NetPostgre -p 5050:5050 fenglc/pgadmin4:latest

<h2> Rodando o serviço: </h2>

    O container do PgAdmin tem as seguintes configurações para ser execultádo:
        - Acesso o seu navegador e digite:
            http://localhost:5050 
        - Para acessar a pagina pela primeira vez devem ser digitado os seguintes dados:

            user: pgadmin4@pgadmin.org
            password: admin

            OBS.: Após acsso pode ser criado um usuário , sendo que esse usário so terá 
            os seus dados guardadso se for utilziado um volume.
