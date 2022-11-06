# MVC - Model View Controller

É um padrão que separa um aplicativo em 3 grupos de componentes princiais:
Modelos, Exibições e Componentes. Esse padrão ajuida a obter a separação de interesses.

---

</br>

## Context, Controllers e Rotas das páginas

As classes Context do MVC são exatamente iguais as dos projetos webapi. [Ver Anotações WebAPIs](../5%20-%20APIs%20com%20C%23/Anota%C3%A7%C3%B5es%20WebAPIs.md).

As classes Controller do MVC herdam de Controller, apenas isso, é até mais simples que o do webapi. [Ver Anotações WebAPIs](../5%20-%20APIs%20com%20C%23/Anota%C3%A7%C3%B5es%20WebAPIs.md).

O Controller das paginas é influenciado pelo nome, HomeController vai automaticamente buscar as views dos seus metodos na pasta Home (pois antes do Controller está escrito Home, se tivesse OlaController ele iria buscar na pasta Ola) que está na pasta Views, assim como o return View(); vai retornar a pagina com o nome correspondente ao metodo em que ele está, exemplo Index() ou Privacy().

![MarcacoesComoRotasFuncionam](imgs\MarcacoesComoRotasFuncionam.png)

Quando acessar o link da pagina referente a um controller, exemplo:  
`https://localhost:7277/Home`  
Automaticamente ele puxa o metodo Index.  
O Index é a unica excessão, os outros é necessario dizer o caminho certinho, exemplo:  
`https://localhost:7277/Home/Privacy`

---

</br>

## Paginas

As paginas são montadas com html de forma similar a um site normal, e são salvas no formato `.cshtml`.

O formato `cshtml` mistura html com cSharp, existem comandos como:
```c#
@model IEnumerable<ProjetoMVC.Entities.Contato>
```
e

```c#
@foreach (var item in Model)
{}
```
Esses comandos são alguns exemplos provenientes do AspNet MVC.

<br>

A primeira linha de codigo da pagina define uma lista de Contato chamada model, ela que vai pegar nossa entidade modelo de contato para nos trabalharmos com ela na nossa listagem de contatos.

![Pagina-CSHTML](../6%20-%20FrontEnd%20com%20MVC/imgs/Pagina-CSHTML.png)

---



