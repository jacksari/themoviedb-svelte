<script>
    export let movie;
    const {title,overview,id} = movie
    let url = `https://image.tmdb.org/t/p/w500${movie.backdrop_path}`
    let href = `/movie/${id}`;
</script>

<style lang="scss">
    .movie-list{
      border-bottom: 1px solid darkred;
      border-left: 1px solid darkred;

        padding: 10px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        img{
            height: 50px;
            width: 50px;
          border-radius: 50%;
        }
      h2{
        margin: 0;
      }
    }
    a{
      text-decoration: none;
    }
</style>


<a rel=prefetch  href={href}>
    <div class="movie-list">
        <img src={url} alt="">
        <h2>{movie.title}</h2>
    </div>
</a>
