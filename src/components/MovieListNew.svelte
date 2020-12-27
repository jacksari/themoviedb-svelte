<script>
    import {onMount} from 'svelte'
    import MovieListItem from "./MovieListItem.svelte";

    let movies = []
    onMount(async () => {
        let res = await fetch('https://api.themoviedb.org/3/movie/now_playing?api_key=00c2d56408907405dc1302cb38d24592&language=es-ES&page=1');
        let pelis = await res.json()
        movies = pelis.results

        //console.log(movies)
    })
</script>

<style lang="scss">
  .movie-list-over{
    overflow-y: scroll;
    height: 600px;
    text-align: center;
    &::-webkit-scrollbar{
      width: 7px;
      background: #fa807280;
      &-thumb{
        background: salmon;
        border-radius: 10px;
      }
    }


  }
  .title{
    background: cornflowerblue;
    color: white;
    padding: 10px;
    text-align: center;
    border-top-left-radius: 20px;
    border-top-right-radius: 20px;

  }
  .card-list{
    margin: 0px 40px;
  }

</style>
<div class="card-list">
    <div class="title">
        <h2>Películas Nuevas</h2>
    </div>
    <div class="movie-list-over">

        {#each movies as movie}
            <MovieListItem movie={movie}/>
        {/each}
    </div>
</div>
