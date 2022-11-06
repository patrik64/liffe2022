<script>
  import Youtube from "svelte-youtube-embed";

  export let data;

  let id = '';
  for(let x in data) {
    id += data[x];
  }

  import movies from "$lib/data/movies.json";

  let movie = movies[id - 1];

  let getWeekday = (date) => {
    if(date === "9.11.2022") {
      return "Wednesday";
    } else if (date === "10.11.2022") {
      return "Thursday";
    } else if (date === "11.11.2022") {
      return "Friday";
    } else if (date === "12.11.2022") {
      return "Saturday";
    } else if (date === "13.11.2022") {
      return "Sunday";
    } else if (date === "14.11.2022") {
      return "Monday";
    } else if (date === "15.11.2022") {
      return "Tuesday";
    } else if (date === "16.11.2022") {
      return "Wednesday";
    } else if (date === "17.11.2022") {
      return "Thursday";
    } else if (date === "18.11.2022") {
      return "Friday";
    } else if (date === "19.11.2022") {
      return "Saturday";
    } else if (date === "20.11.2022") {
      return "Sunday";
    }

    return "Bugday";
  }

  let formatShow = (show) => {
    let str = show.date + " - " + getWeekday(show.date) + " - " + show.time + "h - " + show.kino;
    return str;
  };

  let getUrl = () => {
    return "https://liffe2022.vercel.app/" + id;
  }

  let getImageUrl = () => {
    return "https://liffe2022.vercel.app/images/movies/" + movie.image;
  }

  let getOgDescription = () => {
    let ret = "IMDB: " + movie.score;
    ret += '\n';
    for(let s in movie.shows) {
      let show = movie.shows[s];
      ret += show.date + " - " + getWeekday(show.date) + " - " + show.time + "h - " + show.kino;
      ret += '\n';
    }
    return ret;
  }

</script>

<svelte:head>
   <meta property="og:site_name" content="liffe2022" />
   <meta property="og:locale" content="en" />
   <meta property="og:url" content={getUrl()} />
   <meta property="og:type" content="website" />
   <meta property="og:title" content={movie.name} />
   <meta property="og:description" content={getOgDescription()} />
   <meta property="og:image" content={getImageUrl()} />
   <meta property="og:image:width" content="400" />
   <meta property="og:image:height" content="400" />
   <meta property="og:image:alt" content={movie.name} />
</svelte:head>
  
{#if movie}
<div class="my-10 mx-auto lg:w-1/2 bg-white shadow overflow-hidden sm:rounded-lg">
  <div class="px-4 py-5 sm:px-6">
    <div class="text-2xl leading-6 font-medium">{movie.name}</div>
    {#if movie.image && movie.image.length > 0}
      <img class="my-4 object-contain" src={`/images/movies/${movie.image}`} alt="" />
      <div class="text-xss text-gray-500">&copy; imdb</div>
    {/if}
  </div>
  <div class="border-t border-gray-200 px-4 py-5 sm:p-0">
    <dl class="sm:divide-y sm:divide-gray-200">
      <div class="py-4 sm:py-5 sm:grid sm:grid-cols-4 sm:gap-4 sm:px-6">
        <dt class="text-sm font-medium text-gray-600">Name</dt>
        <dd class="mt-1 text-sm text-gray-600 sm:mt-0 sm:col-span-2">{movie.name}</dd>
      </div>
      <div class="py-4 sm:py-5 sm:grid sm:grid-cols-4 sm:gap-4 sm:px-6">
        <dt class="text-sm font-medium text-gray-600">SLO Name</dt>
        <dd class="mt-1 text-sm text-gray-600 sm:mt-0 sm:col-span-2">{movie.sloname}</dd>
      </div>
      <div class="py-4 sm:py-5 sm:grid sm:grid-cols-4 sm:gap-4 sm:px-6">
        <dt class="text-sm font-medium text-gray-600">ENG Name</dt>
        <dd class="mt-1 text-sm text-gray-600 sm:mt-0 sm:col-span-2">{movie.engname}</dd>
      </div>
      <div class="py-4 sm:py-5 sm:grid sm:grid-cols-4 sm:gap-4 sm:px-6">
        <dt class="text-sm font-medium text-gray-600">IMDB Score</dt>
        <dd class="mt-1 text-sm text-gray-600 sm:mt-0 sm:col-span-2">{movie.score}</dd>
      </div>
      <div class="py-4 sm:py-5 sm:grid sm:grid-cols-4 sm:gap-4 sm:px-6">
        <dt class="text-sm font-medium text-gray-600">IMDB</dt>
        <dd class="mt-1 text-sm text-gray-600 sm:mt-0 sm:col-span-2"><a href={movie.links[1].lvalue} class="hover:text-black">{movie.links[1].lvalue}</a></dd>
      </div>
      <div class="py-4 sm:py-5 sm:grid sm:grid-cols-4 sm:gap-4 sm:px-6">
        <dt class="text-sm font-medium text-gray-600">Liffe</dt>
        <dd class="mt-1 text-sm text-gray-600 sm:mt-0 sm:col-span-2"><a href={movie.links[0].lvalue} class="hover:text-black">{movie.links[0].lvalue}</a></dd>
      </div>
      {#each movie.shows as show, showIdx}
          <div class="py-4 sm:py-5 sm:grid sm:grid-cols-4 sm:gap-4 sm:px-6">
              <dt class="text-sm font-medium text-gray-600">Show {showIdx+1}</dt>
              <dd class="mt-1 text-sm text-gray-600 sm:mt-0 sm:col-span-2">{formatShow(show)}</dd>
          </div>
      {/each}
      <div class="py-4 sm:py-5 sm:grid sm:grid-cols-4 sm:gap-4 sm:px-6">
          <dt class="text-sm font-medium text-gray-600">Trailer</dt>
          <dd class="mt-1 text-sm text-gray-600 sm:mt-0 sm:col-span-2"><Youtube id="{movie.links[2].lvalue}" /></dd>
        </div>
    </dl>
  </div>
</div>
{/if}