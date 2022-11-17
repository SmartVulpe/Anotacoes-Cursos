# Notas VSCode e comandos console DotNet


## Básico para usar dotnet no VSCode

Caso use o VSCode tem q instalar o .net separado pelo [site oficial](https://dotnet.microsoft.com/en-us/download) e mais as seguintes extensões:
- C# (obrigatório).
- C# Extensions (do autor JosKreativ).
- vscode-solution-explorer (facilita criar e manipular solutions).
- vscode-icons (extensão visual, não é necessária, mas ajuda a distinguir mais facilmente os arquivos).

Para abrir uma pasta no vscode via terminal/bash digitar o comando:
**code .**



## Comandos console DotNet

- **dotnet new console** = cria um projeto de console (na última versão do dotnet instalada no computador) na pasta q você está.
- **dotnet new console --framework net5.0** = cria um projeto de console na versão especificada, nesse caso na versão 5 do .net.
- **dotnet run** = executa o projeto da pasta q você está.


## Debugar no VSCode

Para debugar no VSCode siga os seguintes passos:
- Clicar **ao lado da linha** que você deseja que o programa pare para começar a analise, para adicionar o breakpoint.
- **Apertar F5** (ou o botão com o símbolo de "play com um insetinho" que fica na esquerda), o VSCode irá gerar e abrir um arquivo json com as config para debugar, você pode fechar esse arquivo que abriu pois você não vai mexer nele.
- **Apertar F5** novamente (ou o botão da esquerda) para começar a rodar o projeto em modo debug.
- Quando o programa chegar no breakpoint ele vai parar, então para seguir passo a passo você pode **apertar F10** ou no botão correspondente que apareceu acima na caixa de código do VSCode.


## Criando e Usando Solutions

**Para criar uma solution** no VSCode de forma simples vamos utilizar a extensão "vscode-solution-explorer", e seguir os passos:

- Clicar no ícone novo que apareceu na aba lateral esquerda (com a logo do visual studio). Vai aparecer escrito **No Solution Found**.
- Clica com o botão direito em **No Solution Found**.
- Clica em **Create new empty solution**, e dai é só dar um nome para a solution.

**Para adicionar um projeto na solution**:
- Clique com o botão direito na solution.
- Add existing project.
- Ir na pasta do projeto e **selecionar o arquivo csproj** do projeto.

**Para criar um projeto só de classes, sem executável**:
- Clica com o botão direito na solution.
- Add new project
- Class Library
- Escolhe a linguagem (nesse caso C#).
- De um nome.

Neste caso é recomendável o uso de .Common no final do nome para identifica-lo como um projeto que terá classes que serão acessadas por todos os projetos da solution (vide [Convenções e Boas Praticas.md](https://github.com/daniellfranco/desafio-dio-primeiro-repositorio-github/blob/main/Anota%C3%A7%C3%B5es%20Cursos%20Bootcamp%20DotNet%20DIO/2%20-%20%20C%23/Conven%C3%A7%C3%B5es%20e%20Boas%20Praticas.md)).


**Quando você vai organizar as pastas do projeto**, exemplo: criou a solution em cima de um projeto e dai moveu os arquivos do projeto para uma pasta especifica para organizar, é necessário conferir e corrigir os caminhos que estão no arquivo da **solution.sln**.

Também é necessário referenciar os outros projetos que você queira usar em outro projeto dentro da solution, para isso:
- Vá na aba do VSCode que mostra só a solution (aquele botão com a logo do visual studio).
- Clica com o botão direito no projeto principal.
- Add Reference.  

O VSCode vai fazer as referências dentro do arquivo da solution.sln tudo automaticamente (**é necessário a extensão vscode-solution-explorer**).

---

## Instalando Nugets

Para instalar um nuget no vscode você vai no site nuget.org
Escolhe um pacote nuget, clica, ai na pagina do pacote vai ter uma aba escrito ".NET CLI" e ai vai ter o comando de console certinho para copiar, colar e executar na pasta do projeto. E não precisa colocar a parte --version para pegar sempre a ultima, somente se quiser uma versão especifica.