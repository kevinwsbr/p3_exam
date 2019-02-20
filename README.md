# # Prova - Projeto de Software

## Funcionalidades
- Adição/remoção de informações referentes aos projetos e atividades.
- Associação de usuários.
- Alteração do status
	- “Em processo de criação” para “Iniciado”. O coordenador deve poder iniciar uma criação apenas se constarem todas as informações básicas.
	- “Iniciado” para “Em andamento”. O coordenador deve poder confirmar a alocação.
	- “Em andamento” para “Concluído”. O coordenador deve poder alterar o status para “Concluído”, se existir a descrição do projeto e atividades.
- Consulta por usuário;
- Consulta por projeto;
- Consulta por atividade;
- Relatório de projeto e atividades da unidade acadêmica.

## Diagrama

![](https://github.com/kevinwsbr/p3_exam/blob/master/diagrama.jpg "Diagrama do projeto")

## Classes
O sistema foi dividido nas seguintes classes:
### Users
A classe `Users` é responsável por reunir os atributos comuns a todos os membros da universidade como nome, e-mail e instituição de origem, além disso - há a definição de métodos que devem ser escritos em cada uma das subclasses. Da classe `Users`, derivam as seguintes subclasses:
#### Student
A classe Student possui como atributo os campos `role` que identifica seu grau na universidade (bacharelado, mestrado ou doutorado) e `registry` - que possui a sua matrícula acadêmica.
#### Teacher
A classe `Teacher` possui como atributo o campo `SIAPE`, responsável por identificar sua matrícula de professor junto à instituição; e métodos referentes à gerência dos projetos.
#### Professional
A classe `Professional` possui o campo `job`, onde é armazenado o tipo de função (desenvolvedor,
testador, analista ou técnico) desempenhada pelo profissional na instituição. Optou-se por incluir a categoria técnico dentro desta classe pois não observou-se nenhuma especificidade da categoria em relação às demais.
#### Researcher
A classe `Researcher` possui o atributo `researcher_ID` - que identifica o registro do membro na base de pesquisadores (*Lattes* e afins) e, assim como a classe `Teacher`, métodos referentes à gerência dos projetos.
### Projects
A classe `Projects` possui os atributos pertencentes a um projeto (nome, descrição, data de início/término, ID do responsável e status) - métodos que englobam a adição/exclusão de usuários e atividades no projeto e um método responsável por alterar o status atual do projeto.
### Activities
A classe `Activities` engloba os atributos de uma atividade. Além de seus identificadores, a classe é composta pela classe `Tasks` e possui um método para associar membros a uma atividade. 
### Tasks
A classe `Tasks` possui os atributos relativos a uma tarefa de um projeto e o identificador dos usuários responsáveis por ela.
## Distribuição dos Métodos
Nas classes que herdam de `Users` encontram-se os métodos `register()`, `update()` e `delete()` - cada um destes métodos possui interações com atributos específicos de cada classe, por isso foram reescritos nas subclasses.

Dentro das classes `Teacher` e `Researcher` é possível encontrar os métodos referentes à gerência dos projetos - tais como `startProject()` e `deleteProject()`.

As classes `Projects` e `Activities` possuem o método `generateReport()`, responsável por retornar todas as informações referentes aos projetos e atividades desenvolvidas. Ainda na classe `Projects`, encontram-se os métodos `addMember()` e `removeMember()` - responsáveis pelo controle de membros de um projeto e o método `changeStatus()`, onde é possível fazer a mudança de status do projeto e `addActivity()`, responsável pelo cadastro de atividades em um projeto.

Nas classes `Activities` e `Tasks` existe um método chamado `associate()`, onde é possível associar membros do projeto a estas atividades/tarefas.

## Herança
Conforme dito na seção **Classes**, as classes `Teacher`, `Student`, `Professional` e `Researcher` herdam da classe `Users` pois compartilham diversos atributos (como nome e e-mail) e métodos - `register()`, `update()` e `delete()`.
## Classe Abstrata
`Users` é uma classe abstrata. Foi definida desta forma pois não é possível instanciar um usuário sem que este seja de um tipo específico (aluno, professor, pesquisador, etc). Dessa forma, as subclasses de `Users` fazem a implementação dos métodos definidos em `Users`. 
## Interface
Não houve implementação de interfaces no projeto.

## Polimorfismo
Observa-se o uso de polimorfismo no método `update()` presente na classe `Users` e nas classes que herdam desta. Dessa forma, o método `update()` é escrito em cada "classe filha" com a adição dos campos específicos de cada uma das classes.
## Tratamento de Exceções
Apesar de não ser descrito no diagrama, todas as interações com a entrada de dados (validação e pré-processamento) e com a persistência destes no banco de dados devem ter suas exceções devidamente tratadas como o uso de blocos `try...catch()`.

## Extensibilidade
Devido a baixa complexidade, não observou-se o uso de extensibilidade no projeto. Sendo assim, esta não foi implementada.
## Reuso
Além dos *getters* e *setters* presentes em cada classe, não foi identificado reuso dos métodos desenvolvidos. 
