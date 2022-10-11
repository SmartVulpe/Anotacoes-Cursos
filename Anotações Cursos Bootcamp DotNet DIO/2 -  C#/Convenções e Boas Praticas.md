# Convenções

## Convenções de nomes:

- camelCase = primeira palavra tudo minuscula e as seguintes com a primeira letra maiúscula. 
- PascalCase = cada palavra tem a primeira letra maiúscula.
- snake_case = tudo minusculo e separa as palavras com underline.
- spinal-case = tudo minusculo e separa as palavras com traço.

Os padrões usados no C#/.net são **camelCase** e o **PascalCase**.

- PascalCase nas situações: 
  - Nomes de Classes.
  - Assembly.
  - Structs.
  - Interfaces (sempre com o I antes dos nomes, exemplo: IControle).
  - Delegates.
  - Enums.
  - Métodos.
  - Propriedades.
  - Campos públicos.
  - Eventos.  
<br>
- camelCase nas situações:
  - Variáveis locais
  - Parâmetros de métodos
  - Campos privados
  - Campos protegidos.  

Fonte adicional com recomendações de escritas e diversas informações interessantes de boas práticas (leitura extremamente recomendada):  
[Padrão de nomenclatura no código para o C# - StackOverflow](https://pt.stackoverflow.com/questions/31646/padr%C3%A3o-de-nomenclatura-no-c%C3%B3digo-para-o-c)

## Dicas:

- Evite abreviar nomes, pois nem sempre será você que irá dar manutenção no código e ele tem que ser o mais entendível possível.

- O nome do arquivo e o nome da classe deve ser o mesmo, pode ser diferente, mas por convenção deve ser o mesmo para facilitar encontrar.  
<br>

## Convenções de Projetos

Por convenção projetos adicionais que são adicionados a uma solution geralmente têm o mesmo nome de base e um sufixo para indicar sua finalidade. É comum ver projetos em solutions com nomes como:
```c#
MeuProjeto.Web
MeuProjeto.Api
MeuProjeto.BackOffice
MeuProjeto.Common
MeuProjeto.Core
MeuProjeto.Client
MeuProjeto.Communication
MeuProjeto.Proxy
MeuProjeto.Migrate
MeuProjeto.Test
MeuProjeto.NET5
MeuProjeto.NET6
```

# Boas Práticas de Códigos


- Deve-se representar valores monetários utilizando o tipo **Decimal**, ele é mais preciso para operações monetárias evitando qualquer falha critica causada por arredondamento, além de não necessitar formatação adicional na hora de mostrar o valor, pois já entrega mostrando 2 números após a vírgula.
Mais detalhes em:   
[.Net - Float(Single), Double e Decimal. Afinal qual devo usar ?](https://www.macoratti.net/12/12/c_num1.htm)

