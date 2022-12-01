# Comandos SQL

**Os comandos SQL são universais entre os bancos que seguem o padrão SQL**

- Primeiramente, os comandos funcionam em minusculo, mas a boa pratica do sql é usar os comandos/palavras reservadas em maiúsculo.

- Segundo, UPDATE e DELETE devem sempre ser usados com o comando WHERE e de preferencia com uma ID, pois são comandos destrutivos que geralmente não tem volta, se fizer sem o where ele vai atualizar a tabela toda ao invés de um cliente só ou deletar a tabela toda.

- Terceiro, no sql usa aspas simples.

## Comandos

**`SELECT * FROM Clientes`** - seleciona tudo da tabela Clientes, o asterisco significa "todas as colunas da tabela".

---

**`SELECT Nome, Sobrenome FROM Clientes`** - puxa somente as colunas nome e sobrenome. (ps: trazer só as colunas que você quer é uma boa pratica alem de conferir mais performance ao programa)

---

**`ORDER BY Sobrenome`** - ordena as tabelas pela ordem crescente da coluna Sobrenome, que é string então vai ser ordem alfabetica.

---

**`ORDER BY Nome DESC`** - ordena as tabelas pela ordem DEcrescente da coluna Nome, que é string então vai ser ordem alfabetica.

---

**`ORDER BY Nome, Sobrenome`** - ordena a tabela pelo nome e pelo sobrenome, onde tiver um "aglomerado" de clientes com o mesmo nome, ele vai orderar pelo sobrenome também.

---

**`WHERE Nome = 'Adam'`** - vai retornar todos os clientes com o nome de Adam. (precisa ter um SELECT FROM antes do WHERE).

---

**`WHERE Nome = 'Adam' AND Sobrenome = 'Reynolds'`** - retorna o cliente que tiver o nome Adam E o sobrenome Reynolds.

---

**`WHERE Nome = 'Adam' OR Sobrenome = 'Reynolds'`** - retorna os clientes que tiver o nome Adam OU o sobrenome Reynolds.

---

**`WHERE Nome LIKE 'G%'`** - retorna todos os nomes que começam com G. o Like permite consultas com caracteres especiais, e o porcentagem significa que é para ignorar tudo oq vier depois, só é obrigatório o G no inicio, e ser fizer %G% iria buscar todo mundo que tiver a letra G em qualquer lugar do nome.

---

**`INSERT INTO Clientes (Nome, Sobrenome, Email, AceitaComunicados, DataCadastro)
VALUES ('Daniel', 'Franco', 'email@email.com', 1, GETDATE())`**  
Esse comando insere um cliente na tabela, seguindo a ordem de colunas passada na primeira linha, se vc passar uma ordem diferente, desde que no VALUES vc respeite a ordem diferente que voce passou dá certo.

---

**`INSERT INTO Clientes VALUES ('Daniel', 'Franco', 'email@email.com', 1, GETDATE())`**
Se fizer dessa forma funciona tambem, mas dai é obrigatorio seguir a ordem de colunas que está na tabela, se inverter vai dar erro, na opção anterior vc pode definir a ordem que vc quer, nessa opção não dá.

---

**SEMPRE DE UPDATE USANDO O WHERE, SE VC ESQUECER DO WHERE VAI EDITAR TODOS OS CLIENTES E AI SÓ VOLTANDO BACKUP SE TIVER BACKUP:**
```sql
UPDATE Clientes
SET Email = 'emailatualizado@email.com', 
    AceitaComunicados = 0
WHERE Id = 1003
```
esse comando atualiza o email e o booleano AceitaComunicados do cliente com o Id 1003, é melhor usa o Id nesses casos pq o Id é unico e garante que não ta mudando no errado.

---

**`BEGIN TRAN`** - esse comando cria tipo um checkpoint para dar rollback, se nao executar antes de uma ação critica, depois nao adianta tentar dar rollback.

---

**`ROLLBACK`** - esse comando retorna ao checkpoint criado pelo begin tran.

---

**`DELETE Clientes WHERE Id = 1006`** - deleta o cliente da id 1006 da tabela Clientes. TAMBÉM NUNCA EXECUTE ISSO SEM O COMANDO WHERE.

---

Para criar uma tabela:  
```sql
CREATE TABLE Produtos (  
	Id int IDENTITY(1,1) PRIMARY KEY NOT NULL, --o banco de dados vai gerenciar uma id para nos. primary key significa que a ID vai ser unica e jamais vai se repetir, mesmo q vc delete uma ID ela jamais vai ser reutilizada.  
	Nome varchar(255) NOT NULL, --uma string de até 255 caracteres  
	Cor varchar(50) NULL, --uma string de até 50 caracteres  
	Preco decimal(13,2) NOT NULL,   
	Tamanho varchar(5) NULL, --string de 5 caracteres  
	Genero char(1) NULL --um caractere  
)  
```

---

Esse comando altera a linguagem durante a execução da query:  
**`SET LANGUAGE 'Português'`**  
Isso resolve o problema que eu tive com o script que não conseguia converter a data pois os meses estavam com as iniciais em ingles ao invés de Português, no meu caso teria que usar SET LANGUAGE 'INGLES'. E esse comando afeta só a query, se vc trocar de query ele volta a seguir o padrão original do servidor.

---

**`DROP TABLE IF EXISTS dbo.Produtos`** - deleta a tabela Produtos se ela existir.

---

**`SELECT COUNT(*) FROM Produtos`** - retorna a quantidade de linhas que tiver na tabela produtos, a coluna com o valor de linhas vai aparecer que a coluna está sem nome, você pode dar um nome para o retorno escrevendo o comando dessa forma `"SELECT COUNT(*) QuantidadeProdutos FROM Produtos"` ai ele vai nomear a coluna como QuantidadeProdutos.

---

Também da para combinar o COUNT(*) com o where:  
**`SELECT COUNT(*) QuantidadeProdutosTamanhoM FROM Produto WHERE Tamanho = 'M'`**  
Ai ele vai retornar quantos produtos com tamanho M tem.

---

**`SELECT SUM(Preco) PrecoTotal FROM Produtos`** - retorna a soma de todos os itens da coluna preço (obviamente só funciona com colunas de tipos numericos). também da para usar WHERE.

---

**`SELECT MAX(Preco) FROM Produtos`** - retorna o valor mais alto da coluna Preco, também da para dar um retorno com nome, e usar WHERE.

---

**`SELECT MIN(Preco) ProdutoMaisBarato FROM Produtos`** - retorna o valor mais baixo da coluna Preco, também da para usar WHERE.

---

**`SELECT AVG(Preco) FROM Produtos`** - ele vai somar e tirar a media do valor dos itens da coluna Preco.

---

```sql
SELECT
	Nome + ', Cor: ' + Cor
FROM Produtos
```
Concatena colunas, isso ai vai retornal algo estilo: 
NomeDoProduto, Cor: branco
e se fizer assim:
```sql
SELECT
	Nome + ', Cor: ' + Cor NomeProduto
FROM Produtos
```
ele vai retornar como uma coluna de nome NomeProduto.
e se fizer assim:
```
SELECT
	Nome + ', Cor: ' + Cor NomeProdutoCompleto,
	Nome,
	Cor
FROM Produtos
```
Ele vai retornar uma coluna de nome NomeProdutoCompleto que é a nossa concatenação, uma coluna só com o Nome e uma coluna só com a Cor.

---


**`UPPER(Nome)`** - função que deixa o tudo em maiúsculo.  
**`LOWER(Cor)`** - função que deixa tudo em minusculo.  
Essas funções são usadas junto com a select, e elas vão retornar colunas sem nomes, então é legar nomear elas.  
Exemplo:  
**`SELECT UPPER(Nome) Nome FROM Produtos`**

---

```sql
ALTER TABLE Produtos
ADD DataCadastro DATETIME2
```
Altera a tabela produtos adicionando a coluna DataCadastro que é o tipo datetime2.

---

```sql
ALTER TABLE Produtos
DROP DataCadastro
```
altera a tabela produtos removendo a coluna DataCadastro.

---

Para formatar a data, ao chamar pelo select usa o comando:  
**`FORMAT(DataCadastro, 'dd/MM/yyyy hh:mm')`**  
Obs: se quiser a hora no formato de 24hrs coloque o h maiúsculo HH:mm.

---

Para agrupar a lista por similares da mesma tabela e contar quantos que agrupou, exemplo agrupou todos os produtos tamanho G, ai aparece G - 11, pq eram 11 produtos desse tamanho.  
```sql
SELECT Tamanho, COUNT(*) Quantidade FROM Produtos --precisa do GROUP BY pra isso funciona
WHERE Tamanho <> '' --o simbolo <> significa diferente, então seria lido como: ONDE Tamanho for diferente de nada.
GROUP BY Tamanho --agrupa onde for igual dessa tabela.
ORDER BY Quantidade DESC --ordena do maior para o menor da tabela Quantidade q é criada pelo resultado ali na primeira linha.
```
Obs: a ordem desses comandos é importante.

---

Para definir uma ID como primary key que foi gerada só como IDENTITY que faz ela ser única:
Vá no seu DB > Tabelas, e clique na tabela em questão com o botão direito e em Designe, ai clica no Id com o botão direito e Adicionar Primary Key, e dá ctrl+S para salvar.

---

Ao criar uma tabela, dentro do parenteses com os dados de criação, se você for colocar uma foreign key voce faz assim:
```sql
CREATE TABLE Enderecos (
	Id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
	IdCliente int NULL,
	Rua varchar(255) NULL,
	Bairro varchar(255) NULL,
	Cidade varchar(255) NULL,
	Estado char(2) NULL,

	CONSTRAINT FK_Enderecos_Clientes FOREIGN KEY(IdCliente)
	REFERENCES Clientes(Id)
)
```
Explicando, toda foreign key é uma restrição (constraint) e você dá um nome para essa restrição, na boa pratica vc coloca FK pra dizer que é foreign key e o nome das duas tabelas que se relacionam, em seguida basicamente você especifica que o int IdCliente é a coluna vai mostrar/armazenar a referencia, e por fim você referencia para o Id da tabela de clientes.

---

**`INNER JOIN`** - retorna a junção de duas tabelas relacionadas.  
Como usar:
```sql
SELECT * FROM Clientes --puxa tudo do Clientes
INNER JOIN Enderecos ON Clientes.Id = Enderecos.IdCliente --Junta oque veio com a tabela endereços, mas só se o id de clientes bater com o idcliente da tabela endereços.
WHERE Clientes.Id = 4
```

---

```sql
ALTER TABLE Produtos
ADD UNIQUE(Nome)
```
Altera a tabela produtos para que a coluna Nome se torne unica, ou seja, não pode repetir dados, se ja tiver um nome la e tentar botar outro nome IGUAL ele vai dar erro.

---

```sql
ALTER TABLE Produtos
ADD CONSTRAINT CHK_ColunaGenero CHECK(Genero = 'U' OR Genero = 'M' OR Genero = 'F')
```
Cria uma regra (restrição) de checagem chamada CHK_ColunaGenero (você pode dar o nome que quiser ou se nao quiser não precisa nomear pode deixar sem nome mas o nome facilita para verificar oque é nas propriedades da tabela) que checa se ao adicionar um produto ele está recebendo uma das 3 letras U (unisex) ou M (masculino) ou F (feminino), se for outra coisa ele vai retornar erro.

---

```sql
ALTER TABLE Produtos
ADD DEFAULT GETDATE() FOR DataCadastro
```
Faz uma regra (restrição) que por padrão na hora de adicionar um cliente se não for informado a data de cadastro ele puxa a data atual.

---

Para apagar uma constraint (regra):  
Seleciona o nome da tabela na query, aperta alt+f1 para abrir as propriedades, ai você busca la qual é a constraint que você quer apagar, da um ctrl+c no nome para copiar ele certinho pq se não foi dado um nome vai ter monte de numero como no exemplo abaixo, ai na query vc escreve:  
```sql
ALTER TABLE Produtos
DROP CONSTRAINT CK__Produtos__Genero__5165187F
```

---

É possível criar uma PROCEDURE que é como um método, para facilitar a inserção de dados quando você normalmente repete muito os comandos.  
E faz da seguinte forma:
```sql
CREATE PROCEDURE InserirNovoProduto
@Nome varchar(255),
@Cor varchar(50),
@Preco decimal,
@Tamanho varchar(5),
@Genero char(1)

AS

INSERT INTO Produtos (Nome, Cor, Preco, Tamanho, Genero)
VALUES(@Nome, @Cor, @Preco, @Tamanho, @Genero)
```
Dai voce executa e ta salva a procedure, para ver as procedures da db vá até a db em questão, Programmability, Stored Procedures, ai vai ta ai, no caso essa do exemplo vai ta aparecendo como dbo.InserirNovoProduto. (se nao aparecer clique no ícone de refresh)

para executar a procedure:
```sql
EXEC InserirNovoProduto
'NomeDoProduto',
'CorDoProduto',
50,
'G',
'U'
```
e executa.

Mais um exemplo de criação de procedure:
```sql
CREATE PROCEDURE ObterProdutoPorTamanho
@TamanhoProduto VARCHAR(5)
AS
SELECT * FROM Produtos WHERE Tamanho = @TamanhoProduto

--E executa dessa forma:
EXEC OobterProdutoPorTamanho 'M'

--Mais um exemplo de criação de procedure:
CREATE PROCEDURE ObterProdutoTamanhoM
AS
SELECT * FROM Produtos WHERE Tamanho = 'M'

--E executa dessa forma:
EXEC ObterProdutoTamanhoM
```
---

Functions são como procedures que são como métodos de programação
A principal diferença é que functions sempre tem que ter um retorno.
exemplo:  
```sql
CREATE FUNCTION CalcularDesconto(@Preco DECIMAL(13, 2), @Porcentagem INT)
RETURNS DECIMAL(13, 2)

BEGIN
	RETURN @Preco - @Preco / 100 * @Porcentagem
END
```
Explicando: o `@` é o atributo, `DECIMAL(13, 2)` é o tipo decimal já formatado para mostrar 13 casas antes da virgula e 2 casas depois da virgula, `RETURNS` no plural é o tipo de retorno do método, o `begin` e `end` é tipo as chaves {}, e o `RETURN` é igual o return de programação.  

Exemplo de uso:
```sql
SELECT
	Nome,
	Preco,
	dbo.CalcularDesconto(Preco, 50) PrecoComDesconto
FROM Produtos WHERE Tamanho = 'M'
```
Resultado:  
Ele vai pegar o valor da coluna preço dos produtos de Tamanho M e adicionar 50% de desconto, e mostrar o novo valor na coluna PrecoComDesconto.
Então no resultado terá 3 colunas: Nome, Preco que está com o valor inalterado, e a PrecoComDesconto que está com o valor ja descontado.

---

`CTRL + K + C` - comenta oq tiver selecionado

---

**Se vc executar e tiver algo selecionado ele vai executar só oq tiver selecionado, se nao tiver nada selecionado ele executa tudo oque tiver escrito na query.**

---

ALT+F1 estando com o nome da tabela selecionado na Query - Abre as propriedades da tabela, mostrando o tipo que é cada coluna e seus detalhes como por exemplo se pode ou não ser nula.
