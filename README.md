# Criando-Uma-Wiki-de-Reposit-rios-do-GitHub-Com-React

Criar uma Wiki de repositórios do GitHub usando React é uma ótima maneira de aplicar seus conhecimentos de JavaScript e React, além de aprender sobre a interação com APIs. Aqui está um exemplo de como podemos começar:

1. **Crie um novo projeto React**:
   Você pode começar criando um novo projeto React usando `create-react-app`.

   ```bash
   npx create-react-app minha-wiki-github
   cd minha-wiki-github
   ```

2. **Instale as dependências necessárias**:
   Talvez você precise de bibliotecas como `axios` para fazer requisições HTTP.

   ```bash
   npm install axios
   ```

3. **Configure a API do GitHub**:
   Você pode usar o `axios` para consumir a API do GitHub e buscar os repositórios.

   ```javascript
   import axios from 'axios';

   const fetchRepos = async (username) => {
     try {
       const response = await axios.get(`https://api.github.com/users/${username}/repos`);
       return response.data;
     } catch (error) {
       console.error("Erro ao buscar repositórios", error);
     }
   };
   ```

4. **Liste os repositórios**:
   Crie componentes React para exibir a lista de repositórios.

   ```javascript
   import React, { useState, useEffect } from 'react';

   const RepoList = ({ username }) => {
     const [repos, setRepos] = useState([]);

     useEffect(() => {
       const getRepos = async () => {
         const reposData = await fetchRepos(username);
         setRepos(reposData);
       };

       getRepos();
     }, [username]);

     return (
       <ul>
         {repos.map(repo => (
           <li key={repo.id}>{repo.name}</li>
         ))}
       </ul>
     );
   };
   ```

5. **Estilize sua aplicação**:
   Use CSS ou bibliotecas de componentes como Material-UI para estilizar sua Wiki.

6. **Gerencie o estado da aplicação**:
   Se a sua aplicação crescer, considere usar o Context API ou Redux para gerenciar o estado global.

Lembre-se de ler a documentação da API do GitHub para entender melhor como você pode interagir com ela. 

Adicionar um campo de pesquisa na sua Wiki de repositórios do GitHub é uma ótima maneira de melhorar a usabilidade. Aqui está um exemplo de como podemos implementar isso em um projeto React:

1. **Crie um componente de campo de pesquisa**:
   Primeiro, crie um componente que inclua um input para os usuários digitarem suas buscas.

   ```javascript
   import React, { useState } from 'react';

   const SearchBar = ({ onSearch }) => {
     const [searchTerm, setSearchTerm] = useState('');

     const handleSearch = (event) => {
       setSearchTerm(event.target.value);
     };

     const handleSubmit = (event) => {
       event.preventDefault();
       onSearch(searchTerm);
     };

     return (
       <form onSubmit={handleSubmit}>
         <input
           type="text"
           placeholder="Digite o nome do repositório..."
           value={searchTerm}
           onChange={handleSearch}
         />
         <button type="submit">Pesquisar</button>
       </form>
     );
   };
   ```

2. **Integre o campo de pesquisa com a lista de repositórios**:
   No componente que lista os repositórios, você pode adicionar uma função para lidar com a busca e filtrar os resultados com base no termo de pesquisa.

   ```javascript
   import React, { useState, useEffect } from 'react';
   import { fetchRepos } from './services/github'; // Supondo que você tenha um arquivo de serviços

   const RepoList = ({ username }) => {
     const [repos, setRepos] = useState([]);
     const [filteredRepos, setFilteredRepos] = useState([]);

     useEffect(() => {
       const getRepos = async () => {
         const reposData = await fetchRepos(username);
         setRepos(reposData);
         setFilteredRepos(reposData);
       };

       getRepos();
     }, [username]);

     const handleSearch = (searchTerm) => {
       const filtered = repos.filter(repo =>
         repo.name.toLowerCase().includes(searchTerm.toLowerCase())
       );
       setFilteredRepos(filtered);
     };

     return (
       <>
         <SearchBar onSearch={handleSearch} />
         <ul>
           {filteredRepos.map(repo => (
             <li key={repo.id}>{repo.name}</li>
           ))}
         </ul>
       </>
     );
   };
   ```

3. **Atualize o estado com base na pesquisa**:
   Quando o usuário digita no campo de pesquisa e submete o formulário, o estado `filteredRepos` é atualizado para mostrar apenas os repositórios que correspondem ao termo de pesquisa.

Com esses passos, você terá um campo de pesquisa funcional que permite aos usuários filtrar os repositórios por nome. Lembre-se de ajustar os nomes das funções e variáveis conforme necessário para o seu projeto.

https://github.com/digitalinnovationone/trilha-react-desafio-2
