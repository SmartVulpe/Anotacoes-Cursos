
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

### Oque acontece se colocar uma barra no inicio do endpoint da action?

Se colocar uma barra no endpoint da action, ele ignora a rota que está no atributo Route que está no cabeçalho da classe do controlador.
```c#
[HttpGet("/primeiro")]
```
A URL fica assim: `https://localhost:7275/primeiro`  
Mesmo que na rota da classe tenha mais coisas, exemplo: `Route("[sistema/v2/api/Controller]")` ele vai ignorar toda essa rota e fazer como no exemplo acima.  

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


| :warning: AVISO :warning:                                                                                                                                                                                                                                                                                                                                                                                                          |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Não use restrições para a validação de entrada. Se as restrições forem usadas para validação de entrada, a entrada inválida resultará em uma resposta `404 NotFound`. A entrada inválida deve produzir um `400 Bad Request` com uma mensagem de erro apropriada. ***As restrições de rota são usadas para desfazer a ambiguidade entre rotas semelhantes***, não para validar as entradas de uma rota específica. |
|                                                                                                                                                                                                                                                                                                                                                                                                                         |

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

#### **Dicas:**

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


---


