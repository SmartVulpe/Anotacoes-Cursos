# Minhas anotações sobre CSharp  

## Qual a diferença entre metodo, procedimento e função?  

**Procedimento**: Parte de um programa ou classe que não retorna um valor (da definição de Delphi/Pascal). No Visual Basic/VB.NET, também é conhecimento como Subroutine (Subrotina, ou simplesmente Sub);  

**Função**: Parte de um programa ou classe que retorna um valor (da definição de Delphi/Pascal/Visual Basic/Visual Basic .NET);  

**Método**: Procedimento ou função pertencente a uma classe (várias linguagens de programação definem desta forma, por exemplo, c++, c#, java, etc.).  

"Há uma questão no Programmers em que isso é largamente debatido, mas o consensual é isso."  

---  

## Namespace 

o namespace indica qual o nome da pastinha que o Arquivo.cs pertence, da para ter varios repetidos desde q sejam de pastinhas diferentes.  

---  

## Declaração de variáveis

É possivel declarar várias variaveis do mesmo tipo na mesma linha, exemplo:  
```c#
public double largura, altura, comprimento;
```  

---  

## Classes 

Uma classe é um molde, que pode conter caracteristicas (as variaveis) de uma pessoa por exemplo, e metodos para executar uma ação referente a essa classe.  

- Toda classe começa com letra maiuscula (padrão universal de boas praticas de orientação a objetos).

---  

## Objetos  
  
Um objeto é como uma variavel contendo as classes (e suas variaveis e metodos) de um outro arquivo.

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

PS: Da pra instanciar varios objetos da mesma classe, literalmente igual variaveis, só dar outro nome ao objeto que no caso desse exemplo é a palavra "obj".

---

## Métodos  
  
É possivel usar o MESMO METODO para mais de uma ação ao mesmo tempo DESDE QUE ELES TENHAM PARAMETROS DIFERENTES.
Exemplo:

public void apresentar()
{}

public void apresentar(string nome)
{}

public void apresentar(string nome, int idade)
{}

***ESSES 3 PODEM EXISTIR SIMULTANEAMENTE***
O software vai saber qual vc ta usando conforme oque você preencher nos parametros  
Exemplo:  
Se não preencher nada ele vai executar o primeiro  
**apresentar();**  

Se colocar uma string, ele vai executar o segundo:  
**apresentar("Soul");**  

Se colocar uma string E um int, ele vai executar o terceiro:    
**apresentar("Soul", 20);**  

E na hora q for escrever esse método ele vai mostrar na janelinha q aparece de auto-completar que tem 2 overloads (nesse caso do apresentar), q é a primeira opção e mais as 2 extras, totalizando 3 opções de uso do mesmo metodo.  

---

## Operadores Ternarios

São como IFs, mas mais simples e limitados, muito úteis para comparações com resultados simples (apenas um true ou false, ou só retornar um texto ou um valor fixo q não exige ser calculado conforme comparação seja verdadeira ou falsa), exemplo:  
situacao = media >= 7 ? "aprovado" : "reprovado";  
Ou seja, a variavel string **situacao** recebe aprovado caso a media for **maior ou igual a 7**, ou reprovado caso não.  

---  

## Encapsulamento

Serve para proteger os dados de uma classe expondo somente o necessario.

Ou seja você vai ter os métodos e variaveis, que só a classe vai utilizar internamente em seus métodos, **como privados ou protected**, assim eles não aparecerão no objeto. Somente oque é para ser usado fora vai aparecer.  
Isso aumenta a segurança do projeto além de deixar mais limpo na hora de usar o objeto.   
Vide **Modificadores de Acesso** logo abaixo.

---

## Modificadores de acesso (public / private / protected)

Modificadores de acesso são a maneira q vc tem de visualizar um metodo ou variavel.  

public    -> Atributos e métodos visíveis em qualquer classe.  
private   -> Atributos e métodos visíveis apenas na classe onde são criados.  
protected -> Atributos e métodos visíveis em classes onde são criados ou herdados.  

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

***Assim como os métodos da pra ter mais de um construtor usando parametros diferentes.***

**Dica:** se digitar **ctor** (abreviação para construtor) e apertar tab duas vezes ele vai criar automatimente um modelo de construtor para você.

--- 

## Get e Set

**Get** e **Set** é uma tecnica para ler e escrever em uma propriedade, vc pode permitir apenas leitura (Get) ou apenas escrita (Set), ou ambos, essa tecnica melhora a segurança do projeto principalmente quando utilizada com variaveis privadas (Vide Encapsulamento).

Exemplo de uso:  
```c#
    private string nome;

    public string Nome
    {
        get { return nome; }

        set { nome = value; }
    }
```

As boas práticas dizem que quando usada com variaveis privadas o metodo get/set deve ter o mesmo nome que a variavel, mas com a primeira letra em maiuscula.

Também é possivel criar códigos para tratamentos de entrada ou saida dentro das chaves.

---

## This

**This** serve para forçar pegar o valor do atributo (variavel), ao inves de um valor que veio por um **parametro** de mesmo nome, exemplo:

La no arquivo main o objeto que contem esse codigo está setando para nome: 
```c#
Pessoa("Nayala");        

    // Atributo
private string nome = "Soul";

public Pessoa(string nome)
{
    //Detalhe: Ambos atributo e parametro tem o mesmo nome

    //Sem o this ele pega o valor do parametro
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

ou seja, como o primeiro estava sem o **this** ele pegou o q foi setado para o atributo, e o segundo q tinha o **this** ele pegou oq tava na variavel nome.

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
**MAS**, a menos que você tenha um ganho mt bom em algo, procure evitar deixar o codigo muito complexo assim, pois se ouver muitas dependencias de heranças, a hora que você editar um dos primeiros, por exemplo remover um metodo que não faz mais sentido naquela, mas acaba usando em outra la na frente, o código vai quebrar em cascata.  

---

## Polimorfismo

Esse é o polimorfismo em tempo de execução:

Basicamente, uma forma de criar um objeto aproveitando a maior parte de uma classe e sobreescrevendo somente o necessario

Funciona da seguinte forma, ao instanciar um objeto, vc pode instanciar usando duas classes.
exemplo:
Imposto objetoG = new Gerente();

**Dessa forma o objeto objetoG vai receber os metodos e variaveis da classe Imposto, E se ouver o mesmo método ou variável na classe Gerente, o programa vai sobrescrever os metodos da classe Imposto por esses da classe Gerente.**

Você pode ter, por exemplo, um metodo chamado valeTransporte(), e esse método por padrão é de um jeito, mas para o gerente vc precisa que tenha 1 valor diferente, ai vc cria uma classe com o mesmo metodo e essa diferença que precisa, ai na hora que instanciar vc só precisa instanciar com mescla, não vai precisar ter um valeTransporteGerente() pra se diferenciar do valeTransporte padrão, simplifica e padroniza alguns locais do codigo exigindo menos alterações, e joga as alterações em outros locais deixando mais organizado e legivel.

alem de instanciar usando duas classes diferentes, é necessario que o metodo tenha o seguinte:
o metodo que **vai ser sobrescrito** tem que estar assim:
public **virtual** void valeTransporte(){}

e o metodo que **vai sobrescrever** tem que estar assim:
public **override** valeTransporte(){}

*as classes que vão sobrescrever, tem que herdar à que será sobrescrita, senão tambem não funciona.*

Além de haver esse polimorfismo por mesclagem, também da para fazer de uma forma mais simples.
Exemplo.
Você tem a classe Professor que herdou a classe Pessoa, na classe pessoa tem Nome e Idade, e um metodo de se Apresentar(), ai na professor tem o Salario, mas quando você executar o metodo Apresentar herdado da pessoa você quer que ele se apresente diferente.
Então la na Pessoa vc coloca virtual no metodo como explicado acima.
e no metodo professor você faz um novo metodo apresentar com o override como explicado acima com as diferenças que você quer.
A diferença é que na hora de instanciar voce instancia sem mescla, pois a classe professor ja está herdando de pessoa.
Professor p1 = new Professor();

Esse é o polimorfismo em tempo de compilação:

Overloads de metodos também são um tipo de polimorfismo

---

