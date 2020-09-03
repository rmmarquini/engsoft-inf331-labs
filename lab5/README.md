# LAB_05 - Web como Plataforma e Subcomponentes

> Informações sobre as atividades exigidas no laboratório neste [LINK](https://github.com/santanche/component2learn/tree/master/labs/05-web_subcomponentes).

## :arrow_forward: Aluno
* Rafael Mardegan Marquini

## :hammer: Conceitos, Ferramentas e Tecnologias
* Componentização de Software
* Design Pattern: MVC
* [UML](https://www.uml.org/)
* Componentes Web
* [Reactjs](https://www.reactjs.org)
* [Axios](https://github.com/axios/axios)
* [Codepen](https://www.codepen.io)

## :pencil: Tarefas

### :construction: Tarefa 1:
> Escolha um conjunto de componentes do laboratório passado e os represente na forma de componentes com sub-comopnentes.

### :heavy_check_mark: Tarefa 2:
> Crie uma conta no [Codepen](https://www.codepen.io), copie o código do exemplo [React 03 - Componente Barra](https://codepen.io/santanche/pen/KKzmbwR) para a sua conta e construa um exemplo de componente adaptando o exemplo apresentado. Por se tratar de programação em JavaScript, podem ser feitas adaptações bastante simples.

#### Resultado da atividade
* Construí um exemplo que utiliza a biblioteca **Axios** para buscar meus repositórios do Github e retorná-los numa tabela na DOM.
* [Codepen](https://codepen.io/rmmarquini/pen/NWNaOLL)

#### Códigos-fonte

**HTML**

~~~HTML
<div id="app"></div>
~~~

**CSS**

~~~CSS
.container h1 {
  text-align: center;
}

.content {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 2.5rem auto 0;
}

.content table {
  max-width: 80%;
  border-collapse: collapse;
}

.content > table > thead > tr > th,
.content > table > tbody > tr > td {
  text-align: left;
  padding: 0.25rem;
}

.content > table > thead > tr > th:first-child,
.content > table > tbody > tr > td:first-child {
  width: 27.5%;
}

.content > table > thead > tr {
  background-color: #FAC000;
}

.content > table > tbody > tr:nth-child(2n+1) {
  background-color: #F4F4F4;
}
~~~

**Javascript** 

~~~JS
class Repositories extends React.Component {
    /**
     * Construtor da classe contendo o estado onde serão armazenados os repositórios
     */
    constructor(props) {
        super(props);
        this.state = {repos: []};
    }

    /**
     * Método lifecycle para criar a instância do componente na DOM
     */
    componentDidMount() {
        axios.get('https://api.github.com/users/rmmarquini/repos')
            .then(response => this.setState({ repos: response.data }))
            .catch(error => console.log(error));
    }

    /**
     * Retorno do componente
     */
    render() {
        return (
            <div class="container">
                <h1>Repositórios Github de Rafael</h1>
            
                <div class="content">
                    <table>
                    <thead>
                        <tr>
                        <th>Repositório</th>
                        <th>Descrição</th>
                        </tr>
                    </thead>
                    <tbody>
                        {this.state.repos.map(repo => 
                            <tr key={repo.id}>
                                <td>{repo.name}</td>
                                <td>{repo.description}</td>
                            </tr>
                        )}
                    </tbody>
                    </table>
                </div>
            
            </div>
        );
    }
}

/**
* Renderizando o componente
*/
ReactDOM.render(<Repositories />, document.querySelector('#app'));
~~~


---
Made with :coffee: by Rafa Mardegan.