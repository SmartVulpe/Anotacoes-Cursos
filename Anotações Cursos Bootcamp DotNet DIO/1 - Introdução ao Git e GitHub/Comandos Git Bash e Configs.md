# Comandos Basicos Git

- **git init** --- inicializa a pasta para virar um repositorio
- **git add .** --- pega tudo oq foi modificado e adiciona no stage para dar o commit
- **git commit -m** --- "descrição do commit aqui com aspas" - faz o commit e deixa uma mensagem.
- **git status** --- checa o status do repositorio se tem alguma alteração.
- **git config --list** --- para listar as config (apertar Q para sair)
- **git remote -v** --- mostra o link do repositorio remoto cadastrado
- **git push origin master** --- envia para a branch master do repositorio remoto q esta usando o alias origin (obs: se o rep for criado no github vai ser *origin main*).
- **git pull origin master** --- faz o download dos arquivos atualizados do repositorio remoto.
- **git clone "link do repositorio sem aspas"** --- clona o repositorio para a tua maquina.


# Comandos Bash Úteis

- **openssl sha1 nomedoarquivo** --- gera o hash sha1 do arquivo
- **cat** --- exibe o conteudo de um arquivo no console



# Configurações Úteis/Importantes

### Configurar o autor dos commits:

- **git config --global user.email "seu email com aspas"**
- **git config --global user.name "nome do usuario sem aspas"**



### Para não precisar ficar entrando no site do git para digitar senha toda vez que você der commit você vai precisar fazer o seguinte:

Primeiro gerar uma chave SSH publica e privada, que vão servir na tua autenticação.

Depois você clona seus repositorios usando o link SSH.

- #### Para gerar uma chave ssh no bash para usar no github, digite esse comando:

  - **ssh-keygen -t ed25519 -C "seu email sem aspas"**
  - o -C tem q ser maiusculo.
  - caminho padrão que fica salvo as chaves publicas e privadas é: c:/Users/NomeUsuario/.ssh/
  - da pra abrir pelo bash usando o comando **cat nomedoarquivo.pub**
  - Então você pode copiar o conteudo do arquivo ssh publico (.pub), e colocar no github na area das chaves SSH.


- ##### Depois para colocar no git do pc, vc vai na pasta .ssh pelo git bash, e digita os comandos:

  - **eval $(ssh-agent -s)**
  - **ssh-add id_ed25519**
  - Esse id é o nome do arquivo q foi gerado, e é o sem .pub, porque agora você vai usar a chave privada e não a publica.
  - Ai você vai digitar a senha q vc colocou no arquivo na hora de gerar, e pronto está configurado.

- **Para clonar um repositorio como SSH:**

  - no github tem um botão "Code" no menu que ele abra tem uma opção SSH, então você copia o link dessa opção.
  - no bash você digita o seguinte comando e coloca o link ssh que você copiou:
  - **git clone "link ssh sem aspas"**
  - Então na primeira vez vai precisar dar yes para botar a key e o github nos conhecidos do teu git.

Depois disso é só usar, e a cada commit vc só vai precisar digitar no bash a senha que você colocou na hora de criar a chave SSH.

