#[Douglas Augusto](http://github.com/DouglasAugustoJunior)- Outros projetos. # 
 
 
![VERSÃO DO SW](https://img.shields.io/badge/Version-1.0-blue.svg)
 
![LINGUAGEM FINALIDADE](https://img.shields.io/badge/javascript-system-orange.svg)
 
O **Buscar Filmes** é um projeto simples que utilizei para praticar meus conhecimentos em JS. **[Projeto Online](https://douglasaugustojunior.github.io/BuscaFilmesJS/)**

![Imagem](https://github.com/DouglasAugustoJunior/BuscaFilmesJS/blob/master/images/Busca.PNG?raw=true)

![Imagem](https://github.com/DouglasAugustoJunior/BuscaFilmesJS/blob/master/images/Detalhe.PNG?raw=true)


 
Desenvolvido em HTML5,CSS3,Bootstrap e JS, ele traz diversas situações interessantes para utilizar diversos recursos, incluindo a API Axios.
 
## Busca de filmes
 

        function buscarFilmes(filmepesquisa){
      axios.get('http://www.omdbapi.com/?apiKey=APIKeyHere&s='+filmepesquisa) // busca o titulo do filme inserido na API
      .then(function (response) {
        console.log(response); // mostra resultados no log
          var filmes = response.data.Search; //data e search são as ramificações do objeto json que o response tras
          var mostrarfilmes = ''; // armazena o resultado da busca em HTML
          for (var i=0;i<filmes.length;i++){ //percorre todos os filmes encontrados
            mostrarfilmes+=`
                            <div class="col-md-6">
                                <div class="thumbnail">
                                    <img src="${filmes[i].Poster} class="img-thumbnail">
                                    <h4>${filmes[i].Title}</h4>
                                    <p><a href="#" class="btn btn-dark" role-"button" onclick="filmeDetalhes('${filmes[i].imdbID}')">Ver detalhes</a></p>
                                </div>
                            </div>`; // monta visualização do filme com bootstrap e html
          }
          document.getElementById('filmes').innerHTML = mostrarfilmes; // envia os filmes para a div filmes
      }) 
      .catch(function (error) { // caso retorne algum erro
        console.log('Ocorreu um erro ao buscar:'+error);
        alert('OPS!Tente novamente por favor.');
      });
    }

 

 
##Detalhes Filmes
 

        function filmeDetalhes(id){
        //alert('ID escolhido:'+id);
        sessionStorage.setItem('filmeID',id); // armazena ID na seção do navegador
        window.location = 'detalhes.html'; // vai para a página detalhes
        return false; // para função
    }
    
    function mostraFilmes(){
        var filmeID = sessionStorage.getItem('filmeID');
        axios.get('http://www.omdbapi.com/?apiKey=APIKeyHere&i='+filmeID) // busca o filme pelo ID salvo na seção
      .then(function (response) {
        var filme = response.data; // armazena filme buscado
        console.log(filme); // exibe filme no log
        var mostrarfilme=`
                            <div class="col-md-6">
                                <img src="${filme.Poster} class="img-responsive">
                                <h3><strong>${filme.Title}</strong></h3>        
                            </div>
                            <div class="col-md-6">
                                <div class="well clearfix">
                                    <ul class="list-group">
                                        <li class="list-group-item"><strong>Gênero: ${filme.Genre}</strong></li>
                                        <li class="list-group-item"><strong>Atores: ${filme.Actors}</strong></li>
                                        <li class="list-group-item"><strong>Pais: ${filme.Country}</strong></li>
                                        <li class="list-group-item"><strong>Diretor: ${filme.Director}</strong></li>
                                        <li class="list-group-item"><strong>Produção: ${filme.Production}</strong></li>
                                        <li class="list-group-item"><strong>Duração: ${filme.Runtime}</strong></li>
                                        <li class="list-group-item"><strong>Ano: ${filme.Year}</strong></li>
                                        <li class="list-group-item"><strong>Nota: ${filme.imdbRating}</strong></li>
                                        <li class="list-group-item"><strong>Votos: ${filme.imdbVotes}</strong></li>
                                    </ul>
                                    <h3>Descrição</h3>
                                     ${filme.Plot}
                                     <hr>                                        
                                         <a href="http://imdb.com/title/${filme.imdbID}" target="_blank" class="btn btn-success" pull-left>Trailler</a>
                                         <a href="index.html" target="_blank" class="btn btn-dark" pull-right>Pesquisar novamente</a>
                                     </hr>
                                </div>
                            </div>`; // monta visualização do filme com bootstrap e html
            document.getElementById('filme').innerHTML = mostrarfilme; // envia os filmes para a div filmes
        
      }) 
      .catch(function (error) { // caso retorne algum erro
        console.log('Ocorreu um erro ao buscar:'+error);
        alert('OPS!Tente novamente por favor.');
      });
    }

Para mais informações acesse [meus repositórios](http://github.com/DouglasAugustoJunior).
