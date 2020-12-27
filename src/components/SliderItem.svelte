<script>
    export let movie;
    const {title,overview} = movie
    //console.log(movie)
    let url = `https://image.tmdb.org/t/p/original${movie.backdrop_path}`
    //console.log(movie)
</script>

<style lang="scss">
    .slide-content{

        height: 100%;
        background-size: cover;
        background-repeat: no-repeat;
        background-position: center top;
        display: flex;
        justify-content: center;
        align-items: flex-end;
        .content{
          text-align: center;
          background: #333333cc;
            color: white;
            border-radius: 20px;
            width: 50%;
            height: auto;
            padding: 10px;
          margin-bottom: 30px;
          h1{
            font-weight: bold;
          }
          p{
            font-weight: lighter;
          }
        }
    }
</style>

<div class="slide-content" style="background-image: url('{url}')">
    <div class="content">
        <h1>{title}</h1>
        <p>{overview}</p>
    </div>
</div>


