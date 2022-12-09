
***Essa anotação ainda está em construção, ainda há algumas coisas desorganizadas, e outras que precisam ser revisadas.***


# Índice

- [Índice](#índice)
- [Anotações](#anotações)
  - [Oque é uma API](#oque-é-uma-api)
  - [Para que serve uma API](#para-que-serve-uma-api)
  - [**PRECISA ADICIONAR** Oque é Rest/RestFull](#precisa-adicionar-oque-é-restrestfull)
  - [**PRECISA ADICIONAR** Oque Torna uma API Rest/RestFull](#precisa-adicionar-oque-torna-uma-api-restrestfull)
  - [Alguns sites de APIs](#alguns-sites-de-apis)
  - [Dicas Importantes](#dicas-importantes)
  - [Comandos dotnet para criar e executar api](#comandos-dotnet-para-criar-e-executar-api)
  - [Oque é o Swagger](#oque-é-o-swagger)
  - [Classes Controller](#classes-controller)
    - [O básico para uma classe controller é:](#o-básico-para-uma-classe-controller-é)
  - [Caminho URL API](#caminho-url-api)
  - [ORM (Object Relational Mapper)](#orm-object-relational-mapper)
  - [Oque é o Entity Framework?](#oque-é-o-entity-framework)
  - [CRUD](#crud)
  - [Verbos HTTP](#verbos-http)
  - [Comandos DotNet para instalar pacotes](#comandos-dotnet-para-instalar-pacotes)
  - [Entidades (Entities)](#entidades-entities)
  - [Classes Context](#classes-context)
  - [AppSettings](#appsettings)
  - [Connection Strings](#connection-strings)
  - [Configurando a conexão com a DB na Program.cs](#configurando-a-conexão-com-a-db-na-programcs)
  - [Oque é o Migrations?](#oque-é-o-migrations)
    - [Executando o Migrations](#executando-o-migrations)
  - [DataAnnotations](#dataannotations)
  - [Validação](#validação)
    - [Criando Atributo customizado](#criando-atributo-customizado)
    - [IValidatableObject](#ivalidatableobject)
  - [Rotas / Endpoints](#rotas--endpoints)
    - [Informar mais de um parâmetro na action](#informar-mais-de-um-parâmetro-na-action)
    - [Oque acontece se colocar uma barra no inicio do endpoint da action?](#oque-acontece-se-colocar-uma-barra-no-inicio-do-endpoint-da-action)
    - [Múltiplos endpoints na mesma action](#múltiplos-endpoints-na-mesma-action)
  - [Restrição de Rotas](#restrição-de-rotas)
    - [Tabela de Referencia de Restrições](#tabela-de-referencia-de-restrições)
  - [Tipos de retorno de ação](#tipos-de-retorno-de-ação)
    - [Tipo Especifico](#tipo-especifico)
    - [IActionResult](#iactionresult)
    - [`ActionResult<T>`](#actionresultt)
  - [Model Binding](#model-binding)
    - [QueryStrings](#querystrings)
    - [Valores de Formulários](#valores-de-formulários)
    - [Atributos para definir de onde é a fonte dos dados](#atributos-para-definir-de-onde-é-a-fonte-dos-dados)
    - [\[FromServices\]](#fromservices)
    - [Atribuição automática](#atribuição-automática)
  - [Métodos Assíncronos](#métodos-assíncronos)
    - [Vale a pena usar Actions Assíncronas?](#vale-a-pena-usar-actions-assíncronas)
  - [Informações interessantes](#informações-interessantes)
    - [Serviço Scooped, Singleton e Transient](#serviço-scooped-singleton-e-transient)
  - [Soluções de problemas](#soluções-de-problemas)
    - [Problema de Serialização CÍCLICA](#problema-de-serialização-cíclica)
  - [Otimizando o código](#otimizando-o-código)
    - [HTTP GET](#http-get)
      - [Dicas:](#dicas)



# Anotações

## Oque é uma API

Uma API (Application Programming Interface) é uma forma de comunicação entre computadores ou programas de computadores.
Em outras palavras, é um software que fornece informações para outro software.

API é um software que faz a intermediação entre o software do cliente com o software do servidor. Exemplo: um garçon de um restaurante seria uma API.

[Voltar ao Índice](#índice)

---

## Para que serve uma API

Principal função de uma API é: Disponibilizar métodos (endpoints) e serviços, permitindo a comunicação e integração entre diferentes sistemas.

[Voltar ao Índice](#índice)

---

## **PRECISA ADICIONAR** Oque é Rest/RestFull



[Voltar ao Índice](#índice)

---

## **PRECISA ADICIONAR** Oque Torna uma API Rest/RestFull



[Voltar ao Índice](#índice)

---

## Alguns sites de APIs

date.nager.at - site de api de feriados.
dog.ceo/dog-api - side de api de imagens de cachorros.

[Voltar ao Índice](#índice)

---

## Dicas Importantes

- SEMPRE busque ler primeiro a documentação da API para ver como ela funciona e como usa-la.


- `dotnet --help` - use para buscar comandos.

[Voltar ao Índice](#índice)

---

## Comandos dotnet para criar e executar api

Comando para criar um projeto de web api:
`dotnet new webapi`

Comando para rodar e quando alterar o código ja recompilar em tempo de execução (similar ao HotReload do vs community):
`dotnet watch run`

[Voltar ao Índice](#índice)

---

## Oque é o Swagger

Swagger é um frontend para testar apis em ambiente de desenvolvimento, não é exatamente necessário mas é um recurso que facilita os testes.

[Voltar ao Índice](#índice)

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

[Voltar ao Índice](#índice)

---

## Caminho URL API

O endereço do método no link, é formado pelo localhost (ou o domínio que ele estiver) / nome do controlador sem a palavra controller exemplo UsuarioController, ele vai mostrar só Usuário, e dai no nome que você colocou em cima do método, exemplo:
```c#
[HttpGet("ObterDataHoraAtual")]
public IActionResult ObterDataHora()
```

Exemplo de como o link vai ficar:  
`https://localhost:7275/Usuario/ObterDataHoraAtual`  

[Voltar ao Índice](#índice)

--- 

## ORM (Object Relational Mapper)

ORM (Object Relational Mapper) é uma técnica de mapeamento objeto relacional que permite fazer uma relação dos objetos com os dados que os mesmos representam. É isso que o Entity Framework e o Dapper são, e existem varios outros ORM's disponiveis.

[Voltar ao Índice](#índice)

---

## Oque é o Entity Framework?

O Entity Framework é um framework ORM (Object-Relational Mapping) criado para facilitar a integração com o banco de dados, mapeando tabelas e gerando comandos SQL de forma automática.  
Resumindo: ele gera os código que você colocaria na query automaticamente.  

[Voltar ao Índice](#índice)

--- 

## CRUD

- C - CREATE (Insert)  
- R - READ (Select)  
- U - UPDATE (Update)  
- D - DELETE (Delete)  

[Voltar ao Índice](#índice)

---

## Verbos HTTP
- Get - Selecionar/Buscar Dados.  
- Post - Enviar dados.   
- Put - Atualizar dados.    
- Patch - Atualizar parcialmente dados.   
- Delete - Deletar dados.   

[Voltar ao Índice](#índice)

---

## Comandos DotNet para instalar pacotes

`dotnet tool install --global dotnet-ef` - Ferramenta para inserir comandos no entity framework via terminal, só precisa instalar uma vez no computador.  

`dotnet add package Microsoft.EntityFrameworkCore.Design` - Pacote para instalar o entity framework no PROJETO, precisa instalar ele em todo projeto que for usar o entity framework.  

`dotnet add package Microsoft.EntityFrameworkCore.SqlServer` - Pacote para instalar o modulo do entity framework para o SQL Server, o EF é modular então precisa instalar o Design q é uma base, e o modulo referente ao banco de dados que você for usar, nesse caso o SQL Server. Também precisa instalar em todo projeto.  

[Voltar ao Índice](#índice)

---

## Entidades (Entities) 

São classes no programa que também são tabelas no banco de dados.
Nelas precisa ter propriedades com os mesmos nomes que vai ter na tabela do banco de dados.

[Voltar ao Índice](#índice)

---
## Classes Context

Elas fazem uma ligação do programa com o banco de dados, seja de conexão quanto de referenciamento de entidades.
A classe context herda a classe DbContext, nela precisa ter um construtor que vai fazer a ligação da conexão, e vai ter uma propriedade do tipo:  
```c# 
public DbSet<NomeDaEntidade> NomeDaEntidade { get; set; }
```  
Que vai servir para referenciar a entidade, senão ela só vai existir la nas entities mas nao vai funcionar.

[Voltar ao Índice](#índice)

---

## AppSettings

Existe 2 arquivos json no projeto, um é o appsetings, e um é o appsettings.Development, o primeiro você configura com as coisas que você vai precisar na hora de implementar o programa em ambiente de produção, e o segundo você usa com as configurações para o ambiente de desenvolvimento, por exemplo configurar para usar um banco de dados que é só para desenvolvimento e configurar um comando para impedir de mandar um email aos usuários.

PS: o appsetting.Developtment.json no visual studio community fica escondido, ao lado do appsetting.json tem um triangulo para abrir como se fosse uma pasta, clique nele e vai aparecer o .Development abaixo.

[Voltar ao Índice](#índice)

---

## Connection Strings

Você vai colocar a connection string logo depois de fechar a chave do Logging, a connection string do sql server express é assim:
```json
"ConnectionStrings": {
    "ConexaoPadrao": "Server=localhost\\sqlexpress; Initial Catalog=Agenda; Integrated Security=True"
  }
```
O `"ConnectionStrings":` tem que ser sempre esse nome, mas o "ConexaoPadrao" pode ser o nome que você quiser.

[Voltar ao Índice](#índice)

---

## Configurando a conexão com a DB na Program.cs

```c#
builder.Services.AddDbContext<AgendaContext>(options =>
        options.UseSqlServer(builder.Configuration
        .GetConnectionString("ConexaoPadrao")));
```
Aqui nos estamos dizendo para o builder adicionar um DbContext do tipo AgendaContext, e passando algumas opções, dizendo para usar SqlServer, e passando a connection string (caminho para acessar o banco de dados e como fazer login) que está no appsettings.json ou appsettings.Development.json.  

Daria para colocar a connection string direto aqui, mas se um dia precisar mudar teria que recompilar o código, e estando la no json ele vai estar junto com o programa compilado e ai é mais fácil alterar.  

[Voltar ao Índice](#índice)

---

## Oque é o Migrations?

O Migrations é um mapeamento que o entity framework faz das nossas classes (entities) para transforma-las em tabelas.  
Ele vai executar nas classes que tiverem referenciadas na classe Context.  
"Migrations é um código que serve para espelhar as suas alterações no código no banco de dados".  
Ele tem um método Up para aplicar mudanças nas tabelas, e um método Down para reverte-las.  

[Voltar ao Índice](#índice)

### Executando o Migrations

Para executar o migrations é preciso fazer o comando manualmente via terminal, o comando é:  
`dotnet-ef migrations add CriacaoTabelaContato`  
No caso o **CriacaoTabelaContato** é apenas um nome para definir que você fez nessa migração, como era uma migração simples de apenas uma tabela, foi dado esse nome.   

Na pasta Migrations que o comando vai criar, tem alguns dados da tabela que ele criou.  
Você pode notar duas coisas que ele faz automaticamente:  
Primeiro, ele vai alterar o nome da Entities que deve ser nomeada no singular, para o plural.  
Segundo se a classe tiver uma propriedade Id ele vai automaticamente reconhecer e usar ela como uma identity e adicionar a constraint de Primary Key.  

Ai para adicionar essa tabela no banco de dados use o comando:  
`dotnet-ef database update`  

[Voltar ao Índice](#índice)

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
- `[RegularExpression(".+\\@.+\\..+")]` - Permite usar expressões regulares em validações mais específicas.
- `[Compare("Senha")]` - Compara duas propriedades que o usuário informou (util para validação de senha, exemplo aquele campo para repetir a senha para confirmar).
**Fonte: Curso WebAPI AspNet Core do Macoratti.**

Mais atributos:  
[DataAnnotations - Learn EF Core](https://www.learnentityframeworkcore.com/configuration/data-annotation-attributes)  
[Data Annotation Attributes - DevExpress](https://docs.devexpress.com/AspNet/400998/components/site-navigation-and-layout/form-layout/concepts/data-annotation-attributes)  
[Model validation in ASP.NET Core MVC and Razor Pages - Microsoft Learn](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/validation?view=aspnetcore-7.0)

**Exemplos de uso:**  

Na classe da Entity/Models:
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

// Também dá para especificar o máximo e o mínimo. 
[StringLength(80, MinimumLength=4)]
public string Nome { get; set; }

// E combinar com mensagem de erro:
[Required(ErrorMessage = "Essa propriedade é obrigatória")]
[StringLength(80), ErrorMessage = "Texto muito longo"]
public string Nome { get; set; }

// Exemplo de validação especifica de email.
[RegularExpression(".+\\@.+\\..+", ErrorMessage = "Informe um email válido...")]
public string Email { get; set; }
```
**Fonte: Curso WebAPI AspNet Core do Macoratti.**

OBS: No curso o Macoratti diz que usar DataAnnotations deixa o código "meio poluído" e que seria mais "elegante" usar a Fluent API para isso. Pelo que deu a entender é só uma questão estética não tendo muita diferença em qualidade.

[Voltar ao Índice](#índice)

---

## Validação

A validação pode ser feita de duas formas, usando os atributos [DataAnnotations](#dataannotations), ou uma interface `IValidatableObject`.  

Usando atributos, nós temos os atributos pré definidos, alguns exemplos aqui: [DataAnnotations](#dataannotations).    
E temos também a possibilidade de criar um atributo customizado.  

### Criando Atributo customizado

Para criar um atributo customizado fazemos o seguinte.    
- Primeiro é recomendado criar uma classe dentro de uma pasta **Validations**, essa classe deve ter no final de seu nome OBRIGATORIAMENTE a palavra **Attribute**, exemplo: PrimeiraLetraMaiusculaAtribbute.   
- Ela deve herdar de **ValidationAttribute**.  
- Deve sobrescrever o método **IsValid**.  
- O **object? value** é o dado de entrada que será validado.  
- O ValidationContext traz informações do contexto que o atributo de validação está sendo executado (ele é necessário mesmo que você não use ele diretamente).  
  
Seu método principal deve se parecer com isso:    
```c#
protected override ValidationResult? IsValid(object? value,
            ValidationContext validationContext)
{
  // seu código aqui
  // Exemplo da primeira letra maiúscula
  if (value == null || string.IsNullOrEmpty(value.ToString()))
  {
      return ValidationResult.Success;
  }

  var primeiraLetra = value.ToString()[0].ToString();
  if (primeiraLetra != primeiraLetra.ToUpper())
  {
      return new ValidationResult("A primeira letra do nome tem que ser maiúscula!");
  }
  return ValidationResult.Success;
}
```
Explicando o código:  
Primeiramente não é a função desse atributo do exemplo verificar se o valor é ou não nulo, sua função é apenas verificar a primeira letra da string, porém se for nulo ele não funciona, então se for nulo ele retorna um sucesso antes de verificar a letra e deixa a cargo das outras validações decidirem se é permitido ou não ser nulo.  
Não sendo nulo ele vai fazer sua operação, sempre que você retorna um ValidationResult que não seja `.Success` ele considera que é um erro 400, pois quando há um sucesso na validação o retorno é silencioso (não tem como mandar mensagem).  

### IValidatableObject

Esse formato de validação é feito direto na model do produto por exemplo, ela tem como desvantagem não ser reaproveitável pois ela é criada direto na model para aquela model apenas, mas tem como vantagem permitir validações mais complexas e **bem** especificas, como por exemplo verificar alguma interação entre propriedades como só ser valido se propriedade A e propriedade B tiverem determinados dados.

Para faze-lo:
- A classe de modelo tem que implementar a interface **IValidatableObject**.
- O método de validação é colocado abaixo das propriedades da model.

```c#
namespace Models;
public class Produto : IValidatableObject
{
  public int ProdutoId { get; set; }
  public string? Nome { get; set; }
  public string? Descricao { get; set; }
  public decimal Preco { get; set; }
  public float Estoque { get; set; }
  public DateTime DataCadastro { get; set; }

  public IEnumerable<ValidationResult> Validate(ValidationContex validationContext)
  {
    if (!string.IsNullOrEmpty(this.Nome))
        {
            var primeiraLetra = this.Nome[0].ToString();
            if (primeiraLetra != primeiraLetra.ToUpper())
            {
                yield return new
                  ValidationResult("Aprimeira letra do produto deve ser maiúscula",
                  new[]
                  { nameof(this.Nome) }
                  );
            }
        }

        if (this.Estoque <= 0)
        {
            yield return new
                ValidationResult("O estoque deve ser maior que zero",
                new[]
                { nameof(this.Estoque) }
                );
        }

        // exemplo de interação de propriedades que
        // essa forma de validação permite e a via Atributo não
        // "Easter Egg"
        if (this.Nome == "Café" && this.Estoque == 0)
        {
            yield return new
                ValidationResult("CAFÉÉÉÉ!!! QUERO CAFÉÉÉ!!! NÃO TEM CAFÉÉÉ!!!!!!!!!",
                new[]
                { "Easter Egg" });
        }

  }
}
```

[Voltar ao Índice](#índice)

---

## Rotas / Endpoints

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

</br>

### Informar mais de um parâmetro na action 

Para mais de um parâmetro tem que colocar uma barra entre as chaves
```c#
[HttpGet("{id}/{produto}")]
```
Exemplo de como fica a url `https://localhost:7275/Produtos/1/Refri`
Ou seja, NomeDoControlador/id/produto

Também é possível definir um valor padrão, quando o valor não for informado ele usa esse valor padrão, exemplo:
```c#
[HttpGet("{id}/{produto=Pastel}")]
```

Para múltiplos parâmetros confira também [Model Binding](#model-binding)

[Voltar ao Índice](#índice)

### Oque acontece se colocar uma barra no inicio do endpoint da action?

Se colocar uma barra no endpoint da action, ele ignora a rota que está no atributo Route que está no cabeçalho da classe do controlador.
```c#
[HttpGet("/primeiro")]
```
A URL fica assim: `https://localhost:7275/primeiro`  
Mesmo que na rota da classe tenha mais coisas, exemplo: `Route("[sistema/v2/api/Controller]")` ele vai ignorar toda essa rota e fazer como no exemplo acima.  

[Voltar ao Índice](#índice)

### Múltiplos endpoints na mesma action

Uma action também pode ter mais de um EndPoint.  
Exemplo:  
```c#
[HttpGet("primeiro")]
[HttpGet("teste")]
[HttpGet("/primeiro")]
public ActionResult<Produto> Get()
{}
```
Nesse exemplo essa action vai poder ser acessada por 3 exemplos de rotas diferentes:  
`https://localhost:7275/produtos/primeiro`
`https://localhost:7275/produtos/teste`
`https://localhost:7275/primeiro`

[Voltar ao Índice](#índice)

## Restrição de Rotas

É possível restringir os parâmetros informados nas rotas. Definindo um tipo a ser recebido, valor mínimo, máximo, somente letras, etc.  

**Apesar de servir, isso não deve ser usado como validação e sim como filtro** (vide o aviso abaixo retirado do site da Microsoft), a ideia aqui é criar um seletor de caminhos, um exemplo seria você ter dois gets que recebem um id, mas um realmente é um id de inteiro, e o outro é para buscar via nome, mas na URL o campo forma uma rota igual nos 2, exemplo:  
Com int: `https://localhost:7275/produtos/1`  
Com letras: `https://localhost:7275/produtos/abc`   
O campo de ambos fica após produtos, mesmo que no endpoint um esteja escrito ID e um esteja escrito NOME, o sistema não diferencia diretamente, mas por tipo é possível, porém `1` pode ser visto como string, então se for usar tem que ser uma definição que aceite apenas letras, então o sistema vai ver e "opa isso aqui é um numero, e o único get que tem aqui que aceita números é esse; E esse aqui é uma letra, então essa solicitação vai para esse outro get aqui que aceita apenas letras".


Exemplos:  
```c#
// Limita a ser um inteiro
[HttpGet("{id:int}")]

// Limita que seja um inteiro e seu valor mínimo seja 1
[HttpGet("{id:int:min(1)}")]

// Somente letras maiúsculas ou minusculas podem ser inseridos
[HttpGet("{valor:alpha}")]

// Somente letras maiúsculas ou minusculas podem ser inseridos
// e com exatamente 5 dígitos, se for menos de 5 ou
// mais de 5 não funciona
[HttpGet("{valor:alpha:length(5)}")]

// No mínimo 5 dígitos
[HttpGet("{valor:alpha:minlength(5)}")]
// No máximo 5 dígitos
[HttpGet("{valor:alpha:maxlength(5)}")]
```


### Tabela de Referencia de Restrições


| :warning: AVISO :warning:                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Não use restrições para a validação de entrada. Se as restrições forem usadas para validação de entrada, a entrada inválida resultará em uma resposta `404 NotFound`. A entrada inválida deve produzir um `400 Bad Request` com uma mensagem de erro apropriada. ***As restrições de rota são usadas para desfazer a ambiguidade entre rotas semelhantes***, não para validar as entradas de uma rota específica. |
|                                                                                                                                                                                                                                                                                                                                                                                                                   |

**Na minha opinião com base no meu conhecimento atual, em casos como o min(1) onde digitar 0 iria resultar em um 404 NotFound seria válido usar isso.**  

| restrição         | Exemplo                                     | Correspondências de exemplo          | Observações                                                                                                               |
| ----------------- | ------------------------------------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| int               | `{id:int}`                                  | 123456789, -123456789                | Corresponde a qualquer inteiro                                                                                            |
| bool              | `{active:bool}`                             | true, FALSE                          | Correspondências true ou false.                                                                                           | Não diferenciam maiúsculas de minúsculas. |
| datetime          | `{dob:datetime}`                            | 2016-12-31, 2016-12-31 7:32pm        | Corresponde a um valor válido DateTime na cultura invariável. Consulte o aviso anterior.                                  |
| decimal           | `{price:decimal}`                           | 49.99, -1,000.01                     | Corresponde a um valor válido decimal na cultura invariável. Consulte o aviso anterior.                                   |
| double            | `{weight:double}`                           | 1.234, -1,001.01e8                   | Corresponde a um valor válido double na cultura invariável. Consulte o aviso anterior.                                    |
| float             | `{weight:float}`                            | 1.234, -1,001.01e8                   | Corresponde a um valor válido float na cultura invariável. Consulte o aviso anterior.                                     |
| guid              | `{id:guid}`                                 | CD2C1638-1638-72D5-1638-DEADBEEF1638 | Corresponde a um valor Guid válido.                                                                                       |
| long              | `{ticks:long}`                              | 123456789, -123456789                | Corresponde a um valor long válido.                                                                                       |
| minlength(value)  | `{username:minlength(4)}`                   | Rick                                 | A cadeia de caracteres deve ter, no mínimo, 4 caracteres.                                                                 |
| maxlength(value)  | `{filename:maxlength(8)}`                   | MyFile                               | A cadeia de caracteres não pode ser maior que 8 caracteres.                                                               |
| length(length)    | `{filename:length(12)}`                     | somefile.txt                         | A cadeia de caracteres deve ter exatamente 12 caracteres.                                                                 |
| length(min,max)   | `{filename:length(8,16)}`                   | somefile.txt                         | A cadeia de caracteres deve ter, pelo menos, 8 e não mais de 16 caracteres.                                               |
| min(value)        | `{age:min(18)}`                             | 19                                   | O valor inteiro deve ser, pelo menos, 18.                                                                                 |
| max(value)        | `{age:max(120)}`                            | 91                                   | O valor inteiro não deve ser maior que 120.                                                                               |
| range(min,max)    | `{age:range(18,120)}`                       | 91                                   | O valor inteiro deve ser, pelo menos, 18, mas não maior que 120.                                                          |
| alpha             | `{name:alpha}`                              | Rick                                 | A cadeia de caracteres deve consistir em um ou mais caracteres a-z alfabéticos e não diferencia maiúsculas de minúsculas. |
| regex(expression) | `{ssn:regex(^\\d{{3}}-\\d{{2}}-\\d{{4}}$)}` | 123-45-6789                          | A cadeia de caracteres deve corresponder à expressão regular. Confira dicas sobre como definir uma expressão regular.     |
| required          | `{name:required}`                           | Rick                                 | Usado para impor que um valor não parâmetro está presente durante a geração de URL.                                       |

Fonte da tabela: [Roteamento no ASP.NET Core - Microsoft Learn](https://learn.microsoft.com/pt-br/aspnet/core/fundamentals/routing?view=aspnetcore-7.0). (Leitura recomendada, documentação rica em informações interessantes sobre roteamento.)

[Voltar ao Índice](#índice)

---

## Tipos de retorno de ação

Existem alguns tipos de retornos para os métodos actions, como por exemplo:

### Tipo Especifico

Esse tipo de retorno pode ser complexo ou primitivo (int, string, decimal...).
Usando um tipo especifico você perde um pouco de versatilidade, pois ele só retorna o tipo, não permite retornar um Status Code por exemplo.

### IActionResult

IActionResult é um tipo de retorno que permite retornar vários tipos diferentes, desde que estejam dentro de algum Status Code, exemplo:

```c#
[HttpGet]
public IActionResult Get()
{
    var produto = _context.Produtos.FirstOrDefault();
    if(produto == null)
    {
        return NotFound();
    }
    return Ok(produto);
}
```


### `ActionResult<T>`

A classe abstrata ActionResult implementa a interface IActionResult, como resultado, tudo oque a IActionResult faz a ActionResult também faz e com alguns adicionais.  
Se for usar ActionResult sem o tipo, creio ser melhor usar a IActionResult, é para ser mais otimizado.  
Se for retornar o tipo, a `ActionResult<Tipo>` é o ideal, pois com ela você pode retornar assim:  
```c#
[HttpGet]
public ActionResult<Produto> Get()
{
    var produto = _context.Produtos.FirstOrDefault();
    if(produto == null)
    {
        return NotFound();
    }
    return produto;
}
```

A titulo de comparação, antes da ASP.Net Core 2.1 não tinha o ActionResult, então para retornar só o objeto usando o IActionResult, era retornado da seguinte forma: 
```c#
return new ObjectResult(produto);
```


Mais informações em: [Tipos de retorno de ação do controlador na API Web do ASP.NET Core - Microsoft Learn](https://learn.microsoft.com/pt-br/aspnet/core/web-api/action-return-types?view=aspnetcore-7.0)

[Voltar ao Índice](#índice)

---

## Model Binding

O Model Binding (Vinculação de Modelos) é um recurso que nos permite mapear dados de uma requisição HTTP para os parâmetros de uma Action de um controlador.

Esse mapeamento inclui todos os tipos de parâmetros: números, strings, arrays, listas, tipos complexos, listas de objetos, etc.

**Fonte de dados**

1. Valores de Formulários: (Post e Put) enviados no corpo do request.
2. Rotas: `[Route("api/[Controller]")]` ou `[HttpGet("{id}")]`. Verifique: [Rotas/Endpoints](#rotas--endpoints)
3. QueryStrings: `api/produtos/4?nome=Suco&ativo=true`


### QueryStrings

QueryStrings são dados passados direto na uri após uma interrogação, exemplo:  
neste link:  
`https://localhost:7275/Produtos/1?nome=Suco&gelado=true`  
a Query String é: `?nome=Suco&gelado=true`  
Nela temos o parâmetro nome e o parâmetro gelado sendo informados.  
O `&` serve para concatenar os parâmetros.

### Valores de Formulários

São valores recebidos no corpo do request, são usados para receber dados do tipo complexo, geralmente usado com Post e/ou Put.

### Atributos para definir de onde é a fonte dos dados

`[FromBody]` - Usando esse atributo você especifica que a propriedade vai pegar aquele atributo através do corpo do request.

Exemplo:
```c#
[HttpPost]
public ActionResult Put(int id, [FromBody] Produto produto)
{}
```
O id vai vim pela rota e o json do produto vai vir pelo corpo do request.

`[BindRequired]` - Usando esse atributo exige que o atributo seja informado, se não for ele vai retornar um erro 400.

Exemplo:
```c#
[HttpPost]
public ActionResult Put(int id, [BindRequired] string nome)
{}
```

`[BindNever]` - Informa ao Model Binder para não vincular informação ao parâmetro. É usado na Model/Entidade.  

Exemplo:
```c#
public class Categoria
{
    public int CategoriaId { get; set; }
    public string Nome { get; set; }
    
    [BindNever]
    public string ImagemUrl { get; set; }
}
```
Dessa forma o model binder vai ignorar a vinculação dessa propriedade, ou não permitir.

- `[FromForm]` - Utilize somente os dados recebidos do **formulário** enviado.
- `[FromRoute]` - Vincula apenas os dados que são oriundos da **rota de dados**.
- `[FromQuery]` - Recebe apenas os dados da cadeia de consulta (**QueryString**).
- `[FromHeader]` - Vincula os valores que vêm no **cabeçalho** da requisição HTTP.
- `[FromServices]` - Vincula o valor especificado à implementação que foi configurada no seu **container de injeção de dependência**.

Leitura adicional: [Model binding no ASP.NET Core - Microsoft Learn](https://learn.microsoft.com/pt-br/aspnet/core/mvc/models/model-binding?view=aspnetcore-7.0)

### [FromServices]

O atributo from services basicamente permite que você instancie um objeto que ja esteja carregado no services do program.cs.

Você precisa ter uma interface para ele e sua classe com sua função.  
Por exemplo, imagine um código de mensagem de saudação que irá receber o nome da pessoa.  
No program.cs você coloca a seguinte linha de comando: 
```c#
services.AddTransient<IMeuServico, MeuServico>()  
```
Ou seja, aqui você definiu um serviço, que será Transient que significa que ele irá criar uma nova instancia do serviço toda vez que você chama-lo (existe também scooped e singleton), e definiu com a interface e a classe qual serviço é.  
Mais sobre Scooped, Singleton e Transient em: [Serviço Scooped, Singleton e Transient](#serviço-scooped-singleton-e-transient)

E na controladora você coloca:
```c#
[HttpGet("saudacao/{nome}")]
public ActionResult<string> GetSaudacao([FromServices] IMeuServico meuServico, string nome)
{
  return meuServico.Saudacao(nome);
}
```
Você coloca o atributo FromServices e chama o objeto pela interface.  

Na realidade sua real utilidade segundo a documentação da microsoft é para injeção de dependência que exige construtor, um exemplo seria o _context do EFCore, onde você cria um readonly do _context, e no construtor carrega ele. Mas ai você tem algo que so vai usar uma vez ou poucas vezes que não compensa carregar junto da controladora, ou então é algum serviço de configuração que você pode usar o singleton que carrega ele apenas uma vez e só mata a instancia quando fechar o programa, assim você cria ele por fora la na program, com o tipo de inicialização de instancia que você precisar e usa.  
Mais sobre Scooped, Singleton e Transient em: [Serviço Scooped, Singleton e Transient](#serviço-scooped-singleton-e-transient)

Um pouquinho sobre FromServices no final da pagina: [Model binding no ASP.NET Core - Microsoft Learn](https://learn.microsoft.com/pt-br/aspnet/core/mvc/models/model-binding?view=aspnetcore-7.0)

### Atribuição automática

A partir do ASP.Net Core 2.2, ao colocar o atributo `[ApiController]` na classe controladora fica automático algumas atribuições, como por exemplo, o `[FromBody]` para tipos complexos.

---
O atributo [ApiController] aplica regras de inferência para as fontes de dados padrão dos parâmetros de ação. Essas regras poupam você da necessidade de identificar as origens de associação manualmente aplicando atributos aos parâmetros de ação. As regras de inferência da origem de associação se comportam da seguinte maneira: 

 - [FromServices] é inferido para parâmetros de tipo complexos registrados no Contêiner de DI.
- [FromBody] é inferido para parâmetros de tipo complexos não registrados no Contêiner de DI. Uma exceção à regra de inferência [FromBody] é qualquer tipo interno complexo com um significado especial, como IFormCollection e CancellationToken. O código de inferência da origem da associação ignora esses tipos especiais.
- [FromForm] é inferido para parâmetros de ação do tipo IFormFile e IFormFileCollection. Ele não é inferido para qualquer tipo simples ou definido pelo usuário.
- [FromRoute] é inferido para qualquer nome de parâmetro de ação correspondente a um parâmetro no modelo de rota. Quando mais de uma rota correspondem a um parâmetro de ação, qualquer valor de rota é considerado [FromRoute].
- [FromQuery] é inferido para todos os outros parâmetros de ação. 
---
O trecho acima foi retirado de: [Criar APIs Web com o ASP.NET Core - Microsoft Learn](https://learn.microsoft.com/pt-br/aspnet/core/web-api/?view=aspnetcore-7.0) 

Outro recurso que a ApiController oferece é verificar automaticamente o estado do modelo e retornar respostas HTTP 400 em caso de erros de validação do modelo.

Portanto, não precisamos verificar o modelo usando `ModelState.IsValid` explicitamente em nossas Actions nas Web APIs nem usar explicitamente [FromBody] graças ao atributo [ApiController].

Leitura adicional em ingles (é o mesmo do link acima, mas achei que explicação está um pouco melhor):   
[Create web APIs with ASP.NET Core - Microsoft Learn](https://learn.microsoft.com/en-us/aspnet/core/web-api/?view=aspnetcore-7.0)

[Voltar ao Índice](#índice)

---

## Métodos Assíncronos

Nos métodos **SÍNCRONOS** quando uma solicitação chega ao servidor, ele consome uma "task" é processado, e devolvido, e só então libera esse slot de task.  
Nos métodos **ASSÍNCRONOS** a solicitação chega, entra em uma task, começa a ser processado, o sistema devolve o slot de task para poder receber outras solicitações, e quando a primeira solicitação for concluída o sistema revisa e devolve a solicitação.  
Em resumo, métodos síncronos são sequenciais, que só libera a action para outra solicitação após concluir a primeira, e os assíncronos não são sequenciais, o servidor vai recebendo e processando tudo e conforme for terminando ele devolve.

Para um método ser assíncrono, é necessário utilizar as palavras `Task`, `async` e `await`, exemplo:
```c#
[HttpGet]
public async Task<ActionResult<IEnumerable<Categoria>>> GetCategoriasAsync()
{
    return await _context.Categorias.ToListAsync();
}
```
Não é necessário terminar o nome do método com Async, mas é uma boa pratica para informar que é assíncrono.  
ToList também precisa ser Async para funcionar corretamente.  
Todo método usado dentro de uma action async é bom conferir se tem versão async, por exemplo o `FirstOrDefault`, ele tem a versão `FirstOrDefaultAsync` e ela deve ser usada.

- A instrução `async` faz com que um método possa ser executado de forma assíncrona.
- A palavra reservada `await` indica que um treco de código deve esperar por outro trecho de código para o controle retornar ao chamador do método.
- A classe `Task<TResult>` representa uma **única operação** que **retorna** um valor, e essa **operação** pode ser executada de forma **assíncrona**.

### Vale a pena usar Actions Assíncronas?
"O assincronismo é útil para melhorar a experiência do usuário quando há alguma operação que demanda muito tempo para ser executada."  

**Pontos a serem avaliados:**
- O assincronismo não é grátis.
- Sempre que usá-lo terá uma perda de desempenho, especialmente se usar thread.
- O ganho que ele dá é a execução em paralelo, assim você pode atender mais requisições.
- A requisição especifica não ficará mais rápida em hipótese alguma.
- Então tenha certeza que haverá algum ganho antes de usar este recurso.

**Se justifica usar métodos async quando é uma solicitação que não depende somente da nossa aplicação, como por exemplo acessar um banco de dados.**

Fonte: [Curso Web API ASP.NET Core Essencial (.NET6) - Macoratti](https://www.udemy.com/course/curso-web-api-asp-net-core-essencial/)

Leitura recomendada: [Programação assíncrona com async e await (C#) - Microsoft Learn](https://learn.microsoft.com/pt-br/dotnet/csharp/programming-guide/concepts/async/)

[Voltar ao Índice](#índice)

---

## Informações interessantes  

### Serviço Scooped, Singleton e Transient

Transient: Cria uma nova instância do serviço, toda vez que você o solicita. Em um mesmo request se você solicitar o serviço mais de uma vez , para cada vez uma nova instância será criada.

Scoped: Cria uma nova instância para cada escopo. (Cada request é um escopo). Dentro do escopo, ele reutiliza o serviço existente. Em um mesmo request se você solicitar o serviço mais de uma vez somente será criar uma instância do serviço e reusada dentro do request.

Singleton: Cria um novo serviço apenas uma vez durante o tempo de vida do aplicativo e o usa em todos os lugares. Assim essa instância será usada em todos os request e será criada apenas uma vez no início e encerrada quando o processamento terminar

É mais seguro criar serviços Transients, pois você sempre obtém a nova instância. Mas, como o sistema de injeção de dependência vai criar os serviços toda vez, eles usarão mais memória e recursos e podem ter um impacto negativo no desempenho se você usar muitos serviços neste tempo de vida.

A recomendação e usar serviços Transient para serviços leves com pouco ou nenhum estado.

Os serviços com tempo de vida Scoped são a melhor opção quando você deseja manter o estado dentro de um request. E são indicados para a maioria dos serviços usados em aplicações web.

Um uso comum de Scoped seria para  qualquer lógica de banco de dados implementando classes, uma vez que uma conexão pode ser permitida em um request. A classe DbContext do EF Core geralmente usa este tempo de vida.

Singletons são criados apenas uma vez e não são destruídos até o final do aplicativo. Qualquer vazamento de memória nesses serviços aumentará com o tempo. Singletons também são eficientes em termos de memória, pois são criados depois de reutilizados em todos os lugares.

Use Singletons onde for necessário manter o estado geral do aplicativo e para tratar tarefas como:  Configuração ou parâmetros do aplicativo, serviço de registro, armazenamento em cache de dados são alguns dos exemplos em que você pode usar singletons.

[Voltar ao Índice](#índice)

---

## Soluções de problemas

### Problema de Serialização CÍCLICA  

Acontece as vezes da entidade ter referencia a outra entidade (para fazer chave estrangeira por exemplo), e isso pode acarretar em um loop.
Por exemplo, a classe Categorias referencia a classe Produtos que por sua vez referencia Categorias de volta. E quando você coloca no método Get um include() para pegar por exemplo os produtos daquela categoria, ele vai criar esse loop e dar um erro.

Para resolver isso, na classe program, adicione esses métodos em AddControllers():
```c#
builder.Services.AddControllers()
    .AddJsonOptions(options =>
        options.JsonSerializerOptions
            .ReferenceHandler = ReferenceHandler.IgnoreCycles);
```
Isso vai resolver o problema.

Fonte: Curso WebAPI AspNet Core do Macoratti.

[Voltar ao Índice](#índice)

---

## Otimizando o código

### HTTP GET

Quando consultamos entidades usando o entity framework ele armazena as entidades no contexto (em cache) realizando um tracking ou rastreamento das entidades para acompanhar o estado das entidades.

Este recurso **adiciona uma sobrecarga** que afeta o desempenho das consultas rastreadas.

Para melhorar o desempenho podemos usar o método: `AsNoTracking()`

```c#
var produtos = _context.Produtos.AsNoTracking().ToList();
```

**OBS: Usar `AsNoTracking()` APENAS para consultas somente leitura SEM a necessidade de alterar os dados.**

#### Dicas:

- Nunca retorne todos os registros em uma consulta!  
Exemplo de solução: Limite para pegar so alguns dados.  
```c#
_context.Produtos.Take(10).ToList();
```
*Obs: Em produção pode e deve ser aprimorado para paginação.*

--

- Nunca retorne objetos relacionados sem aplicar um filtro!  
Exemplo de solução: Usar where para limitar por id.  
```c#
_context.Categorias.Include(p => p.Produtos)
    .Where(c => c.CategoriaId <= 5).ToList();
```
*Obs: Em produção pode e deve ser aprimorado para paginação.*

[Voltar ao Índice](#índice)

---


