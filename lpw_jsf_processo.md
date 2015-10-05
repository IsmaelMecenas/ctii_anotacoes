# Processo para construir sistemas com JavaServer Faces, Primefaces e Hibernate

## Camada de negócio

* Fazer o diagrama de classes (UML)
* Criar o projeto no NetBeans:
  * Escolha Java Web Application
  * Dê um nome ao projeto
  * Selecione a versão do Java e o servidor HTTP (usamos Tomcat)
  * Selecione o JavaServer Pages
    * Em Components selecione PrimeFaces 
  * Selecione Hiberntate
    * Escolha a opção para criar uma nova conexão
    * Escolha o driver do seu DBMS
    * host=localhost
    * A porta depende do DBMS. No postgresql é 5432
    * Entre no seu DBMS e crie uma base de dados
    * Coloque o nome da base no campo database
  * Finalize a contrução do projeto
* Crie um pacote negocio
* Programe as classes de acordo com seu diagrama

## Colocar anotações de JSF

## Fazer a interface de repositório genérico

## Fazer o DaoManager do Hibernate

## Fazer os contrutores (builders)

## Implementar o repositório para Banco de Dados

* Crie um pacote para colocarar as implementações
* Crie uma classe 
* Crie os métodos
  * Inserir
  * Alterar
  * Remover
  * Recuperar
  * Recupear todos
* Esses métodos delegam as tarefas para o DaoManager
* Os métodos inserir, alterar e remover recebem o objeto
* Os métodos recuperar e recuperar todos usar HQL para recuperar
  * recuperar: "from <Classe> where codigo=" + codigo
  * recuperarTodos: "from <Classe>"
* O método recuperar recebe o codigo/id do objeto. Depois de chamar do Dao para pegar o HQL ele recebe uma lista e deve pegar o primeiro elemento
* 

## Colocar anotações de JSF nos builders

* A anotação @ManagedBean permite que você acesse uma instância da classe pelas páginas JSF. Coloca-se o atributo name com o nome.
* A anotaçõa @RequestScoped faz com o que um objeto novo seja criaddo a cada requisição
* 

## Criar controladores

## Criar as páginas de JSF

### Criando páginas de cadastro.

# Parte de Ismael

# Untitled

Procedimentos para a criação de um projeto em LPW
1° Declara o Entity e o Table

* declara antes do class
* @ Entity e @ Table

2° Declara o Id e o GeneratedValue

* @Id obrigatório e o @GeneratedValue antes da primaryKey
* se quiser colocar o @Column (length = 20[tamanho opcional]) private string variável;

3° Se precisar colocar o @ManyToMany e etc, se tiver alguma lista.

4° Colocar os construtores

* @Deprecated no construtor vazio.

5° Onde tiver lista, iniciar dentro do construtor

6° É necessário criar um banco de dados.

* Create database NomeDoBanco;

7° Alterar o hibernate config do projeto

* altera o nome do banco de dados no connection.url depois do 3306/nome?
* coloca um connection.password, se o banco de dados tiver senha.

8° Fazer o mapeamento das classes

* <mapping class=”cordenadas da classe”/>

9°Copia o Dao e o executa com o drivr do JDBC o mysql (importa da biblioteca)

* o Dao é o responsável por gerenciar o banco de dados, pode dar erro nos many’s.

10° Criar os repositórios (comportamentos)

* criar um novo pacote, esse pacote normalmente será chamado de comportamentos
* criar uma interface (repositório genérico)
* criar outros repositórios, mas dessa vez serão classes
* Essas novas classes implementarão o repositório genérico.
* dentro delas faz o CRUD, segue o passo a passo:
* ->
* @Override
* public void inserir(Classe o) {
*  DaoManagerHiber.getInstance().persist(o);
*  }
*  @Override
*  public void alterar(Classe o) {
*  DaoManagerHiber.getInstance().update(o);
*  }
*  @Override
*  public Classe recuperar(int codigo) {
*  return (Classe) DaoManagerHiber.getInstance().recover("from NomeDaClasse where codigo="+codigo).get(0);
*  }
*  @Override
*  public void excluir(Classe o) {
*  DaoManagerHiber.getInstance().delete(o);
*  }
*  @Override
*  public List<Classe> recuperarTodos() {
*  return DaoManagerHiber.getInstance().recover("from NomeDaClasse");

11) Inserir o JSF

* @ManagedBean (name =”bClasse”), serve para identificar as classes no JSF
* @RequestScoped
* fazer isso nos Builders, antes do class

12)Criar os controladores, mas como?

* criar um pacote, esse pacote normalmente será chamado de controladores
* criar classe
* criar um objeto, private RepositorioGenerico<classe>
* criar um construtor
* colocar os métodos
* Notações: @ManagedBean , @SessionScoped , colocar um objeto no escopo da seção.
* exemplo de um controlador:


@ManagedBean

@SessionScoped

public class ControladorClasse {



 private RepositorioGenerico<Classe> repositorioClasse = null;



 public ControladorClasse(){

 this.repositorioClasse = new RepositorioClasseImplDB();

 }

 public void inserir(Classe classe){

 this.repositorioClasse.inserir(classe);

 }



 public void alterar(Classe classe){

 this.repositorioConsole.alterar(console);

 }

 public Classe recuperar(int codigo){

 return this.repositorioClasse.recuperar(codigo);

 }

 public List<Classe> recuperarTodos(){

 return this.repositorioClasse.recuperarTodos();

 }

 public void excluir(Classe classe){

 this.repositorioConsole.excluir(console);

 }

}


13) Criar página cadastro, mas como?

* Vai na pasta páginas web.
* Cria uma página JSF
* No body, criar o form, como? -> <h:form id=”NomeDoID”></h:form>
* Dentro do form, cria o fieldset, faz uma caixa com uma borda superior na pag da web.<p:fieldset></p:fieldset>
* - Dentro do fieldset cria um panelgrid.
* exemplo:



<h:body>

 <h:form id="formulario">

 <p:fieldset legend="Cadastro de Console">

 <p:panelGrid columns="2">

 <h:outputText value ="Nome"/>

 <p:inputText value="#{bConsole.nome}"

 </p:panelGrid>

 </p:fieldset>

 </h:form>

</h:body>
