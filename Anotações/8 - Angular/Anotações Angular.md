# Indice

- [Indice](#indice)
- [Oque é o Angular?](#oque-é-o-angular)
- [Oque são Componentes](#oque-são-componentes)
- [Oque são Templates](#oque-é-um-template)



# Oque é o Angular?

O Angular é um framework de desenvolvimento front-end mantido pelo Google. Ele é uma ferramenta poderosa e popular para a criação de aplicativos da web dinâmicos e single-page (SPAs). Aqui estão algumas das principais funcionalidades e propósitos do Angular:      


- **Desenvolvimento de SPAs (Single Page Applications):** O Angular é especialmente eficaz no desenvolvimento de SPAs, onde uma única página web é carregada inicialmente e as atualizações subsequentes são realizadas dinamicamente, sem a necessidade de recarregar a página inteira. Isso resulta em uma experiência de usuário mais rápida e fluida.    

- **Two-way Data Binding:** Uma característica fundamental do Angular é o two-way data binding, que estabelece uma conexão automática entre os modelos de dados da aplicação e a interface do usuário. Qualquer alteração nos dados é refletida automaticamente na interface do usuário, e vice-versa, simplificando o gerenciamento do estado da aplicação.    

- **Injeção de Dependência:** O Angular utiliza um sistema de injeção de dependência para organizar e tornar mais modular o código. Isso facilita a manutenção, teste e extensão do código, permitindo que componentes e serviços sejam injetados em outros, tornando o código mais reutilizável e fácil de entender.     

- **Módulos e Componentes:** O Angular organiza o código em módulos, que são conjuntos lógicos de funcionalidades da aplicação, e componentes, que são blocos de construção reutilizáveis que compõem a interface do usuário. Isso facilita a modularização do código, melhorando a legibilidade e a manutenção.    

- **Roteamento:** O Angular oferece um sistema de roteamento robusto, que permite a navegação entre diferentes partes de uma aplicação sem a necessidade de recarregar a página. Isso é essencial para criar aplicativos de várias páginas dentro de uma única SPA.    

- **Manipulação do DOM:** O Angular lida com a manipulação do DOM de forma eficiente, simplificando a interação com elementos da página e garantindo uma renderização rápida e eficaz.   

- **Testabilidade:** O Angular foi projetado com a testabilidade em mente. Ele fornece ferramentas e estruturas para facilitar a escrita de testes unitários e de integração, garantindo a qualidade e a estabilidade do código.   

- **Ecossistema Rico:** O Angular possui um ecossistema rico, com uma variedade de bibliotecas, ferramentas e extensões que facilitam o desenvolvimento e melhoram a produtividade.   

Em resumo, o Angular é uma ferramenta abrangente para o desenvolvimento front-end que oferece estruturas sólidas para criar SPAs eficientes, modularizar o código, facilitar a manutenção e promover as melhores práticas de desenvolvimento web.   



[Voltar ao Indice](#indice)    

---

# Comandos CLI

- `ng --help` - Mostra a lista com todos os comandos.

- `ng new nome-do-projeto` - Cria um projeto angular.

- `ng g --help` - Lista de comandos para *gerar* "coisas" como classes, componentes, enum, applications, etc...   

- `ng g component components/new-component` - Cria um novo componente chamado *new-component* na pasta *components* que ele vai criar dentro da pasta src/app/ mesmo que voce use esse comando na raiz do projeto, o ideal é usar na raiz do projeto.     



[Voltar ao Indice](#indice)    

---

# Oque são Componentes?

Um componente é uma unidade de código responsável por uma única tarefa ou funcionalidade. Ele é composto por três partes principais:      

- **Template:** É o código HTML que define a interface visual do componente.

- **Estilo:** É o código CSS que define o estilo visual do componente.

- **Classe:** É a classe JavaScript que define a lógica de funcionamento do componente.

Os componentes são usados para organizar e modularizar o código Angular. Eles permitem que você desenvolva aplicações mais complexas e escaláveis, mantendo o código organizado e fácil de manter.    

Aqui estão alguns dos benefícios de usar componentes no Angular:     

- **Reutilização:** Os componentes podem ser reutilizados em diferentes partes da aplicação. Isso ajuda a reduzir a duplicação de código e a melhorar a produtividade.

- **Testabilidade:** Os componentes podem ser testados de forma independente, o que ajuda a garantir a qualidade do código.

- **Organização:** Os componentes ajudam a organizar o código Angular, tornando-o mais fácil de entender e manter.

Alguns exemplos de componentes Angular são:     

- **Componentes de formulário:** São usados para criar formulários para coletar dados do usuário.

- **Componentes de listagem:** São usados para exibir uma lista de itens.

- **Componentes de navegação:** São usados para controlar a navegação entre diferentes páginas da aplicação.

Os componentes são uma ferramenta fundamental para o desenvolvimento de aplicações Angular. Eles permitem que você desenvolva aplicações mais complexas e escaláveis, mantendo o código organizado e fácil de manter.    



[Voltar ao Indice](#indice)    

---

# Oque é um Template?

Um template é um arquivo HTML que define a interface visual de um componente. Ele é composto por uma combinação de elementos HTML, diretivas e expressões.     

Os templates são usados para definir a aparência visual dos componentes Angular. Eles permitem que você crie interfaces visuais complexas e interativas de forma rápida e fácil.      

Aqui estão alguns dos benefícios de usar templates no Angular:     

- **Reutilização:** Os templates podem ser reutilizados em diferentes componentes. Isso ajuda a reduzir a duplicação de código e a melhorar a produtividade.    

- **Testabilidade:** Os templates podem ser testados de forma independente, o que ajuda a garantir a qualidade do código.     

- **Organização:** Os templates ajudam a organizar o código Angular, tornando-o mais fácil de entender e manter.     


[Voltar ao Indice](#indice)    

---

# Oque é Control Flow?

No Angular, o controle de fluxo é a capacidade de controlar a ordem em que o código é executado.    

Ele é usado para executar código condicionalmente, iterar sobre coleções e repetir código.    

O controle de fluxo é uma ferramenta essencial para o desenvolvimento de aplicações Angular. Ele permite que você crie aplicativos mais complexos e interativos.    



[Voltar ao Indice](#indice)    

---

# Oque é Deferrable View?

Deferrable Views, também conhecidos como @defer blocks, são uma nova funcionalidade introduzida no Angular 17 que permite adiar o carregamento de determinadas partes de uma aplicação.     

Isso pode ser usado para melhorar o desempenho das aplicações, especialmente aquelas com grandes quantidades de conteúdo.     



[Voltar ao Indice](#indice)    

---


# Oque são Signals?

Signals são uma nova funcionalidade introduzida no Angular 17 que permite que os componentes se comuniquem entre si de forma assíncrona. Isso pode ser usado para melhorar a performance e a escalabilidade das aplicações.

**Exemplos**

Aqui estão alguns exemplos de como usar Signals para melhorar o desempenho e a escalabilidade das aplicações:

- Comunicação entre componentes: Você pode usar Signals para permitir que componentes se comuniquem entre si de forma assíncrona. Isso pode ajudar a melhorar o desempenho das aplicações, pois os componentes não precisam esperar que a resposta seja recebida antes de continuar.

- Notificações: Você pode usar Signals para enviar notificações para outros componentes. Isso pode ser útil para notificar os componentes de eventos que ocorrem em outros lugares da aplicação.

- Atualizações de dados: Você pode usar Signals para atualizar dados em vários componentes de forma assíncrona. Isso pode ajudar a melhorar a escalabilidade das aplicações, pois os componentes não precisam esperar que os dados sejam atualizados antes de renderizar.


**Considerações**

Ao usar Signals, é importante considerar os seguintes fatores:

- Eficiência: Os Signals podem melhorar o desempenho e a escalabilidade das aplicações, mas eles também podem adicionar complexidade.

- Manutenção: Os Signals podem tornar as aplicações mais difíceis de manter. É importante documentar cuidadosamente como os Signals são usados na aplicação.


Os Signals são uma nova funcionalidade poderosa que pode ser usada para melhorar o desempenho e a escalabilidade das aplicações Angular.



[Voltar ao Indice](#indice)    

---


