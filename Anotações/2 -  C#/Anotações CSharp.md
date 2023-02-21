# Minhas anotações sobre CSharp  

## Índice
- [Minhas anotações sobre CSharp](#minhas-anotações-sobre-csharp)
  - [Índice](#índice)
- [Base do CSharp](#base-do-csharp)
  - [Namespace](#namespace)
  - [Declaração de variáveis](#declaração-de-variáveis)
    - [Tipos de Valor](#tipos-de-valor)
    - [Tipos de referencia](#tipos-de-referencia)
    - [Declaração de variáveis na mesma linha](#declaração-de-variáveis-na-mesma-linha)
  - [Concatenação e Interpolação](#concatenação-e-interpolação)
  - [Classes](#classes)
  - [Objetos](#objetos)
  - [Qual a diferença entre método, procedimento e função?](#qual-a-diferença-entre-método-procedimento-e-função)
  - [Atributos](#atributos)
  - [Campos e Propriedades](#campos-e-propriedades)
  - [Argumentos e Parâmetros](#argumentos-e-parâmetros)
  - [Get e Set](#get-e-set)
  - [Overload de Métodos](#overload-de-métodos)
  - [Operadores Ternários](#operadores-ternários)
  - [Encapsulamento](#encapsulamento)
  - [Modificadores de acesso (public / private / protected)](#modificadores-de-acesso-public--private--protected)
  - [Construtor](#construtor)
    - [Construtor Estático](#construtor-estático)
  - [This](#this)
  - [Variáveis e Métodos ESTÁTICOS](#variáveis-e-métodos-estáticos)
  - [Herança](#herança)
  - [Polimorfismo](#polimorfismo)
  - [Classe Abstrata](#classe-abstrata)
  - [Classes e Métodos Selados](#classes-e-métodos-selados)
  - [Classe object](#classe-object)
  - [Interface (*não é interface gráfica*)](#interface-não-é-interface-gráfica)
- [Teórico](#teórico)
  - [Alocação de Memória](#alocação-de-memória)
  - [Limpeza de memória](#limpeza-de-memória)
  - [Tipos de valor (Teórico)](#tipos-de-valor-teórico)
  - [Tipos de referência (Teórico)](#tipos-de-referência-teórico)
- [Outras informações](#outras-informações)
  - [Conversão de tipos](#conversão-de-tipos)
  - [Listas](#listas)
  - [Summary](#summary)
  - [Definindo uma região e formatando estilo monetário](#definindo-uma-região-e-formatando-estilo-monetário)
    - [Formatações manuais](#formatações-manuais)
  - [Serialização](#serialização)
  - [Tuplas](#tuplas)
  - [Desconstrutor](#desconstrutor)
  - [Tipos Especiais](#tipos-especiais)
    - [Tipos Anuláveis](#tipos-anuláveis)
    - [Tipos Anônimos](#tipos-anônimos)
    - [Tipo Dinâmico](#tipo-dinâmico)
  - [Classes Genéricas](#classes-genéricas)
  - [Métodos de Extensão](#métodos-de-extensão)
  - [Instrução Using (Objeto descartável)](#instrução-using-objeto-descartável)
- [Dicas](#dicas)
  - [Palavras Reservadas](#palavras-reservadas)
  - [Carregando uma variável numérica com valor máximo](#carregando-uma-variável-numérica-com-valor-máximo)
  - [IF sem comparador](#if-sem-comparador)
  - [Uso diferenciado do switch-case](#uso-diferenciado-do-switch-case)
  - [Quebrando laços de repetição antes do fim](#quebrando-laços-de-repetição-antes-do-fim)
  - ["Alterando" o tamanho de um Array](#alterando-o-tamanho-de-um-array)
  - [Copiando Arrays](#copiando-arrays)
  - [Tratamento Get e Set simples usando =\>](#tratamento-get-e-set-simples-usando-)
  - [Usando o nome dos parâmetros ao passar os argumentos](#usando-o-nome-dos-parâmetros-ao-passar-os-argumentos)
  - [Botou um valor decimal float ou double e não funcionou?](#botou-um-valor-decimal-float-ou-double-e-não-funcionou)
  - [Links para leitura sobre Design Patterns](#links-para-leitura-sobre-design-patterns)

</br>

---

# Base do CSharp

## Namespace 

O namespace indica qual o nome da pastinha que o Arquivo.cs pertence, da para ter vários repetidos desde que sejam de pastinhas diferentes.  
Obviamente que se você der using em mais de uma pasta com um arquivo de mesmo nome você terá que detalhar mais na hora de instanciar botando o caminho da pasta junto, senão irá dar conflito.

[Voltar ao Índice](#índice)

---  

## Declaração de variáveis

### Tipos de Valor

São valores primitivos, que armazenam o valor diretamente, vide: [Tipos de Valor (Teórico)](#tipos-de-valor-teórico)  

Tabela com os tipos de valor:
![Tabela dos tipos de valor](imgs/Tabela-tipos-de-valor.png)  
Nesta tabela tem muitos tipos raros de serem utilizados, dela normalmente você irá utilizar apenas: bool, decimal, double, e int.

Note que nesta tabela não tem string! Pois ela é um tipo de referencia.

--

### Tipos de referencia

São valores mais complexos que na area primitiva da memoria (memoria Stack) ele apenas tem o caminho de referencia para outro local da memoria (memoria heap) que ficam armazenados dados mais complexos que contem múltiplas variáveis primitivas dentre outras coisas, vide: [Tipos de Referencia (Teórico)](#tipos-de-referência-teórico)

Destes temos:
- Os objetos, vide: [Objetos](#objetos);
- As **strings**;
- E o DYNAMIC, vide: [Tipo Dinâmico](#tipo-dinâmico);

Fonte, créditos da imagem e Leitura adicional recomendada: [CSharp data types - Tutorials Point](https://www.tutorialspoint.com/csharp/csharp_data_types.htm)

--

### Declaração de variáveis na mesma linha

É possível declarar várias variáveis do mesmo tipo na mesma linha, exemplo:  
```c#
public double largura, altura, comprimento;
```  

[Voltar ao Índice](#índice)

---  

## Concatenação e Interpolação

A forma mais comum de concatenar textos com dados é essa:
```c#
Console.WriteLine("Meu nome é " + nome + " e minha idade é " + idade + " anos");
```
Mas a partir do C# 6 (para referencia o .NET6 usa o C# 10) é possível **interpolar** textos, em outras palavras, é uma forma diferente de concatenar, utiliza um cifrão antes das aspas e chaves entre os dados de variáveis, exemplo:
```c#
Console.WriteLine($"Meu nome é {nome} e minha idade é {idade} anos");
```

Também é possível executar operações simples dentro das chaves, como um operador ternário.
```c#
Console.WriteLine($"Eu tenho {numeroCarros} {(numeroCarros > 1 ? "carros" : "carro")}");
```
Obs: o operador ternário tem que estar dentro de parenteses.

Leitura adicional: [String Interpolation - Microsoft Learn](https://learn.microsoft.com/pt-br/dotnet/csharp/tutorials/string-interpolation)

[Voltar ao Índice](#índice)

---

## Classes 

Uma classe é uma **abstração** de algo que você quer representar, em outras palavras é como um molde, que irá conter as características (as variáveis) de uma pessoa por exemplo, e métodos para executar uma ação referente a essa classe.  

- Toda classe começa com letra maiúscula (padrão universal de boas praticas de orientação a objetos).

[Voltar ao Índice](#índice)

---  

## Objetos  
  
Um objeto é uma especie de variável que armazena uma classe.

Para instanciar (chamar/carregar para outro arquivo exemplo o arquivo Pessoa.cs para dentro do Program.cs) tem que fazer dessa forma:

```c#
Pessoa obj = new Pessoa();
```

Então a pessoa vai se chamar "obj" dentro do arquivo Program.cs e você vai poder usar ela dessa forma:

```c#
obj.idade = 27;
obj.nome = Nayala;
obj.mensagemBonita();
```

PS: Da pra instanciar vários objetos da mesma classe, literalmente igual variáveis, só dar outro nome ao objeto que no caso desse exemplo é a palavra "obj".

[Voltar ao Índice](#índice)

---

## Qual a diferença entre método, procedimento e função?    

**Procedimento**: Parte de um programa ou classe que não retorna um valor (da definição de Delphi/Pascal). No Visual Basic/VB.NET, também é conhecimento como Subroutine (Sub-rotina, ou simplesmente Sub).

**Função**: Parte de um programa ou classe que retorna um valor (da definição de Delphi/Pascal/Visual Basic/Visual Basic .NET).  

**Método**: Procedimento ou função pertencente a uma classe (várias linguagens de programação definem desta forma, por exemplo, c++, c#, java, etc.).  

[Voltar ao Índice](#índice)

---

## Atributos

"O conceito de atributos pode parecer simples mas muita gente confunde atributos com propriedades de classes ou métodos.  

Mas afinal o que é um atributo na linguagem C# ?  

Os Atributos são um mecanismo para a adição/associação de metadados, tais como instruções do compilador e outros dados sobre seus assemblies, tipos, métodos, propriedades, etc."  

"Os atributos podem ser colocados em praticamente qualquer declaração, embora um atributo específico possa restringir os tipos de declarações nas quais ele é válido. Na linguagem C#, você especifica um atributo colocando o nome do atributo entre colchetes ([ ]) acima da declaração da entidade à qual ele se aplica."     
Explicação retirada de: [Apresentando Atributos - Macoratti](https://www.macoratti.net/18/04/c_atrib1.htm)  

**Exemplos práticos de uso de atributos:**    
Retirados de: [Atributos - Microsoft Learn](https://learn.microsoft.com/pt-br/dotnet/csharp/programming-guide/concepts/attributes/)   
**Obs: Tudo oque tiver entre colchetes [] é um Atributo.**  

```c#
[System.Serializable]  
public class SampleClass  
{
} 

void MethodA([In][Out] ref double x) { }
void MethodB([Out][In] ref double x) { }
void MethodC([In, Out] ref double x) { }

[Conditional("DEBUG"), Conditional("TEST1")]
void TraceMethod()
{
}

// default: applies to method
[ValidatedContract]
int Method1() { return 0; }

// applies to method
[method: ValidatedContract]
int Method2() { return 0; }

// applies to parameter
int Method3([ValidatedContract] string contract) { return 0; }

// applies to return value
[return: ValidatedContract]
int Method4() { return 0; }

```

Fontes e leituras recomendadas:  
[Apresentando Atributos - Macoratti](https://www.macoratti.net/18/04/c_atrib1.htm)  
[Atributos - Microsoft Learn](https://learn.microsoft.com/pt-br/dotnet/csharp/programming-guide/concepts/attributes/)

[Voltar ao Índice](#índice)

---  

## Campos e Propriedades

**Campos** são as variáveis que serão utilizadas para trabalho dentro da própria classe, apesar de poderem ser definidas como publicas a boa pratica diz que o ideal é mantê-las privadas.  
**São escritas em camelCase.**

**Propriedades** são variáveis que serão utilizadas para entrada e saída de dados da classe, elas são acompanhadas de get e set, e normalmente utilizadas para carregar ou transmitir o dado de um **campo** sem que ele seja exposto.  
**São escritas em PascalCase**

**Dica:** se digitar **prop** (abreviação para propriedade) e apertar tab duas vezes ele vai criar automaticamente um modelo de propriedade para você.

Mais detalhes sobre get e set na sessão sobre [Get e Set](#get-e-set)

Fonte e leitura recomendada: [Diferença entre Campos(Fields) e Propriedades(Properties) - Macoratti](https://www.macoratti.net/17/01/c_camprop1.htm)  

[Voltar ao Índice](#índice)

---

## Argumentos e Parâmetros

Um **Parâmetro** é aquela variável que fica dentro do parenteses () do método. **E é escrita em PascalCase.**    
Um **Argumento** é o valor que o parâmetro vai receber.  

```c#
// O parâmetro fica no método  
public void MetodoExemplo(string EssaVariavelEUmParametro)
{
}

// O argumento fica no uso do método  
MetodoExemplo("Argumento é o valor");
```

Fonte: [Argumentos nomeados - Macoratti](https://www.macoratti.net/15/07/c_parnome1.htm)

Leitura adicional para parâmetros adicionais: [Parâmetros Opcionais - Macoratti](https://www.macoratti.net/15/07/c_paraop1.htm)

[Voltar ao Índice](#índice)

---

## Get e Set

**Get** e **Set** é uma técnica para ler e escrever em uma propriedade, você pode permitir apenas leitura (Get) ou apenas escrita (Set), ou ambos, essa técnica melhora a segurança do projeto principalmente quando utilizada com variáveis privadas (Vide Encapsulamento).

Exemplo de uso:  
```c#
    private string nome;

    public string Nome
    {
        get { return nome; }

        set { nome = value; }
    }
```

As boas práticas dizem que quando usada com variáveis privadas o método get/set deve ter o mesmo nome que a variável, mas com a primeira letra em maiúscula.

Também é possível criar códigos para tratamentos de entrada ou saída dentro das chaves.

[Voltar ao Índice](#índice)

---

## Overload de Métodos  
  
É possível usar o MESMO MÉTODO para mais de uma ação ao mesmo tempo DESDE QUE ELES TENHAM PARÂMETROS DIFERENTES.
Exemplo:

public void apresentar()
{}

public void apresentar(string nome)
{}

public void apresentar(string nome, int idade)
{}

***ESSES 3 PODEM EXISTIR SIMULTANEAMENTE***  
O software vai saber qual você está usando conforme oque você preencher nos parâmetros.  
Exemplo:  
Se não preencher nada ele vai executar o primeiro:  
**apresentar();**    

Se colocar uma string, ele vai executar o segundo:  
**apresentar("Daniel");**   

Se colocar uma string E um int, ele vai executar o terceiro:    
**apresentar("Daniel", 20);**  

E na hora que for escrever esse método ele vai mostrar na janelinha que aparece de auto-completar que tem 2 overloads (nesse caso do apresentar), que é a primeira opção e mais as 2 extras, totalizando 3 opções de uso do mesmo método.  

[Voltar ao Índice](#índice)

---

## Operadores Ternários

São como IFs, mas mais simples e limitados, muito úteis para comparações com resultados simples (apenas um true ou false, ou só retornar um texto ou um valor fixo que não exige ser calculado conforme comparação seja verdadeira ou falsa), exemplo:  
```c#
situacao = media >= 7 ? "aprovado" : "reprovado";  
```
Ou seja, a variável string **situacao** recebe aprovado caso a media for **maior ou igual a 7**, ou reprovado caso não.  

[Voltar ao Índice](#índice)

---  

## Encapsulamento

Serve para proteger os dados de uma classe expondo somente o necessário.

Ou seja você vai ter os métodos e variáveis, que só a classe vai utilizar internamente em seus métodos, **como privados ou protected**, assim eles não aparecerão no objeto. Somente oque é para ser usado fora vai aparecer.  
Isso aumenta a segurança do projeto além de deixar mais limpo na hora de usar o objeto.   
Vide **Modificadores de Acesso** logo abaixo.

[Voltar ao Índice](#índice)

---

## Modificadores de acesso (public / private / protected)

Modificadores de acesso são a maneira que você tem de visualizar um método ou variável.  

public    -> Variáveis e métodos visíveis em qualquer classe.  
private   -> Variáveis e métodos visíveis apenas na classe onde são criados.  
protected -> Variáveis e métodos visíveis em classes onde são criados ou herdados.  

[Voltar ao Índice](#índice)

---

## Construtor  

O **Construtor** é um **método** que é executado **no momento que o objeto é instanciado.**  

Ele tem que ter o mesmo nome da classe.  

Toda vez que instanciar um objeto exemplo:  
```c#
Pessoa p = new Pessoa() ; 
```
O programa vai executar o construtor que nesse exemplo será:  
```c#
Public Pessoa()
{}   
```
Dentro do arquivo Pessoa.cs  

***Assim como os métodos da pra ter mais de um construtor usando parâmetros diferentes.***

**Dica:** se digitar **ctor** (abreviação para construtor) e apertar tab duas vezes ele vai criar automaticamente um modelo de construtor para você.

[Voltar ao Índice](#índice)

### Construtor Estático

Construtores Estáticos são usados para inicializar dados estáticos, ele é chamado automaticamente antes que a primeira instancia seja criada.

Exemplo de um construtor estático:
```c#
static CategoriasUnitTestController()
{
    dbContextOption = new DbContextOptionsBuilder<CatalogoAPIContext>()
        .UseSqlServer(connectionString)
        .Options;
}
```

[Voltar ao Índice](#índice)

--- 

## This

**This** serve para forçar pegar o valor do campo (variável), ao invés de um valor que veio por um **parâmetro** de mesmo nome, exemplo:

La no arquivo main o objeto que contem esse código está setando para nome: 
```c#
Pessoa("Nayala");        

// Campo / Variável
private string nome = "Daniel";

public Pessoa(string nome)
{
    //Detalhe: Ambos campo e parâmetro tem o mesmo nome

    //Sem o this ele pega o valor do parâmetro
    Console.WriteLine(nome);

    //Com o this ele pega o valor do campo
    Console.WriteLine(this.nome);
}
```

No console vai aparecer:  
```
Nayala  
Daniel  
```

Ou seja, como o primeiro estava sem o **this** ele pegou o que foi setado para o campo, e o segundo que tinha o **this** ele pegou o que tava na variável nome.

[Voltar ao Índice](#índice)

---

## Variáveis e Métodos ESTÁTICOS

São variáveis e métodos que podem ser acessados **sem precisar instanciar** um objeto.  
Exemplo:  
No arquivo de classe **Exemplo.cs** vai estar assim:

```c# 
public static string nome = "Nayala";
public static void soma(int n1, int n2){}
```

E no arquivo **Program.cs** da pra chamar eles só de fazer assim:

```c# 
Exemplo.soma(3, 7);
Console.WriteLine("Olá " + Exemplo.nome);
```

[Voltar ao Índice](#índice)

---

## Herança

Uma classe pode herdar o conteúdo de outra classe como se fosse dela.
Todo conteúdo publico ou **protected** pode ser usado sem precisar instanciar objeto.  
Conteúdo **PRIVADO** não é herdado.  

**Forma de ativar a herança:**  
Basta por "2 pontos" após o nome da classe e inserir o nome da classe que você quer "estender".  
Exemplo:  

```c#
class Colaborador : Pessoa  
{}  
```

Desse modo a classe Colaborador vai herdar os conteúdos de Pessoa QUE NÃO FOREM PRIVADOS.  

**Detalhe:**  
No C# não existe herança múltipla!  
exemplo:
```c#   
class Colaborador : Pessoa : Passaro : Peixe  
```
Uma classe só pode estender uma classe! (diretamente)  

**Dica:** Você pode herdar uma classe que herda outra classe que herda outra classe e assim por diante.  
**MAS**, a menos que você tenha um ganho mt bom em algo, procure evitar deixar o código muito complexo assim, pois se houver muitas dependências de heranças, a hora que você editar um dos primeiros, por exemplo remover um método que não faz mais sentido naquela, mas acaba usando em outra la na frente, o código vai quebrar em cascata.  

[Voltar ao Índice](#índice)

---

## Polimorfismo

Existem dois tipos de polimorfismo:  
- O Polimorfismo em tempo de compilação (Overloading/Sobrecarga).  
- O Polimorfismo em tempo de execução (Overriding/Sobrescrita).  

**Explicando o Polimorfismo em tempo de execução:**

Basicamente, uma forma de criar um objeto aproveitando a maior parte de uma classe e sobrescrevendo somente o necessário.  

Funciona da seguinte forma, ao instanciar um objeto, você pode instanciar usando duas classes.  
Exemplo: 
```c#   
Imposto objetoG = new Gerente();
```
**Dessa forma o objeto objetoG vai receber os métodos e variáveis da classe Imposto, E se houver o mesmo método ou variável na classe Gerente, o programa vai sobrescrever os métodos da classe Imposto por esses da classe Gerente.**  

Você pode ter, por exemplo, um método chamado valeTransporte(), e esse método por padrão é de um jeito, mas para o gerente você precisa que tenha 1 valor diferente, ai você cria uma classe com o mesmo método e essa diferença que precisa, ai na hora que instanciar você só precisa instanciar com mescla, não vai precisar ter um valeTransporteGerente() pra se diferenciar do valeTransporte padrão, simplifica e padroniza alguns locais do código exigindo menos alterações, e joga as alterações em outros locais deixando mais organizado e legível.

Além de instanciar usando duas classes diferentes, é necessário que o método tenha o seguinte:
O método que **vai ser sobrescrito** tem que estar assim:  

```c#  
public virtual void valeTransporte(){}  
```
E o método que **vai sobrescrever** tem que estar assim: 

```c#  
public override valeTransporte(){}  
```
*As classes que vão sobrescrever, tem que herdar à que será sobrescrita, senão também não funciona.*  

**Além de haver esse polimorfismo por mesclagem, também da para fazer com simples herança.**  
Exemplo:  
Você tem a classe Professor que herdou a classe Pessoa, na classe pessoa tem Nome e Idade, e um método de se Apresentar(), ai na professor tem o Salario, mas quando você executar o método Apresentar herdado da pessoa você quer que ele se apresente diferente.  
Então la na Pessoa você coloca virtual no método como explicado acima.  
e no método professor você faz um novo método apresentar com o override como explicado acima com as diferenças que você quer.  
**A diferença é que na hora de instanciar voce instancia sem mescla, pois a classe professor ja está herdando de pessoa.**  

```c#  
Professor p1 = new Professor();  
```

--

Leitura adicional recomendada: [Polimorfismo - Macoratti](https://www.macoratti.net/12/06/c_poli1.htm)

[Voltar ao Índice](#índice)

---

## Classe Abstrata

- É uma classe que pode conter métodos obrigatórios para todas as classes que a herdarem.

- É possível criar métodos convencionais (não obrigatórios), para que as classes que herdem consigam utilizar.

- **Não** é possível instanciar uma classe abstrata, exemplo: `Produto prod = new Produto();`  

- Padrão utilizado em projetos com muitos desenvolvedores, pois garante uma estrutura pré-moldada com ações que podem ser realizadas.

- Como é utilizada a herança, cada classe pode herdar apenas uma classe abstrata:  

class Produto : PadraoProduto > Ok  
class Produtop : PadraoProduto, CalculoImpostos > Falha  

Exemplo:  

Para usar precisa que a classe que vai ser o padrão esteja com abstract, e o método que for obrigatório também:  

```c#
abstract class Padrao
{

    // Método Obrigatório
    public abstract void taxaEmprestimo(double valor);

    // Opcional

    public void calculoPoupanca(double valor, double taxa)
    {
        Console.WriteLine("Ganhos obtidos pela poupança R$"+(valor * taxa));
    }

}
```
	
Note que o método obrigatório não abre chave, pois ele é obrigatório a ser feito nas classes que herdarem a classe Padrão.

E nas classes que forem herdar o padrão vai estar assim:

```c#
class PessoaFisica : Padrao
{

    // Método obrigatório
    public override void taxaEmprestimo(double valor)
    {
        Console.WriteLine("Taxa de empréstimo para Pessoa Física R$" 
                            + (valor * 0.1));
    }

}
```
	
Note que é necessário botar o override.  

**Se não fizer o método obrigatório dá erro no programa, pois é OBRIGATÓRIO FAZE-LO.**

Por fim, na Main você instancia o objeto classe PessoaFisica por exemplo, da mesma forma que uma normal:
```c#
PessoaFisica pf = new PessoaFisica();
```

A classe opcional pode ser puxada como uma herança pelo objeto pf não precisa ser refeita nem nada se não for necessário.

[Voltar ao Índice](#índice)

---

## Classes e Métodos Selados

Classes e Métodos Selados:  
```C#
public sealed class NomeDaClasse{}

public sealed void NomeDoMetodo(){}
```
Quando está **sealed**, ou seja, selada, a classe inteira ou o método não pode ser herdado, ele pode herdar (ter uma classe pai) mas não pode ser herdado (ter uma classe filha).  

[Voltar ao Índice](#índice)

---

## Classe object

Todas as classes herdam da classe Object, mesmo que você não faça `NomeDaClasse : Object`, é dai que vem aqueles métodos extras que aparecem quando você digita por exemplo: `p1.` ai aparece uma janelinha com uma lista de métodos, e alguns não é da classe que você criou, por exemplo Equals e ToString.  
A classe Object faz parte da raiz do .Net. 

[Voltar ao Índice](#índice)

---

## Interface (*não é interface gráfica*)

Interfaces são como um contrato de um projeto que deve ser seguido daquela forma.

- São utilizadas para criar exclusivamente métodos, propriedades, eventos e indexadores, todos obrigatórios (a classe abstrata tem opção de criar métodos opcionais, essa não, todos são obrigatórios).

- Uma classe pode implementar várias Interfaces (enquanto você só pode herdar 1 classe abstrata numa classe, a interface você pode "implementar" varias (e é usado o termo implementar ao invés de herdar)).

- Os métodos da Interface não contêm cálculos, condicionais, laços, e demais ações (igual as obrigatórias da abstrata que **não abrem chave**.  
```c#
double calculo(double numero);  
string texto();  
void mensagem(string nome, int idade);  
```  

- No C# por padrão um método criado na Interface é implicitamente abstrato e público (diferente da classe abstrata a interface é SEMPRE abstract e public, portanto você não precisa definir no inicio do método as palavras public abstract);  

- Nas boas práticas do C#, **toda interface tem a inicial I**, em seguida o nome da interface:  

```
IPadrao  
ICalculo  
IConsulta  
IAcoes  
```

Exemplo:  
Na classe de interface fica assim:
```c#
interface IPadrao
{
    void somar(int n1, int n2);

    void subtrair(int n1, int n2);
}
```	

**Leitura recomendada para mais detalhes: [Usando Interfaces - Macoratti](https://www.macoratti.net/11/11/c_intf1.htm)**

Leitura recomendada para mais detalhes: [Revisão de conceitos - Interface - Macoratti](https://www.macoratti.net/14/04/c_intf1.htm)

[Voltar ao Índice](#índice)

---
  
## DateTime
  
DateTime é um tipo de dado Struct que coleta a data e hora atual.  

Exemplo de uso:  
```c#
DateTime dataAtual = DateTime.Now;
Console.WriteLine(dataAtual);
```
Resultado vai ser o dia/mes/ano horário.  

Esse tipo também possui vários métodos, como por exemplo adicionar dias ao resultado:  
```c#
DateTime dataAtual = DateTime.Now.AddDays(5); //adiciona 5 dias
```
E se fizer assim:  
```c#
Console.WriteLine(dataAtual.ToString(dd/MM/yyyy));
```
Ou  
```c#
Console.WriteLine(dataAtual.ToShortDateString());
```
Ele vai mostrar só a data sem o horário, e sim o M tem que ser maiúsculo.  

E se fizer assim:  
```c#
Console.WriteLine(dataAtual.ToString(HH:mm));
```
Ou  
```c#
Console.WriteLine(dataAtual.ToShortTimeString());
```
Vai mostrar só a hora e o minuto sem os segundos, e o H tem que ser maiúsculo.  

DateTime.TryParseExact pode ser usado para converter uma data recebida em um padrão para outro, exemplo padrão americano para o padrão brasileiro.  


[Documentação do DateTime - Microsoft Learn](https://learn.microsoft.com/pt-br/dotnet/api/system.datetime?view=net-6.0)  

[Voltar ao Índice](#índice)  

---

# Teórico

## Alocação de Memória 

**Stack** e **Heap** são tipos de memoria, dependendo do tipo da sua variável ela vai para um ou outro tipo de memoria.  

O **Stack** é como uma pilha, ele armazena conforme a sequencia que a variável entrou (primeira linha, segunda linha...), o ultimo a entrar é o primeiro a sair (LIFO - Last In, First Out).  

Na **Stack** são armazenados tipos de variáveis mais simples (tipos primitivos), e quando a variável é complexa como um objeto ele armazena o nome do objeto e a referencia desse objeto que vai estar na memoria **Heap**.  

Na memoria **Heap** são armazenados tipos complexos como objetos, já que objetos podem conter vários tipos diferentes dentro dele.  

Portanto ao armazenar um objeto, seu nome ficará na **Stack** e haverá uma referencia para o objeto de verdade que está na memoria **Heap**.  

[Voltar ao Índice](#índice)  

---

## Limpeza de memória

Ao terminar o método, a limpeza de memoria ocorrerá da seguinte forma:
Na memória **Stack** é tipo uma pilha, ela vai remover da memoria a partir da ultima variável que entrou na **Stack**.  

Na memória **Heap** o C# usa o **Garbage Collector**, que verifica se tem algum objeto que não tem mais referencia na memoria **Stack**, pois se não houver referencia não tem como ele ser usado, então todo objeto da memória **Heap** que não tem mais ligação nenhuma com a memória **Stack** o **Garbage Collector** apaga da memoria. Por isso ela não tem uma ordem de limpeza como a **Stack**, pois um objeto ainda pode estar sendo usado enquanto o proximo e o anterior que entraram ja foram eliminados porque não tiveram mais uso.  

[Voltar ao Índice](#índice)  

---

## Tipos de valor (Teórico)

O tipo de valor armazena dados estáticos e não complexos (também conhecido por tipos primitivos**).  
São tipos simples, como int, float, string, decimal, eles conseguem armazenar seus nomes e seus dados dentro da **Stack** pois são simples.  
E se por exemplo:  
```c# 
int a = 5;  
int b = a;  
```
Ele vai salvar na memória **Stack** da seguinte forma:  
```c# 
a = 5;  
b = 5;  
```
Ele não vai criar uma referencia ao `a`, e sim vai copiar o valor para `b`.  
Portanto se você alterar o valor de `b`, somente `b` será alterado.  

[Voltar ao Índice](#índice)  

---

## Tipos de referência (Teórico)
O tipo de referência armazena dados dinâmicos e complexos.  
São tipos mais complexos, pois podem possuir vários tipos simples e até outros tipos complexos, dentro deles, então na memoria **Stack** é armazenado só o nome e a REFERÊNCIA do verdadeiro tipo que está armazenado lá na memoria **heap**.  
E se por exemplo:
```c#  
Pessoa p1 = new Pessoa("Daniel", "Franco");  
Pessoa p2 = p1;
```  
Ele vai salvar na memoria `p1` e `p2` apontando para o mesmo objeto, portanto se você fizer:  
```c# 
p2.Nome = "Luis"; 
``` 
Tanto `p1` quanto `p2` irão mudar seus dados para `"Luis" "Franco"`, pois ao criar um novo objeto sem instanciar você apenas está criando um novo nome apontando para o mesmo lugar na memoria Heap.
Então você NÃO cria uma copia de um "tipo complexo" dessa forma como nos "tipos simples".  
E se ambos apontam para o mesmo lugar, quando altera um altera o outro TAMBÉM.
Ou seja para criar um `p2` tem que colocar `new Pessoa`, ai ele vai instanciar um novo objeto na memoria Heap, e para copiar os dados de `p1` para `p2` tem que ser feito de forma manual mesmo. Nem se instanciar ambos e depois fizer `p2 = p1` vai fazer o `p2` apontar para o `p1` e quando você for editar o `p2` ele vai alterar o `p1` do mesmo jeito.  

[Voltar ao Índice](#índice)  

---

# Outras informações

## Conversão de tipos

Para converter tipos de variáveis existe o Convert e o Parse, exemplo:
```c#
int a = Convert.ToInt32("5");
int a = int.Parse("5");
```

- É preciso fazer tratamento de entrada pois se a entrada for algo que não é compatível vai dar erro e crashar o programa.  

- A diferença entre os 2 é que o Convert permite valor de entrada nulo e o parse não. No caso do int o Convert vai converter null para 0.  

Se precisar converter algo para string, é só colocar `.ToString();` depois da variável. Exemplo:  
```c#
string texto = a.ToString();
```

Nos tipos numéricos, se vc passar um tipo compatível com outro tipo não é necessário converter.  
Exemplo um double que recebe o valor de um int, ou um long (q é um int que cabe mais números) recebendo um int.  
MAS se um int for receber um long ele vai dar erro, se usar o convert ele aceita certinho SE o valor que tiver no long não for maior do que o int suporta, se for maior vai dar erro.  


Uma forma de converter sem dar erros é usando o TryParse, que espera ja que de erro então se ele não conseguir ele só não faz o processo.  
Exemplo:  
```c#
string a = "15-";
int b = 0;

int.TryParse(a, out b);
```
Aqui acontece o seguinte, como o valor de `a` é invalido pois tem um traço, ele vai dar erro, portanto ele não vai executar a operação e vai manter o valor de `b` como 0, se o valor de `a` não fosse invalido ele iria sobrescrever o valor de `b` com o valor convertido.  

Também é possível gerar a variável durante o TryParse:  
```c#
int.TryParse(a, out int b);  
```
Ai se der erro, ele vai retornar 0 para `b`.  


[Voltar ao Índice](#índice)

---

## Listas

Listas são como arrays aprimorados, ela tem um array interno, você não precisa especificar seu tamanho (se quiser pode), você pode ir adicionando valores e ela vai crescendo sozinha (da resize no array interno sozinha), se remover um item ele reordena a lista e não deixa um espaço vago no meio como no array.  
Declaração e uso:  
```c#
List<string> listaString = new List<string>();
listaString.Add("nome");
listaString.Remove("nome");
``` 
Quando precisar verificar o tamanho da lista, utiliza-se `listaString.Count`, funciona da mesma forma do `array.Lenght`.  

[Voltar ao Índice](#índice)

---

## Summary

`<summary>` = documenta classes e metodos, quando vc passa o mouse sobre ela la no outro arquivo que esta instanciada/usando aparece o comentario no balãozinho.
para usar o summary vc digita barra 3 vezes, no visual studio community ele ja auto completa o seguinte código:
```c#
/// <summary>
/// Texto que quer que apareça ao passar o mouse na classe/metodo.
/// </summary>
```
No VSCode para auto completar é necessário ativar:  
engrenagem > configurações > editor de texto > marcar a opção: Format On Type.  
Ou dentro de configurações usar a barra de busca digitando format on type.

Obs: O summary tem q estar logo acima da classe ou método que voce quer documentar.  

Obs2: Se digitar as /// acima de uma classe com parâmetros, ele gera mais opções para voce documentar os parâmetros, a documentação desses parâmetros aparece no balão SOMENTE quando você está digitando ela, ao colocar a virgula para ir para o proximo parâmetro ele muda a documentação para a do proximo parâmetro.  

Obs3: Se a classe tiver return também tem um campo para documentar o retorno.  
Exemplo:    
```c#
/// <summary>
/// Soma dois valores
/// </summary>
/// <param name="x">Primeiro valor a ser somado</param>
/// <param name="y">Segundo valor a ser somado</param>
/// <returns>Retorna a soma dos valores</returns>
public int SomaPasseOMouseSummary(int x, int y)
{
    return x + y;
}
```

[Voltar ao Índice](#índice)

---

## Definindo uma região e formatando estilo monetário

Ao instalar um sistema operacional ou até mesmo depois de instalado, você define a região do sistema, essa região não é o idioma, e ela define coisas como sigla monetária (`$`, `R$`) e o uso de ponto no lugar de virgula ou vice versa.  

Exemplo:

Se adicionar `:C` na exibição de um valor, ele adiciona o **estilo monetário da região que o SO está configurado**, no nosso caso R$ e ponto na casa do milhar, por exemplo:  
```c#
decimal valorMonetario = 1522.55M;
Console.WriteLine(${valorMonetario:C}";
```
Vai exibir: R$ 1.522,55  

Caso queira garantir que os dados serão visíveis da forma planejada para uma região apenas, é possível definir uma região especifica para o software da seguinte forma:  
```c#
using System.Globalization;

CultureInfo.DefaultThreadCurrentCulture = new CultureInfo("en-US");
```

Como foi colocado `en-US` a localização foi para o estilo americano, então o código acima vai exibir o seguinte:  
$ 1,522.55  
Que é o padrão de formatação de valor americano.  

Se quiser que apenas um valor seja no padrão americano por exemplo e o resto tudo no padrão brasileiro, da para fazer assim:  
```c#
Console.WriteLine(valorMonetario.ToString("C", CultureInfo
.CreateSpecificCulture("en-US")));
```
É possível determinar o numero de casas apos a virgula colocando um numero apos o C, exemplo: C1, C2, C5, C8...  

Se usar N no lugar do C, ele formata como número, similar ao C mas com a exceção do indicador monetário: R$, $...   

Se utilizar P a formatação fica como porcentagem.  
Porém, para o valor sair certo, tem que por ponto na frente do numero (porcentagem = .12; ), do contrario o numero 12 por exemplo vai ser mostrado como 1.200,00% ao invés de 12,00%
Isso independente se for int, float, double ou decimal.  

### Formatações manuais

Também é possível fazer formatações manuais como por exemplo:  
```c#
int numero = 123456;  
Console.WriteLine(numero.ToString("##-##-##"));  
```
A saida vai ser: 12-34-56  
o # representa um digito.  

[Voltar ao Índice](#índice)

---

## Serialização 

Verificar no projeto: [SerializacaoEAtributos](https://github.com/daniellfranco/treinos-basicos-cursos-CSharp/tree/main/Novos/4-SerializacaoEAtributos)  

- <strike>Para fazer serialização em json no dotnet é recomendado o pacote nuget Newtonsoft.Json.</strike>  
- A partir da versão AspNetCore 3.0, o recomendado a usar é a System.Text.Json que tem melhor otimização.
 

Para conferir se um json é valido, use este site:    
https://codebeautify.org/jsonviewer   

- O json representa as horas recebidas pelo datetime de forma independente, usando o padrão ISO 8601.  

A biblioteca json possui ["Atributos"](#atributos) que são um código que fica acima das propriedades que permite alterar o comportamento de algumas coisas.  
Exemplo:  
```c#
[JsonProperty("Nome_Produto")]
public string Produto { get; set; }
```
Esse atributo, ao receber no arquivo json uma propriedade com o nome "Nome_Produto" (que está fora da convenção de código do C# então você não vai querer fazer uma propriedade com esse nome pois não está em PascalCase) ele Vai dizer para o desserializador pegar essa propriedade e colocar na propriedade abaixo que é a Produto.  

[Voltar ao Índice](#índice)

---

## Tuplas

Tuplas são usadas para armazenar varios tipos de valores em uma variável só sem ser um objeto.
Podem ser usadas para facilitar trabalhar com um conjunto de dados, ou para armazenar um conjunto de dados recebido de um banco de dados, ou para retornar/receber multiplos valores de um método, ao invés do método retornar um valor, ele pode retornar 5 valores por exemplo...

Uma tupla pode ser declarada das seguintes formas:
```c#
// No primeiro parenteses você coloca todos os tipos que voce vai ocupar na tupla.
// No segundo você declara eles, precisa ser na ordem dos tipos do primeiro parenteses.
(int, string, string, decimal) tupla = (1, "Daniel", "Franco", 1.80M);

// Também é possivel declarar o nome de cada tipo da tupla
(int ID, string Nome, string Sobrenome, decimal Altura) tupla2 = (2, "Nayala", "Forest", 1.69M);

// Também pode ser declarado das seguintes formas, mas o recomendado é a forma acima
// Pois na acima dá para nomear as variaveis da tupla deixando ela mais legivel.
ValueTuple<int, string, string, decimal> outroExemploTupla = (3, "Daniel", "Franco", 1.80M);

// Também pode ser criado desta forma
var outroExemploTupla2 = Tuple.Create(4, "Nayala", "Forest", 1.69M);

// E quando recebe de um return
// O metodo envia uma tupla mas aqui ele separa em variáveis separadas.
// bool, string, int
var (sucesso, linhasArquivo, quantidadeLinhas) = exemploTuplas.LerArquivo("Arquivos/ArquivoTexto.txt");
// Os nomes desejados tem que estar na ordem que o return mandou:
return (true, linhas, linhas.Count());
// E se por acaso algum dos retornos não for necessario em algum momento, pode-se
// por um _ (underline) no lugar da variavel que vc não vai usar
// exemplo:
// var (sucesso, _, quantidadeLinhas) = exemploTuplas.LerArquivo("Arquivos/ArquivoTexto.txt");
// Ai não cria variavel desnecessaria e melhora a legibilidade do codigo
```

E pode ser lida das seguintes formas:

```c#
// Quando não é dado nome às propriedades:
Console.WriteLine($"ID: {tupla.Item1}");
Console.WriteLine($"Nome: {tupla.Item2}");
Console.WriteLine($"Sobrenome: {tupla.Item3}");
Console.WriteLine($"Altura: {tupla.Item4}");

// Quando é dado nome às propriedades:
Console.WriteLine($"ID: {tupla2.ID}");
// Mas também pode ser lido usando Item mesmo quando a propriedade tem nome.
Console.WriteLine($"Nome: {tupla2.Item2}"); 
Console.WriteLine($"Sobrenome: {tupla2.Sobrenome}");
Console.WriteLine($"Altura: {tupla2.Altura}");
```

Meu projeto com esses codigos: [ExemploTuplas](https://github.com/daniellfranco/treinos-basicos-cursos-CSharp/blob/main/Novos/3-TuplasTernarioEDesconstrucao/Models/ExemploTuplas.cs)


Leituras adicionais:  
[Apresentando Tuples - Macoratti](https://www.macoratti.net/13/07/c_tup1.htm)  
[Tipos de tupla (Referência do C#) - Microsoft Learn](https://learn.microsoft.com/pt-br/dotnet/csharp/language-reference/builtin-types/value-tuples)  

[Voltar ao Índice](#índice)

---

## Desconstrutor

O desconstrutor ele devolve os dados da classe.
Digamos assim, você carregou os dados pelo construtor, tratou eles, e ai agora você precisa pegar eles devolta tratadinhos, quem vai fazer isso é o desconstrutor.

Exemplo simples da classe:
```c#
    internal class ExemploDesconstrutor
    {
        public string Nome { get; set; }

        public string Sobrenome { get; set; }

        //Construtor adiciona os dados
        public ExemploDesconstrutor(string nome, string sobrenome)
        {
            Nome = nome;
            Sobrenome = sobrenome;
        }

        //Descontrutor devolve os dados
        public void Deconstruct(out string nome, out string sobrenome)
        {
            nome = Nome;
            sobrenome = Sobrenome;
        } 
    }
```

Exemplo simples do uso:
```c#
//construtor adicionando os dados
ExemploDesconstrutor p1 = new ExemploDesconstrutor("Daniel", "Franco");

//desconstrutor devolvendo os dados, similar a tupla
(string nome, string sobrenome) = p1;
```


Leitura adicional: 
[Apresentando o recurso Deconstruction - Macoratti](https://www.macoratti.net/20/06/c_deconstr1.htm)


[Voltar ao Índice](#índice)

---

## Tipos Especiais

**[Meu projeto com tipos especiais para mais referencias](https://github.com/daniellfranco/treinos-basicos-cursos-CSharp/tree/main/Novos/5-TiposEspeciais)**

### Tipos Anuláveis

Quando você coloca um ? no nome da variavel, exemplo `string?` ela se torna Nullable (anulável).  

Algumas variáveis como o tipo booleano, bool, não suportam null, no caso do bool é somente true ou false, para aceitar um null, coloca-se um ? no tipo, ficando `bool?`.  
Vale ressaltar que fazer isso sem um tratamento pode causar erros no sistema, pois por exemplo, um booleano pode ser inserido direto em um if sem comparador, pois o if trabalha com true e false (vide [If sem comparador](#if-sem-comparador)), mas se ele receber um null ele não vai saber oque fazer e dar erro.  

Obs: Quando transforma um bool em nullable, ele para de funcionar do jeito "de sempre", no exemplo do if, após você ter certeza que ele não é nulo, você teria que usar um `nomeDaVariavel.Value` para que o if consiga ler se é true ou false.  

**Sugestão de tratamento** - Usar `nomeDaVariavel.HasValue` para ver se não é null.  

Exemplo de uso com tratamento:   
```c#
bool? desejaReceberEmail = null;

if (desejaReceberEmail.HasValue && desejaReceberEmail.Value)
{
    Console.WriteLine("O usuário optou por receber e-mail.");
}
else
{
    Console.WriteLine("O usuário não respondeu ou não optou por receber e-mail.");
}

```

--

### Tipos Anônimos

Tipos anônimos são parecidos com tuplas, mas com a desvantagem que não podem ser editados depois e nem ser usados para retornar métodos, mas ele serve para representar algum objeto novo somente com propriedades que você queira que ele retorne, como se você desconstruísse algum objeto e fazendo um tipo anonimo só com os dados que voce queira.  

Exemplo de uso simples de tipo anonimo:  
```c#
var tipoAnonimo = new { Nome = "Daniel", Sobrenome = "Franco", Altura = 1.80 };

Console.WriteLine("Nome: " + tipoAnonimo.Nome);
Console.WriteLine("Sobrenome: " + tipoAnonimo.Sobrenome);
Console.WriteLine("Altura: " + tipoAnonimo.Altura);
```

Leitura adicional recomendada para mais detalhes e usos: [Tipos Anônimos - Macoratti](https://www.macoratti.net/12/07/c_antip1.htm)

--

### Tipo Dinâmico

Tipos dinâmicos permitem ter seu tipo alterado conforme oque recebem.  

Exemplo:  
```c#
// Iniciou como um int pois recebeu um inteiro
dynamic variavelDinamica = 4;

// Agora virou uma string
variavelDinamica = "Texto";

// Agora virou booleano
variavelDinamica = true;
```

É util em alguns casos dado seu dinamismo, mas pode ser perigoso, uma confusão ao trabalhar com oque ela recebe e vai gerar uma exceção.


[Voltar ao Índice](#índice)

---

## Classes Genéricas

Classes genéricas são uma forma interessante de reaproveitamento de código.
Com elas você não define um tipo na sua criação e sim na hora de instanciar.

Exemplo, você quer criar uma classe que irá manipular arrays de uma forma especifica, e precisa que isso sirva para qualquer tipo de variável que um array aceita. 
Então você coloca esse T, esse T recebe o Tipo que você irá colocar na hora de instanciar:
```c#
class MeuArray<T>
{}
```

A partir dai, todos os locais que você quiser usar o tipo que será definido na instanciação deverão receber T, exemplo:
```c#
// Cria um array do tipo recebido em T
private T[] array = new T[capacidade];

// Adiciona um elemento do tipo recebido no T
public void AdicionarElementoArray(T elemento)
{}
```

Classe de um projeto meu demonstrando o tipo genérico: [Meu Array.cs - Models - Tipos Especiais](https://github.com/daniellfranco/treinos-basicos-cursos-CSharp/blob/main/Novos/5-TiposEspeciais/Models/MeuArray.cs)  

Leituras adicionais:  
[Classes Genéricas - Microsoft Learn](https://learn.microsoft.com/pt-br/dotnet/csharp/programming-guide/generics/generic-classes)  
[Criando e usando uma classe ou método Genérico - Macoratti](https://www.macoratti.net/17/09/c_cugmc1.htm)  


[Voltar ao Índice](#índice)

---

## Métodos de Extensão

Um método de extensão é um recurso para adicionar métodos direto ao tipo.  

Ele é sempre estático, se for feito em uma classe só para métodos de extensão a classe tem que ser estática também, pois assim vai funcionar em qualquer lugar do projeto.  

Exemplo:  
```c#
public static class MetodoDeExtensaoInt
    {
        public static bool EhPar(this int numero)
        {
            return numero % 2 == 0;
        }
    }
```

Esse método EhPar vai extender sua função para o tipo int.
Resumindo de forma pratica:  
Basicamente se você fizer isso, quando você escrever uma variável do tipo int, exemplo `int numero`, você vai poder digitar numero.EhPar(), e nesse caso ele faz uma comparação para conferir se o resto da divisão é 0, se for zero é par, senão é impar, e retorna um true ou false.  

**OBS: Não funciona somente para tipos já existentes, você pode usar para Objetos/Entidades também**   

Leituras adicionais:  

[Métodos de extensão - Microsoft Learn](https://learn.microsoft.com/pt-br/dotnet/csharp/programming-guide/classes-and-structs/extension-methods)  
[Métodos de Extensão (revisitado) - Macoratti](https://www.macoratti.net/18/04/c_extmet1.htm)  

[Voltar ao Índice](#índice)

---

## Instrução Using (Objeto descartável)

É uma forma de declarar um objeto para que ele seja usado somente dentro do escopo e descartado assim que sair do escopo.

[Instrução Using : Close e Dispose - Macoratti](https://www.macoratti.net/20/02/c_using1.htm)

[Voltar ao Índice](#índice)

---

# Dicas

## Palavras Reservadas

Normalmente não é possível utilizar palavras reservadas pelo C# como um nome de variável, classe ou parâmetro, porem se colocar um `@` na frente de uma palavra reservada vc consegue usa-la, mas não é ideal, então evite.  

[Voltar ao Índice](#índice)

---

## Carregando uma variável numérica com valor máximo

Usando o comando:  
```c#
long variavel = long.MaxValue;
```
A variável será carregada com o valor máximo que o long suporta.  
os outros tipos também suportam esse `.MaxValue` pode ser útil para testes.  

[Voltar ao Índice](#índice)

---

## IF sem comparador

O if não precisa ter comparador, se ele receber uma variavel booleana que seja true ou false ele ja determina o caminho, não precisa comparar a variavel boleana, exemp.:
```c#
if (varBool == true)
{}
```
Apenas estar assim ja é o suficiente:
```c#
if (varBool)
{}
``` 
Pois varBool vai estar carregado com um `true` ou um `false`, e o if ja compara se é true ou false, todos os operadores dentro de um if retornam um resultado true ou false para o if decidir o caminho, por isso o if trabalha direto também sem comparação.

[Voltar ao Índice](#índice)

---

## Uso diferenciado do switch-case

Algumas vezes a gente não percebe algumas formas de usar algo sem ter visto antes, esse é o caso dessa forma de usar do switch-case que eu não havia visto anteriormente na faculdade nem em cursos, e até o dia que eu vi isso eu não tinha pensado que poderia funcionar assim.

```c#
switch(letra)
{
	case "a":
	case "e":
	case "i":
	case "o":
	case "u":
		Console.WriteLine("Vogal");
		break;

	default:
		Console.WriteLine("Não é uma vogal");
		break;
}
``` 

Logica: Não é necessário ter um código em cada case, se ele não tiver o `break` ele vai continuar até chegar em um `break`, e se o resultado não bater com nenhum case ele vai pular todos e entrar no default como sempre.  
Eu achava que assim não funcionaria pois por mais que ele entrasse ja no primeiro case, ao ir para o proximo case iria pular o código de dentro dos próximos.

[Voltar ao Índice](#índice)

---

## Quebrando laços de repetição antes do fim

É possível quebrar um laço de repetição antes do seu fim utilizando o comando: 
`break;` (igual do switch case).  
A ideia é fazer um if com isso caso algo especifico seja alcançado antes do fim das repetições.  

[Voltar ao Índice](#índice)

----

## "Alterando" o tamanho de um Array

Não é possível alterar o tamanho de um array em tempo de execução, oque da para fazer é usar um código que vai pegar a referencia do array na memoria, copia-lo, apagar o array original e colocar no lugar na memoria um array novo com capacidade maior.  
Esse comando é:  
```c#
Array.Resize(ref nomeDoArray, 10);
```  
Nesse exemplo você está usando o comando ref para pegar a referencia na memoria do array, e dizendo que agora vc quer que ele tenha 10 espaços.  
Também é possível usar:  
```c#
Array.Resize(ref nomeDoArray, nomeDoArray.Lenght * 2);
```  
Por exemplo para dobrar o tamanho do array se assim for desejado.  

**Dica**: se precisar ficar alterando muito o tamanho de um array considere utilizar um `List<>`.

[Voltar ao Índice](#índice)

---

## Copiando Arrays

Para copiar um array para outro, usasse o comando:  
```c#
Array.Copy(arrayOriginal, arrayDestino, arrayOriginal.Lenght);
``` 
no caso a ultima parte com o `.Lenght` é a quantidade de elementos que você quer copiar, se quer copiar tudo ou só os 2 primeiros por exemplo.

[Voltar ao Índice](#índice)

---

## Tratamento Get e Set simples usando =>

Quando o get ou o set tem apenas 1 linha de código de tratamento, pode se usar `=>` (o nome desse simbolo é body expression) ao invés de chaves.
exemplo:
```c#
get => _nome.ToUpper();
```

Se você usar esse simbolo direto na propriedade, exemplo:  
```c#
public string NomeCompleto => $"{Nome} {Sobrenome}";
```
Automaticamente a propriedade vai ser somente GET e ela vai setar automaticamente as variáveis concatenadas. Ou seja, se em Nome tiver Daniel e sobrenome tiver Franco, em nome completo vai ser armazenado Daniel Franco.

[Voltar ao Índice](#índice)

---

## Usando o nome dos parâmetros ao passar os argumentos

Você pode passar o nome dos parâmetros ao passar o [argumento](#argumentos-e-parâmetros)  
```c#
Pessoa p1 = new Pessoa(nome: "Daniel", sobrenome: "Franco");
```
Serve mais para deixar mais legível, mas também serve para inverter `(sobrenome: "Franco", nome: "Daniel")` se houver algum motivo para isso.

[Voltar ao Índice](#índice)

---

## Botou um valor decimal float ou double e não funcionou?

Precisa botar um M no valor do decimal, exemplo:
```c#
decimal valor = 10.12M;
```
Assim como para float é `f` e o double é `d`.

[Voltar ao Índice](#índice)

---

## Links para leitura sobre Design Patterns

- [.NET - Design Patterns - Identificando e aplicando padrões - Macoratti](https://www.macoratti.net/13/09/net_dp1.htm)   
Esse é uma sequencia, no final de cada artigo tem o link para o proximo.

[Voltar ao Índice](#índice)

----
