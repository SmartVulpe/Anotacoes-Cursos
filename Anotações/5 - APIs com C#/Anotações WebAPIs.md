
## Oque é uma API

Uma API (Application Programming Interface) é uma forma de comunicação entre computadores ou programas de computadores.
Em outras palavras, é um software que fornece informações para outro software.

API é um software que faz a intermediação entre o software do cliente com o software do servidor. Exemplo: um garçon de um restaurante seria uma API.

---

## Para que serve uma API

Principal função de uma API é: Disponibilizar métodos (endpoints) e serviços, permitindo a comunicação e integração entre diferentes sistemas.

---

## Alguns sites de APIs

date.nager.at - site de api de feriados.
dog.ceo/dog-api - side de api de imagens de cachorros.

---

## Dicas Importantes

- SEMPRE busque ler primeiro a documentação da API para ver como ela funciona e como usa-la.


- `dotnet --help` - use para buscar comandos.

---

## Comandos dotnet para criar e executar api

Comando para criar um projeto de web api:
`dotnet new webapi`

Comando para rodar e quando alterar o código ja recompilar em tempo de execução (similar ao HotReload do vs community):
`dotnet watch run`

---

## Oque é o Swagger

Swagger é um frontend para testar apis em ambiente de desenvolvimento, não é exatamente necessário mas é um recurso que facilita os testes.

---

## Classes Controller

Classes Controller são classes que você vai colocar os métodos relacionados às ações de determinada api, exemplo, Get de produto, Set de produto, e elas devem ser separadas relacionadas ao contexto dela, pro exemplo uma controller de produtos deve ter os controladores relacionado a produtos apenas, não devem mexer em coisas do usuário por exemplo, se precisa mexer no usuário é necessário fazer uma controller para/relacionada ao usuário.  

"Uma controller nada mais é que o ponto de entrada que nos vamos disponibilizar os nossos métodos".

**É necessário fazer o nome das controllers terminando com a palavra Controller, exemplo UsuarioController, ProdutoController...**

### O básico para uma classe controller é:  
Esses [atributos](../2%20-%20%20C%23/Anota%C3%A7%C3%B5es%20CSharp.md/#Atributos) no cabeçalho da classe controller
```c#
    [ApiController]
    [Route("[controller]")]
```
E a classe herdar a ControllerBase, não é Controller, é ControllerBase.
e fazer uma "injeção de dependência" através do construtor.
```c#
private readonly AgendaContext _context;
public ContatoController(AgendaContext context)
{
    _context = context;
}
```
Para todos os métodos http com exceção do get, você tem que chamar o método:
`_context.SaveChanges();`  
Senão ele não salva no banco de dados.

---

## Caminho URL API

O endereço do método no link, é formado pelo localhost (ou o domínio que ele estiver) / nome do controlador sem a palavra controller exemplo UsuarioController, ele vai mostrar só Usuário, e dai no nome que você colocou em cima do método, exemplo:
```c#
[HttpGet("ObterDataHoraAtual")]
public IActionResult ObterDataHora()
```

Exemplo de como o link vai ficar:  
`https://localhost:7275/Usuario/ObterDataHoraAtual`  

--- 

## ORM (Object Relational Mapper)

ORM (Object Relational Mapper) é uma técnica de mapeamento objeto relacional que permite fazer uma relação dos objetos com os dados que os mesmos representam. É isso que o Entity Framework e o Dapper são, e existem varios outros ORM's disponiveis.

---

## Oque é o Entity Framework?

O Entity Framework é um framework ORM (Object-Relational Mapping) criado para facilitar a integração com o banco de dados, mapeando tabelas e gerando comandos SQL de forma automática.  
Resumindo: ele gera os código que você colocaria na query automaticamente.  

--- 

## CRUD

- C - CREATE (Insert)  
- R - READ (Select)  
- U - UPDATE (Update)  
- D - DELETE (Delete)  

---

## Verbos HTTP
- Get - Selecionar/Buscar Dados.  
- Post - Enviar dados.   
- Put - Atualizar dados.    
- Patch - Atualizar parcialmente dados.   
- Delete - Deletar dados.   

---

## Comandos dotnet para instalar pacotes

`dotnet tool install --global dotnet-ef` - Ferramenta para inserir comandos no entity framework via terminal, só precisa instalar uma vez no computador.  

`dotnet add package Microsoft.EntityFrameworkCore.Design` - Pacote para instalar o entity framework no PROJETO, precisa instalar ele em todo projeto que for usar o entity framework.  

`dotnet add package Microsoft.EntityFrameworkCore.SqlServer` - Pacote para instalar o modulo do entity framework para o SQL Server, o EF é modular então precisa instalar o Design q é uma base, e o modulo referente ao banco de dados que você for usar, nesse caso o SQL Server. Também precisa instalar em todo projeto.  

---

## Entidades (Entities) 

São classes no programa que também são tabelas no banco de dados.
Nelas precisa ter propriedades com os mesmos nomes que vai ter na tabela do banco de dados.

---
## Classes Context

Elas fazem uma ligação do programa com o banco de dados, seja de conexão quanto de referenciamento de entidades.
A classe context herda a classe DbContext, nela precisa ter um construtor que vai fazer a ligação da conexão, e vai ter uma propriedade do tipo:  
```c# 
public DbSet<NomeDaEntidade> NomeDaEntidade { get; set; }
```  
Que vai servir para referenciar a entidade, senão ela só vai existir la nas entities mas nao vai funcionar.

---

## AppSettings

Existe 2 arquivos json no projeto, um é o appsetings, e um é o appsettings.Development, o primeiro você configura com as coisas que você vai precisar na hora de implementar o programa em ambiente de produção, e o segundo você usa com as configurações para o ambiente de desenvolvimento, por exemplo configurar para usar um banco de dados que é só para desenvolvimento e configurar um comando para impedir de mandar um email aos usuários.

PS: o appsetting.Developtment.json no visual studio community fica escondido, ao lado do appsetting.json tem um triangulo para abrir como se fosse uma pasta, clique nele e vai aparecer o .Development abaixo.

---

## Connection Strings

Você vai colocar a connection string logo depois de fechar a chave do Logging, a connection string do sql server express é assim:
```json
"ConnectionStrings": {
    "ConexaoPadrao": "Server=localhost\\sqlexpress; Initial Catalog=Agenda; Integrated Security=True"
  }
```
O `"ConnectionStrings":` tem que ser sempre esse nome, mas o "ConexaoPadrao" pode ser o nome que você quiser.

---

## Configurando a conexão com a DB na Program.cs

```c#
builder.Services.AddDbContext<AgendaContext>(options =>
        options.UseSqlServer(builder.Configuration
        .GetConnectionString("ConexaoPadrao")));
```
Aqui nos estamos dizendo para o builder adicionar um DbContext do tipo AgendaContext, e passando algumas opções, dizendo para usar SqlServer, e passando a connection string (caminho para acessar o banco de dados e como fazer login) que está no appsettings.json ou appsettings.Development.json.  

Daria para colocar a connection string direto aqui, mas se um dia precisar mudar teria que recompilar o código, e estando la no json ele vai estar junto com o programa compilado e ai é mais fácil alterar.  

---

## Oque é o Migrations?

O Migrations é um mapeamento que o entity framework faz das nossas classes (entities) para transforma-las em tabelas.  
Ele vai executar nas classes que tiverem referenciadas na classe Context.  
"Migrations é um código que serve para espelhar as suas alterações no código no banco de dados".  
Ele tem um método Up para aplicar mudanças nas tabelas, e um método Down para reverte-las.  

## Executando o Migrations

Para executar o migrations é preciso fazer o comando manualmente via terminal, o comando é:  
`dotnet-ef migrations add CriacaoTabelaContato`  
No caso o **CriacaoTabelaContato** é apenas um nome para definir que você fez nessa migração, como era uma migração simples de apenas uma tabela, foi dado esse nome.   

Na pasta Migrations que o comando vai criar, tem alguns dados da tabela que ele criou.  
Você pode notar duas coisas que ele faz automaticamente:  
Primeiro, ele vai alterar o nome da Entities que deve ser nomeada no singular, para o plural.  
Segundo se a classe tiver uma propriedade Id ele vai automaticamente reconhecer e usar ela como uma identity e adicionar a constraint de Primary Key.  

Ai para adicionar essa tabela no banco de dados use o comando:  
`dotnet-ef database update`  

---

## DataAnnotations

DataAnnotation é um [Atributo](../2%20-%20%20C%23/Anota%C3%A7%C3%B5es%20CSharp.md/#Atributos), com ele podemos definir um comportamento diferente do padrão para uma propriedade ou método.

**Alguns Atributos:**  


- `[Key]` - Identifica uma propriedade como uma chave primaria na tabela, normalmente não é usado pois o EFCore automaticamente define uma propriedade como chave primaria se você colocar Id ou AlgumNomeId (Id no final do nome).  
- `[Table("nome")]` - Define um nome para a tabela que a classe será mapeada.   Também não é muito usado pois o EFCore também faz isso automaticamente quando você define as classes no DbContext.  
- `[Column]` - Define a coluna na tabela que a propriedade será mapeada, normalmente usado para especificar a propriedade na tabela (exemplos abaixo).  
- `[DataType]` - Especifica um tipo de dados adicional a uma propriedade.  
- `[ForeignKey]` - Especifica que a propriedade é usada como uma chave estrangeira, pouco usado pelo mesmo motivo do Key.  
- `[NotMapped]` - Exclui a propriedade do mapeamento.  
- `[StringLenght]` - Define o tamanho mínimo e máximo permitido para o tipo.  
- `[Required]` - Especifica que o valor do campo é obrigatório.  
**Fonte: Curso WebAPI AspNet Core do Macoratti.**

Mais atributos: [DataAnnotations - Learn EF Core](https://www.learnentityframeworkcore.com/configuration/data-annotation-attributes)

**Exemplos de uso:**  

```c#
// Propriedades do tipo string
// Com mensagem de erro:
[StringLength(80), ErrorMessage = "Texto muito longo"]
// Ou sem mensagem de erro:
[StringLength(80)]
public string Nome { get; set; }

// Propriedades do tipo decimal
[Column(TypeName = "decimal(18,4)")]
public decimal Valor { get; set; }

// Tornando obrigatório
// Com mensagem de erro:
[Required(ErrorMessage = "Essa propriedade é obrigatória")]
// Ou sem mensagem de erro:
[Required]
public string Nome { get; set; }


// Também dá para combinar:
[Required]
[StringLength(80)]
public string Nome { get; set; }

// E combinar com mensagem de erro:
[Required(ErrorMessage = "Essa propriedade é obrigatória")]
[StringLength(80), ErrorMessage = "Texto muito longo"]
public string Nome { get; set; }
```
**Fonte: Curso WebAPI AspNet Core do Macoratti.**

OBS: No curso o Macoratti diz que usar DataAnnotations deixa o código "meio poluído" e que seria mais "elegante" usar a Fluent API para isso. Pelo que deu a entender é só uma questão estética não tendo muita diferença em qualidade.

---

## Rotas

Quando você tem mais de um método do mesmo tipo que pega exatamente as mesmas propriedades, ele da erro, mesmo eles tendo nomes diferentes (e é necessário ter nomes diferentes a menos que seja um polimorfismo do tipo overload), para o mapeamento de controladores ambos são a mesma coisa.

Para resolver isso há duas opções

Uma é fazer o sistema reconhecer o nome do método na rota:

No atributo de rota que fica no cabeçalho da classe da para fazer isso:
```c#
    [Route("[controller/{action}]")]
```
E então na URL voce vai digitar o `NomeDaControladora/NomeDoMetodo`.  

A outra forma é adicionar rotas nos métodos em si:  

```c#
[HttpGet("produtos")]
```
Ai na hora de escrever na URL, usando o exemplo acima, vai ser o `NomeDaControladora/produtos`.

---

## Tipos de retorno de ação

[Tipos de retorno de ação do controlador na API Web do ASP.NET Core - Microsoft Learn](https://learn.microsoft.com/pt-br/aspnet/core/web-api/action-return-types?view=aspnetcore-7.0)

---

## Informações interessantes  

### Uso do FromBody  

***Antes do dotnet core 2.2***, era necessário colocar `[FromBody]` e um if de validação nos métodos action.  
Exemplo:  
```c#
[HttpPost]
public ActionResult Post([FromBody] Produto produto)
{
    if(!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }
}
```
A partir da versão 2.2 com a introdução do atributo `[ApiController]` no cabeçalho da classe, essa validação se tornou automática, então não é mais necessário o FromBody e o if.  

---