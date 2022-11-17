# Minhas anotações sobre CSharp  

## Índice
- [Minhas anotações sobre CSharp](#minhas-anotações-sobre-csharp)
  - [Índice](#índice)
- [Base do CSharp](#base-do-csharp)
  - [Namespace](#namespace)
  - [Declaração de variáveis](#declaração-de-variáveis)
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
  - [This](#this)
  - [Atributos e Métodos ESTÁTICOS](#atributos-e-métodos-estáticos)
  - [Herança](#herança)
  - [Polimorfismo](#polimorfismo)
  - [Classe Abstrata](#classe-abstrata)
  - [Classes e Métodos Selados](#classes-e-métodos-selados)
  - [Classe object](#classe-object)
  - [Interface (*não é interface gráfica*)](#interface-não-é-interface-gráfica)
- [Teórico](#teórico)
  - [Alocação de Memória](#alocação-de-memória)
  - [Limpeza de memória](#limpeza-de-memória)
  - [Tipos de valor](#tipos-de-valor)
  - [Tipos de referência](#tipos-de-referência)

</br>

---

# Base do CSharp

## Namespace 

O namespace indica qual o nome da pastinha que o Arquivo.cs pertence, da para ter vários repetidos desde q sejam de pastinhas diferentes.  
Obviamente que se você der using em mais de uma pasta com um arquivo de mesmo nome você terá que detalhar mais na hora de instanciar botando o caminho da pasta junto, senão irá dar conflito.

[Voltar ao Índice](#índice)

---  

## Declaração de variáveis

É possível declarar várias variáveis do mesmo tipo na mesma linha, exemplo:  
```c#
public double largura, altura, comprimento;
```  

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

Então a pessoa vai se chamar "obj" dentro do arquivo Program.cs e vc vai poder usar ela dessa forma:

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

"Os atributos podem ser colocados em praticameante qualquer declaração, embora um atributo específico possa restringir os tipos de declarações nas quais ele é válido. Na linguagem C#, você especifica um atributo colocando o nome do atributo entre colchetes ([ ]) acima da declaração da entidade à qual ele se aplica."     
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

Mais detalhes sobre get e set na sessão sobre [Get e Set](#get-e-set)

Fonte e leitura recomendada: [Diferença entre Campos(Fields) e Propriedades(Properties) - Macoratti](https://www.macoratti.net/17/01/c_camprop1.htm)  

[Voltar ao Índice](#índice)

---

## Argumentos e Parâmetros

Um **Parâmetro** é aquela variável que fica dentro do parenteses () do método.  
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
O software vai saber qual vc ta usando conforme oque você preencher nos parâmetros.  
Exemplo:  
Se não preencher nada ele vai executar o primeiro:  
**apresentar();**    

Se colocar uma string, ele vai executar o segundo:  
**apresentar("Soul");**   

Se colocar uma string E um int, ele vai executar o terceiro:    
**apresentar("Soul", 20);**  

E na hora q for escrever esse método ele vai mostrar na janelinha q aparece de auto-completar que tem 2 overloads (nesse caso do apresentar), q é a primeira opção e mais as 2 extras, totalizando 3 opções de uso do mesmo método.  

[Voltar ao Índice](#índice)

---

## Operadores Ternários

São como IFs, mas mais simples e limitados, muito úteis para comparações com resultados simples (apenas um true ou false, ou só retornar um texto ou um valor fixo q não exige ser calculado conforme comparação seja verdadeira ou falsa), exemplo:  
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

Modificadores de acesso são a maneira q vc tem de visualizar um método ou variável.  

public    -> Variáveis e métodos visíveis em qualquer classe.  
private   -> Variáveis e métodos visíveis apenas na classe onde são criados.  
protected -> Variáveis e métodos visíveis em classes onde são criados ou herdados.  

[Voltar ao Índice](#índice)

---

## Construtor  

O **Construtor** é um **método** que é executado **no momento que o objeto é instanciado.**  

Ele tem que ter o mesmo nome da classe.  

Toda vez q instanciar um objeto exemplo:  
```c#
Pessoa p = new Pessoa() ; 
```
O programa vai executar o construtor q nesse exemplo será:  
```c#
Public Pessoa()
{}   
```
Dentro do arquivo Pessoa.cs  

***Assim como os métodos da pra ter mais de um construtor usando parâmetros diferentes.***

**Dica:** se digitar **ctor** (abreviação para construtor) e apertar tab duas vezes ele vai criar automaticamente um modelo de construtor para você.

[Voltar ao Índice](#índice)

--- 

## This

**This** serve para forçar pegar o valor do atributo (variável), ao invés de um valor que veio por um **parâmetro** de mesmo nome, exemplo:

La no arquivo main o objeto que contem esse código está setando para nome: 
```c#
Pessoa("Nayala");        

    // Atributo
private string nome = "Soul";

public Pessoa(string nome)
{
    //Detalhe: Ambos atributo e parâmetro tem o mesmo nome

    //Sem o this ele pega o valor do parâmetro
    Console.WriteLine(nome);

    //Com o this ele pega o valor do atributo
    Console.WriteLine(this.nome);
}
```

No console vai aparecer:  
```
Nayala  
Soul  
```

ou seja, como o primeiro estava sem o **this** ele pegou o q foi setado para o atributo, e o segundo q tinha o **this** ele pegou oq tava na variável nome.

[Voltar ao Índice](#índice)

---

## Atributos e Métodos ESTÁTICOS

São atributos e métodos que podem ser acessados **sem precisar instanciar** um objeto.  
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
Basta por "2 pontos" após o nome da classe e inserir o nome da classe que vc quer "estender".  
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

**Dica:** Você pode herdar uma classe q herda outra classe que herda outra classe e assim por diante.  
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

Você pode ter, por exemplo, um método chamado valeTransporte(), e esse método por padrão é de um jeito, mas para o gerente vc precisa que tenha 1 valor diferente, ai vc cria uma classe com o mesmo método e essa diferença que precisa, ai na hora que instanciar vc só precisa instanciar com mescla, não vai precisar ter um valeTransporteGerente() pra se diferenciar do valeTransporte padrão, simplifica e padroniza alguns locais do código exigindo menos alterações, e joga as alterações em outros locais deixando mais organizado e legível.

Além de instanciar usando duas classes diferentes, é necessário que o método tenha o seguinte:
O método que **vai ser sobrescrito** tem que estar assim:  

```c#  
public virtual void valeTransporte(){}  
```
E o metodo que **vai sobrescrever** tem que estar assim: 

```c#  
public override valeTransporte(){}  
```
*As classes que vão sobrescrever, tem que herdar à que será sobrescrita, senão também não funciona.*  

**Além de haver esse polimorfismo por mesclagem, também da para fazer com simples herança.**  
Exemplo:  
Você tem a classe Professor que herdou a classe Pessoa, na classe pessoa tem Nome e Idade, e um método de se Apresentar(), ai na professor tem o Salario, mas quando você executar o método Apresentar herdado da pessoa você quer que ele se apresente diferente.  
Então la na Pessoa vc coloca virtual no método como explicado acima.  
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

**Se nao fizer o método obrigatório dá erro no programa, pois é OBRIGATÓRIO FAZE-LO.**

Por fim, na Main vc instancia o objeto classe PessoaFisica por exemplo, da mesma forma que uma normal:
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
Quando ta **sealed**, ou seja, selada, a classe inteira ou o método não pode ser herdado, ele pode herdar (ter uma classe pai) mas não pode ser herdado (ter uma classe filha).  

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

- Uma classe pode implementar várias Interfaces (enquanto você só pode herdar 1 classe abstrata numa classe, a interface vc pode "implementar" varias (e é usado o termo implementar ao invés de herdar)).

- Os métodos da Interface não contêm cálculos, condicionais, laços, e demais ações (igual as obrigatórias da abstrata que **não abrem chave**.  
```c#
double calculo(double numero);  
string texto();  
void mensagem(string nome, int idade);  
```  

- No C# por padrão um método criado na Interface é implicitamente abstrato e público (diferente da classe abstrata a interface é SEMPRE abstract e public, portanto vc não precisa definir no inicio do método as palavras public abstract);  

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
Ele vai mostrar só a data sem o horário, e sim o M tem q ser maiúsculo.  

E se fizer assim:  
```c#
Console.WriteLine(dataAtual.ToString(HH:mm));
```
Ou  
```c#
Console.WriteLine(dataAtual.ToShortTimeString());
```
Vai mostrar só a hora e o minuto sem os segundos, e o H tem q ser maiúsculo.  

DateTime.TryParseExact pode ser usado para converter uma data recebida em um padrão para outro, exemplo padrão americano para o padrão brasileiro.  


[Documentação do DateTime - Microsoft Learn](https://learn.microsoft.com/pt-br/dotnet/api/system.datetime?view=net-6.0)  

[Voltar ao Índice](#índice)  

---

# Teórico

## Alocação de Memória 

Stack e Heap são tipos de memoria, dependendo do tipo da sua variável ela vai para um ou outro tipo de memoria.  

o Stack é como uma pilha, ele armazena conforme a sequencia que a variável entrou (primeira linha, segunda linha...), o ultimo a entrar é o primeiro a sair (LIFO - Last In, First Out).  

No Stack são armazenados tipos de variáveis mais simples (tipos primitivos), e quando a variável é complexa como um objeto ele armazena o nome do objeto e a referencia desse objeto que vai estar na memoria Heap.  

Na memoria Heap são armazenados tipos complexos como objetos, já que objetos podem conter vários tipos diferentes dentro dele.  

Portanto ao armazenar um objeto, seu nome ficará na Stack e haverá uma referencia para o objeto de verdade que está na memoria Heap.  

[Voltar ao Índice](#índice)  

---

## Limpeza de memória

Ao terminar o método, a limpeza de memoria ocorrerá da seguinte forma:
Na memória Stack é tipo uma pilha, ela vai remover da memoria a partir da ultima variável que entrou na Stack.  

Na memória Heap o C# usa o Garbage Collector, que verifica se tem algum objeto que não tem mais referencia na memoria Stack, pois se não houver referencia não tem como ele ser usado, então todo objeto da memória Heap que não tem mais ligação nenhuma com a memória Stack o Garbage Collector apaga da memoria. Por isso ela não tem uma ordem de limpeza como a Stack, pois um objeto ainda pode estar sendo usado enquanto o proximo e o anterior que entraram ja foram eliminados porque não tiveram mais uso.  

[Voltar ao Índice](#índice)  

---

## Tipos de valor

O tipo de valor armazena dados estáticos e não complexos.  
São tipos simples, como int, float, string, decimal, eles conseguem armazenar seus nomes e seus dados dentro da Stack pois são simples.  
E se por exemplo:  
```c# 
int a = 5;  
int b = a;  
```
Ele vai salvar na memória stack da seguinte forma:  
```c# 
a = 5;  
b = 5;  
```
Ele não vai criar uma referencia ao a, e sim vai copiar o valor para b.  
Portanto se vc alterar o valor de b, somente b será alterado.  

[Voltar ao Índice](#índice)  

---

## Tipos de referência
O tipo de referência armazena dados dinâmicos e complexos.  
São tipos mais complexos, pois podem possuir vários tipos simples e até outros tipos complexos, dentro deles, então na memoria Stack é armazenado só o nome e a REFERÊNCIA do verdadeiro tipo que está armazenado lá na memoria heap.  
E se por exemplo:
```c#  
Pessoa p1 = new Pessoa("Daniel", "Franco");  
Pessoa p2 = p1;
```  
Ele vai salvar na memoria p1 e p2 apontando para o mesmo objeto, portanto se você fizer:  
```c# 
p2.Nome = "Luis"; 
``` 
Tanto p1 quanto p2 irão mudar seus dados para "Luis" "Franco", pois ao criar um novo objeto sem instanciar você apenas está criando um novo nome apontando para o mesmo lugar na memoria Heap.
Então você NÃO cria uma copia de um "tipo complexo" dessa forma como nos "tipos simples".  
E se ambos apontam para o mesmo lugar, quando altera um altera o outro TAMBÉM.
Ou seja para criar um p2 tem que colocar new Pessoa, ai ele vai instanciar um novo objeto na memoria Heap, e para copiar os dados de p1 para p2 tem que ser feito de forma manual mesmo. Nem se instanciar ambos e depois fizer p2 = p1, isso vai fazer o p2 apontar para o p1 e quando vc for editar o p2 ele vai alterar o p1 do mesmo jeito.  

[Voltar ao Índice](#índice)  

---
