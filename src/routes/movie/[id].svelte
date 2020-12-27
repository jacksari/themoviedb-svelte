<script context="module">
    export async function preload({ params }) {
        // the `slug` parameter is available because
        // this file is called [slug].svelte
        const res = await this.fetch(`https://api.themoviedb.org/3/movie/${params.id}?api_key=00c2d56408907405dc1302cb38d24592&language=es-ES`)
        const data = await res.json();

        if (res.status === 200) {
            return { movie: data };
        } else {
            this.error(res.status, data.message);
        }
    }
</script>

<script>


    import {onMount} from "svelte";

    export let movie;
    //console.log(movie)

    const {poster_path,title,overview,id,homepage, backdrop_path, release_date,tagline,vote_average,genres} = movie;
    let fondo = `https://image.tmdb.org/t/p/original${backdrop_path}`
    let poster = `https://image.tmdb.org/t/p/original${poster_path}`
    import Modal from '../../components/Modal.svelte'

    let showModal = false;

    let movies = []
    let urlVideo
    onMount(async () => {
        let res = await fetch(`https://api.themoviedb.org/3/movie/${id}/videos?api_key=00c2d56408907405dc1302cb38d24592&language=es-ES`);
        let pelis = await res.json()
        movies = pelis.results[0]


        //console.log(movies)
        if(movies != undefined){
            urlVideo = `https://www.youtube.com/embed/${movies.key}`
        }
    })





</script>


<style lang="scss">
    .movie-details{
        display: flex;
        padding: 40px 100px ;
        .movie-poster{
          flex: 0 1 40%;
          padding: 0 80px 0 80px;
          color: white;
          p{
            text-align: center;
            font-size: 20px;
          }
          .poster{
            border-radius: 20px;
            height: 600px;
            background-size: cover;
            background-repeat: no-repeat;
            background-position: center top;
          }
        }
      .movie-content{
        flex: 1;
        color: white;
        &-header{
          h1{
            font-weight: bold;
            font-size: 30px;
          }
          display: flex;
          justify-content: space-between;

          .icon{
            font-size: 10px;
            height: 40px;
            cursor: pointer;
            transition: all 0.5s ease;
            &:hover{
              color: salmon;
              transform: scale(1.2);

            }
          }
        }
        &-body{
            h5{
              font-size: 25px;
              font-weight: bold;
            }
          &-generos{
            display: flex;
            p{
              background: salmon;
              padding: 5px 10px;
              margin: 10px;
              border-radius: 20px;
              font-weight: bold;
            }
          }
          &-release{
            display: flex;
            justify-content: space-between;
            p{
              font-size: 25px;
              font-weight: bold;
              span{
                font-size: 20px;
                font-weight: lighter;
              }
            }
          }
        }
      }
    }
    .video{
      display: flex;
      justify-content: center;
    }
</style>

<svelte:head>
    <title>{title}</title>
</svelte:head>

<div class="movie-details" style="background-image: linear-gradient(rgba(0,0,0,0.8),rgba(0,0,0,0.8)),url('{fondo}')">
    <div class="movie-poster" >
        <div class="poster" style="background-image: url('{poster}')"></div>
        <p>{tagline}</p>
    </div>
    <div class="movie-content">
        <div class="movie-content-header">
            <h1>{title}</h1>
            {#if movies != undefined}
                <svg on:click="{() => showModal = true}" class="w-6 h-6 icon" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z" clip-rule="evenodd"></path></svg>
            {/if}

        </div>
        <div class="movie-content-body">
            <div class="movie-content-body-release">
                <p>Puntaje: <span>{vote_average}</span></p>
                <p>Fecha: <span>{release_date}</span></p>
            </div>
            <p>{overview}</p>
            <h5>Generos</h5>
            <div class="movie-content-body-generos">
                {#each genres as genero}
                    <p>{genero.name}</p>
                {/each}
            </div>

        </div>
    </div>
</div>

{#if showModal}
    <Modal on:close="{() => showModal = false}">

        <div class="video" slot="video">
            {#if movies != undefined}
                <iframe width="900" height="500" src={urlVideo} frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
            {/if}

        </div>
    </Modal>
{/if}

