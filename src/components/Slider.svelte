<script>

    import {Swipe, SwipeItem} from "svelte-swipe"; // gzipped 3.37 KB

    const swipeConfig = {
        autoplay: false,
        delay: 2000,
        showIndicators: true,
        transitionDuration: 1000,
        defaultIndex: 0,
    };

    import {onMount} from 'svelte'
    import SliderItem from "./SliderItem.svelte";

    let movies = []
    onMount(async () => {
        let res = await fetch('https://api.themoviedb.org/3/movie/popular?api_key=00c2d56408907405dc1302cb38d24592&language=es-ES&page=1');
        let pelis = await res.json()
        movies = pelis.results


        //console.log(movies)
    })

    let SwipeComp;

    function nextSlide(){
        SwipeComp.nextItem()
    }

    function prevSlide(){
        SwipeComp.prevItem()
    }

</script>

<style lang="scss">
  :root{
    --sv-swipe-indicator-active-color: red;

  }
  .swipe-holder{
    height: 500px;
    width: 100%;
  }
  .buttons-holder{
    position: absolute;
    width: 90%;
    margin: 10px auto;
    z-index: 100;
    top: 50%;
    left: calc(50% - 45%);
    display: flex;
    justify-content: space-between;
    button{
      background: #55555599;
      color: white;
      text-align: center;
      vertical-align: center;
      border: none;
      height: 50px;
      width: 50px;
      border-radius: 50%;
      padding: 8px;
      font-size: 15px;
      font-weight: bold;
      cursor: pointer;
    }

  }
  .slider{
    position: relative;
  }
</style>

<div class="slider">
    {#if movies.length > 0}
        <div class="swipe-holder">
            <Swipe {...swipeConfig} bind:this={SwipeComp}>
                {#each movies as movie,index}
                    <SwipeItem>
                        <SliderItem movie={movie}/>
                    </SwipeItem>
                {/each}
            </Swipe>
        </div>
        <div class="buttons-holder">
            <button type="button" on:click={prevSlide}>
                <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M9.707 16.707a1 1 0 01-1.414 0l-6-6a1 1 0 010-1.414l6-6a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l4.293 4.293a1 1 0 010 1.414z" clip-rule="evenodd"></path></svg>
            </button>
            <button type="button" on:click={nextSlide}>
                <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
            </button>
        </div>
    {/if}


</div>



