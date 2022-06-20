<template>
 

  <div class="card-container">
    <div class="card-content">
        <div class="card-header">
            <form v-on:submit.prevent="getWeather">
                <input 
                    type="text" 
                    placeholder="Votre Ville" 
                    v-model="citySearch" 
                    autocomplete="off"/>
            </form>
        </div>
        <div class="card-body">
            <h1 class="info">{{ cityname }},{{ country }}</h1>

            <h2> <span class="temperature">{{ temperature }}°C</span></h2>
            <h5>{{ description }}</h5>
            <div class="min-max-temp">
                <h6>{{ minTemp }}°C<span class="material-icons">
south
</span>
</h6>
                <h6>{{ maxTemp }}°C<span class="material-icons">
north
</span></h6>
            </div>
        </div>
        <div class="card-footer">
            <div class="feel-like">
                <h3>Ressentie</h3>
                <h2>{{ feelLike }}°C</h2>
            </div>
            <div class="humidity">
                <h3>Humidité</h3>
                <h2>{{ humidity }} %</h2>
            </div>
        </div>
    </div>
  </div>
</template>

<script>


export default {
    name: 'HomeMain',
    data() {
        return {
            CLEAPI: '02cbe64be4170d5d61a933b7636668cd',
            citySearch: "",
            cityname: "Paris",
            country: "FR",
            temperature: 27,
            description: 'Ensoleillé',
            minTemp: 20,
            maxTemp: 28,
            feelLike:26,
            humidity:55,
        }
    },

    methods: {
        getWeather: async function () {
            console.log(this.citySearch)
            const url = `http://api.openweathermap.org/data/2.5/weather?q=${this.citySearch}&appid=${this.CLEAPI}&exclude=minutely&units=metric&lang=fr`

            const response = await fetch(url);
            const data = await response.json();
            console.log(data)
            this.citySearch = "";
            this.cityname = data.name;
            this.country = data.sys.country;
            this.temperature = Math.round(data.main.temp);
            this.description = data.weather[0].description;
            this.minTemp = Math.round(data.main.temp_min);
            this.maxTemp = Math.round(data.main.temp_max);
            this.feeLike = Math.round(data.main.feels_like);
            this.humidity = Math.round(data.main.humidity);
        }
    },
    
}
</script>

<style lang="scss">
    
    
    .card-container{
        
        width: 400px;
        height: 600px;
        margin: auto;
        overflow: hidden;
        border-radius: 15px;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
        .card-content{
            width: 100%;
            height: 100%;
            
            display: flex;
            flex-direction: column;
            .card-header{
                height: 10%;
                width: 100%;
                display: flex;
                align-items: center;
                justify-content: center;
                form{
                    width:95%;
                    border: 1px solid rgb(174, 174, 174);
                    border-radius: 15px;
                }
                input{
                    background: none;
                    height: 35px;
                    border: none;
                    width: 100%;
                    font-size: 18px;

                    &:focus{
                        outline: none;
                    }
                }
            }

            .card-body{
                
                display: flex;
                flex-direction: column;
                justify-content: space-between;
                align-items: center;
                width: 100%;
                height: 70%;
                color: rgb(1, 1, 26);
                .info{
                    color: rgb(1, 1, 26);
                }
                .min-max-temp{
                    
                    display: flex;
                    justify-content: space-around;
                    width: 60%;
                    color: rgb(1, 1, 26);
                    h6{
                        display: flex;
                        align-items: center;
                        margin: 0;
                        font-size: 24px;
                    }
                }

                .temperature{
                    border: 1px solid rgba(0, 0, 0, 0.168);
                    height: 170px;
                    width: 170px;
                    border-radius: 50%;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    font-size:54px;
                    color: rgb(1, 1, 26);
                }
            }

            .card-footer{
                height: 30%;
                width: 100%;
                display: flex;
                color: rgb(1, 1, 26);
                justify-content: space-around;
            }
        }


    }


</style>