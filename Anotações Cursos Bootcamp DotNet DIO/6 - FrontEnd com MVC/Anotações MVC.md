# MVC - Model View Controller

É um padrão que separa um aplicativo em 3 grupos de componentes princiais:
Modelos, Exibições e Componentes. Esse padrão ajuida a obter a separação de interesses.

---

</br>

# Context, Controllers e Rotas das páginas

As classes Context do MVC são exatamente iguais as dos projetos webapi. [Ver Anotações WebAPIs](../5%20-%20APIs%20com%20C%23/Anota%C3%A7%C3%B5es%20WebAPIs.md).

As classes Controller do MVC herdam de Controller ao inves de ControllerBase, de resto é tudo igual as webapi. [Ver Anotações WebAPIs](../5%20-%20APIs%20com%20C%23/Anota%C3%A7%C3%B5es%20WebAPIs.md).
Obs: no MVC é opcional colocar tag HttpGet, mas as outras como HttpPost é necessario por.

O Controller das paginas é influenciado pelo nome, HomeController vai automaticamente buscar as views dos seus metodos na pasta Home (pois antes do Controller está escrito Home, se tivesse OlaController ele iria buscar na pasta Ola) que está na pasta Views, assim como o return View(); vai retornar a pagina com o nome correspondente ao metodo em que ele está, exemplo Index() ou Privacy().

![MarcacoesComoRotasFuncionam](imgs\MarcacoesComoRotasFuncionam.png)

Quando acessar o link da pagina referente a um controller, exemplo:  
`https://localhost:7277/Home`  
Automaticamente ele puxa o metodo Index.  
O Index é a unica excessão, os outros é necessario dizer o caminho certinho, exemplo:  
`https://localhost:7277/Home/Privacy`

---

</br>

# Paginas

As paginas são montadas com html de forma similar a um site normal, e são salvas no formato `.cshtml`, elas tem que ficar dentro de uma pasta Views, e em seguida uma pasta que seja referente ao que fazem, por exemplo você vai criar uma pasta Contato para colocar paginas com assuntos referentes a contatos dentro.

O formato `cshtml` mistura html com cSharp, existem comandos como este que não existe por padrão no html:
```c#
@foreach (var item in Model)
{}
```
<br>

Esta parte do codigo nomeia a aba da pagina.
```c#
@{
    ViewData["Title"] = "Criar novo contato";
}
```

<br>

## Enviando dados para as paginas

Esse metodo que fica na ContatoController, ele vai criar uma lista com todos os contatos que a context pegou do banco de dados, e retornar ela para a view Index.

![IndexContato](../6%20-%20FrontEnd%20com%20MVC/imgs/IndexContato.png)

Na view Index.cshtml a primeira linha de codigo, ela cria uma propriedade de lista IEnumerable, do tipo Contato, seguindo o caminho do projeto até a model contato, ai você pode utilizar a propriedade model para exibir o conteudo recebido da context.

![Pagina-CSHTML](../6%20-%20FrontEnd%20com%20MVC/imgs/Pagina-CSHTML.png)

---

# Codigos/Tags



- `asp-action="NomeDeAlgumMetodoDaController"` --- Essa tag invoca um metodo lá da classe controller. Por exemplo, se ele estiver dentro de um botão e no parenteses tiver Index, ele vai chamar o metodo Index que vai chamar a pagina Index.

- `asp-for="Nome"` --- Esta tag indica qual a propriedade que está relacionado, por exemplo, se for usada em um campo de texto, ela vai identifica pra qual propriedade o valor inserido no campo vai ser enviado, e também trabalhar as necessidades desse campo, se a propriedade que vir do banco de dados estiver setado que não pode receber nulo, então vai tornar obrigatorio que o campo não fique em branco antes de dar submit em um formulario por exemplo. E se for usado em um Label ele só da o nome da label igual a da propriedade.

- `class="control-label"` --- css? para formar o Label do campo de texto
- `class="form-control"` --- css? para formar o input do campo de texto.
- `class="btn btn-primary"` --- css? para formar um botão.
- `type="submit"` --- quando em um botão de conjunto de formulario, significa que é para submeter o formulario.
- `value="Criar"` --- quando em um bitão de conjunto de formulario, significa que é para retornar os dados do formulario para o metodo Criar.  

Exemplos:

```html
<div class="row">
    <div class="col-md-4">
        <!--Cria um formulario que irá retornar os dados para o metodo Criar-->
        <form asp-action="Criar">
            <!--Grupo do formulario referente ao rotulo e campo de entrada
            de texto da propriedade Nome-->
            <div class="form-group">
                <label asp-for="Nome" class="control-label"></label>
                <input asp-for="Nome" class="form-control" />
            </div>
            <!--Grupo do formulario referente ao rotulo e campo de entrada
            de texto da propriedade telefone-->
            <div class="form-group">
                <label asp-for="Telefone" class="control-label"></label>
                <input asp-for="Telefone" class="form-control" />
            </div>
            <!--Grupo do formulario referente ao rotulo a CHECKBOX da
            propriedade Ativo-->
            <div class="form-group">
                <label asp-for="Ativo" class="control-label"></label>
                <input type="checkbox" asp-for="Ativo" class="form-check-input" />
            </div>
            <br />
            <!--Grupo do formulario referente botão de submit que irá enviar
            os dados do formulario para o metodo Criar que é um HttpPost-->
            <div class="form-group">
                <input type="submit" value="Criar" class="btn btn-primary" />
            </div>
        </form>
    </div>
</div>
<hr/>
<div>
    <!--Chama o metodo Index que irá chamar a View Index-->
    <a asp-action="Index">Voltar</a>
</div>
```