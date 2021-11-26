function movieSelected(id) {
  sessionStorage.setItem('movieId', id);
  window.location = 'movie.html';
  return false;
}

function getMovie() {
  let movieId = sessionStorage.getItem('movieId');
  
  
  axios.get('http://www.omdbapi.com?i='+movieId+'&apikey=6149a617')
    .then((response) => {
      console.log(response);
      let movie = response.data;
      
      let output = `
        <div class="row">
          <div class="col-md-4">
            <img src="${movie.Poster}" class="thumbnail">
          </div>
          <div class="col-md-8">
            <h2>${movie.Title}</h2> 
            <ul class="list-group">
              <li class="list-group-item"><b>Genre: </b>${movie.Genre}</li>
              <li class="list-group-item"><b>Released: </b>${movie.Released}</li>
              <li class="list-group-item"><b>Rated: </b>${movie.Rated}</li>
              <li class="list-group-item"><b>IMDB Rating: </b>${movie.imdbRating}</li>
              <li class="list-group-item"><b>Director: </b>${movie.Director}</li>
              <li class="list-group-item"><b>Actors: </b>${movie.Actors}</li>
            </ul>
          </div>
        </div>
        <div class="row">
          <div class="well">
            <h3>Plot</h3>
            ${movie.Plot}
            <hr>
            <a href="http://imdb.com/title/${movie.imdbID}" target="_blank" class="btn btn-primary">View IMDB</a>
            <a href="index.html" class="btn btn-light">Go Back to Search</a>
          </div>
        </div>
      `;
      
      $('#movie').html(output);
    })
    .catch((err) => {
      console.log(err);
    });      
 }  




const app = Vue.createApp({

    data() {
    return {
      info: null,
      detalhes:null
    }
  },
  created() {
  
    setTimeout(() => this.search('spider'), 50);
    },
    methods:{
   
        search:function(filme){
            axios.get('http://www.omdbapi.com?s='+filme+'&apikey=6149a617')
    .then((response) => {
      console.log(response);
      let movies = response.data.Search;
      let output = '';
      $.each(movies, (index, movie) => {
        output += `
          <div class="col-md-4">
            <div class="well text-center">
              <img src="${movie.Poster}">
              <h5>${movie.Title}</h5>
              <a onclick="movieSelected('${movie.imdbID}')" class="btn btn-primary mb-3" href="movie.html">Ver mais</a>
              
            </div>
          </div>
        `;
      });
      
      this.info=$('#movies').html(output);
    })

     
        },

        movieSelected:function(id) {
          alert('dd')
          sessionStorage.setItem('movieId', id);
          window.location = 'movie.html';
          return false;
        },
        getMovie:function() {
          let movieId = sessionStorage.getItem('movieId');
          
          
          axios.get('http://www.omdbapi.com?i='+tt1228705+'&apikey=6149a617')
            .then((response) => {
              console.log(response);
              let movie = response.data;
              
              let output = `
                <div class="row">
                  <div class="col-md-4">
                    <img src="${movie.Poster}" class="thumbnail">
                  </div>
                  <div class="col-md-8">
                    <h2>${movie.Title}</h2> 
                    <ul class="list-group">
                      <li class="list-group-item"><b>Genre: </b>${movie.Genre}</li>
                      <li class="list-group-item"><b>Released: </b>${movie.Released}</li>
                      <li class="list-group-item"><b>Rated: </b>${movie.Rated}</li>
                      <li class="list-group-item"><b>IMDB Rating: </b>${movie.imdbRating}</li>
                      <li class="list-group-item"><b>Director: </b>${movie.Director}</li>
                      <li class="list-group-item"><b>Actors: </b>${movie.Actors}</li>
                    </ul>
                  </div>
                </div>
                <div class="row">
                  <div class="well">
                    <h3>Plot</h3>
                    ${movie.Plot}
                    <hr>
                    <a href="http://imdb.com/title/${movie.imdbID}" target="_blank" class="btn btn-primary">View IMDB</a>
                    <a href="index.html" class="btn btn-light">Go Back to Search</a>
                  </div>
                </div>
              `;
              
              this.detalhes=$('#movie').html(output);
            })
            .catch((err) => {
              console.log(err);
            });      
         }  

        
       

        
    }
  }).mount('#film')



  

