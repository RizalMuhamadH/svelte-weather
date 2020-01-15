<script>
  let API_KEY = "257b69d3850c608a8431b5862d7d8f69";
  let BASE_URL = "https://api.openweathermap.org/data/2.5/";
  let query = "";
  let weather;
  
	function fetchWeather(event) {
		if (event.key === 'Enter') {
			fetch(BASE_URL + "weather?q="+query+"&units=metric&APPID="+API_KEY).then(r => r.json()).then(res => {
				weather = res;
				// console.log(weather);
				// console.log(weather.name);
				
				// return { weather };
			});
			
		}
	}

	function dateBuilder () {
		let d = new Date();
		let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
		let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
		let day = days[d.getDay()];
		let date = d.getDate();
		let month = months[d.getMonth()];
		let year = d.getFullYear();
		return `${day} ${date} ${month} ${year}`;
    }

</script>
<style>
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	div#app {
		padding: auto;
		background-image: url('assets/cold-bg.jpg');
		background-size: cover;
		background-position: bottom;
		transition: 0.4s;
		height: 100%;
	}

	div#app.warm {
		background-image: url('assets/warm-bg.jpg');
	}

	.warp{
		padding: 30px;
	}

	.search-box {
		width: 100%;
		margin-bottom: 30px;
	}
	.search-box .search-bar {
		display: block;
		width: 100%;
		padding: 15px;

		color: #313131;
		font-size: 20px;
		appearance: none;
		border: none;
		outline: none;
		background: none;
		box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
		background-color: rgba(255, 255, 255, 0.5);
		border-radius: 0px 16px 0px 16px;
		transition: 0.4s;
	}
	.search-box .search-bar:focus {
		box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
		background-color: rgba(255, 255, 255, 0.75);
		border-radius: 16px 0px 16px 0px;
	}
	.location-box .location {
		color: #FFF;
		font-size: 32px;
		font-weight: 500;
		text-align: center;
		text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
	}
	.location-box .date {
		color: #FFF;
		font-size: 20px;
		font-weight: 300;
		font-style: italic;
		text-align: center;
	}
	.weather-box {
		text-align: center;	
	}
	.weather-box .temp {
		display: inline-block;
		padding: 10px 25px;
		color: #FFF;
		font-size: 102px;
		font-weight: 900;
		text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
		background-color:rgba(255, 255, 255, 0.25);
		border-radius: 16px;
		margin: 30px 0px;
		box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
	}
	.weather-box .weather {
		color: #FFF;
		font-size: 48px;
		font-weight: 700;
		font-style: italic;
		text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
	}

  /* @media (min-width: 480px) {
    h1 {
      font-size: 4em;
    }
  } */
</style>

<svelte:head>
  <title>Weathers</title>
</svelte:head>

<div id="app" class="{weather != null && weather.main.temp > 16 ? 'warm' : ''}">
	<div class="warp">
		<div class="search-box">
			<input type="text" bind:value={query} class="search-bar" on:keydown={fetchWeather} placeholder="Search..." />
		</div>
		{#if weather != null && weather.cod != "404"}
			<div class="weather-wrap">
				<div class="location-box">
					<div class="location">{weather.name}, {weather.sys.country}</div>
					<div class="date">{dateBuilder()}</div>
				</div>
				<div class="weather-box">
					<div class="temp">{Math.round(weather.main.temp)}&#176;C</div>
					<div class="weather">{weather.weather[0].main}</div>
				</div>
			</div>
		{/if}
	</div>
</div>
