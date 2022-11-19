GUI - Graphic User Interface.  
CLI - Command Line Interface.

----------

O git usa git SHA1 na encriptação.

Usando o git bash dá para testar sha1  
comando:  
`openssl sha1 nomedoarquivo`    
ai ele vai da o codigo de encriptação (q pode ser usado como comparador de alteração no arquivo)  

----------

# Blobs
É um bloco basico de conteudo "Um blob (objeto binário grande) do Git é o tipo de objeto usado para armazenar o conteúdo de cada arquivo em um repositório. O hash SHA-1 do arquivo é calculado e armazenado no objeto do blob. Esses pontos de extremidade permitem que você leia e grave objetos de blob no banco de dados do Git no GitHub."  
Basicamente dentro do arquivo vai ta escrito blob o numero de caracteres e um \0 antes de começar o conteudo, exemplo:  
blob 9\0conteudo  

É preciso ter cuidado pq se vc fizer o sha1 de um arquivo txt com a palavra conteudo, ele vai da um resultado (has), mas se vc fizer essa comparação usando um arquivo q vc gerou e mandou no git ele vai dar um hash diferente pois vai ter mais essas palavras ai ""blob 9\0"conteudo".  

# Trees  

As trees armazenam blobs, elas possuem os nomes dos arquivos, os blobs não possuem os nomes, e podem apontar para arquivos e para outras trees (imagine como uma pasta que tem arquivos, e, outras pastas dentro).  
Se mudar uma virgula num blob, quando passa o sha1 da tree, vai mudar o sha1 da tree tambem, pois ela engloba os blobs juntos na verificação de hash.  


# Commits
O commit ele aponta para uma arvore, aponta para o parente (ultimo commit feito com o hash anterior), aponta para um autor, e aponta para uma mensagem tambem (para explicar alteração e tal), e a data/tempo q foi feito. o commit tambem tem um sha1.  

O git é mt confiavel pois se vc alterar um caractere numa blob, ela vai gerar um sha1 novo, que por consequencia vai alterar o sha1 da tree que esta apontando para o blob q vc alterou, q por consequencia vai alterar o sha1 de outra possivel arvore q esteja apontando para essa arvore, que por fim vai alterar o sha1 do commit q que aponta pra arvore inicial.  
Ou seja, não tem como fazer uma alteração e ela passar batido, e nem alguem alterar sem vc saber pq vai aparecer no historico do commit.  
Também não tem como corromper o arquivo numa transferencia pois tem toda essa verificação até o servidor na nuvem e o computador/usuario que ta dando o commit.  

------------
Quando vc cria um arquivo novo e ainda não deu commit, ele fica como Untracked, pq o git ainda não ta vendo ele, depois q vc da o commit ele vai direto para staged, ai na proxima vez q vc mexer nele ele é tracked e vai para modified e quando der add denovo ele vai para staged para aguardar o commit.


`git status` pode dizer q vc removeu um arquivo quando vc move esse arquivo para uma pasta nova q não existia antes.
apenas de um git add "nome do arquivo" "nome da pasta/"
sem as aspas
ou git add . que pega tudo.
e de git status denovo q ele deve dizer certinho q ta movendo, confere bem, e dai da um commit.

--------------