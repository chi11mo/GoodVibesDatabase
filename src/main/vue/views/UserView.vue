<template>
    <!-- partial -->
    <q-page padding>
    <body>
    <h1>Clubübersicht</h1>
    <h2>SAISON 2021-2022</h2>
    <!-- partial:index.partial.html -->
    <!-- Font | Optional-->
    <div class="container">
        <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Saira+Semi+Condensed:300,400,700"/>
        <!-- Wrapper | For this page - !!ignore-->
        <div v-for="user in users" :key="user.id">

            <div class="wrapper">
                <!-- *** fut-player-card ***-->
                <div class="fut-player-card">
                    <!-- Player Card Top-->
                    <div class="player-card-top">
                        <div class="player-master-info">
                            <div class="player-rating"><span>{{ user.id }}</span></div>
                            <div class="player-position"><span>RW</span></div>
                            <div class="player-nation"></div>
                            <div class="player-club"></div>
                        </div>

                        <div class="player-picture"><img id="twitchProfileImg" :src="user.imgUrl"
                                                         draggable="false"/>

                            <div class="player-extra"><span></span><span></span></div>
                        </div>
                    </div>
                    <!-- Player Card Bottom-->
                    <div class="player-card-bottom">
                        <div class="player-info">
                            <!-- Player Name-->
                            <div class="player-name"><span>{{ user?.name }}</span></div>
                            <!-- Player Features-->
                            <div class="player-features">
                                <div class="player-features-col"><span>
              <div class="player-feature-value">TWITCH</div>
              <div class="player-feature-title"></div></span><span>
              <div class="player-feature-value">DISCORD</div>
              <div class="player-feature-title"></div></span><span>
              <div class="player-feature-value">PSN</div>
                                    <div class="player-feature-title"></div></span><span>
              <div class="player-feature-value">Steam</div>
              <div class="player-feature-title"></div></span></div>

                                <div class="player-features-col"><span>
              <div class="player-feature-value"><a
                  href="https://www.twitch.tv/{{user.twitch}}">{{ user.twitch }}</a></div>
              <div class="player-feature-title"></div></span><span>
              <div class="player-feature-value">{{ user?.discord }}</div>
              <div class="player-feature-title"></div></span><span>
              <div class="player-feature-value"><a
                  href="https://psnprofiles.com/{{user.twitch}}">{{ user?.psn }}</a></div>
                                        <div class="player-feature-title"></div></span><span>
              <div class="player-feature-value">{{ user?.steam }}</div>
              <div class="player-feature-title"></div></span></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>


    </body>
    </q-page>
</template>

<script>
import UserService from "../api/services/UserService";

export default {
    name: "UserView",
    data() {
        return {
            users: [],
            title: "",
            search: '',
        };
    },
    async mounted() {
        this.retrieveUsers();
    },
    async beforeMount() {
        this.retrieveUsers();
    },
    async created() {
        this.retrieveUsers();
    },
    methods: {
        /**
         * Method to get All existing Users from Api.¬
         */
        retrieveUsers() {
            UserService.getUser()
                .then(response => {
                    this.users = response.data;
                })
                .catch(e => {
                    console.log(e);
                });
        },
    }
}
</script>

<style scoped>
.q-page {
    background-color: #333333;
}
h1 {

    color: rgb(255, 255, 255);
}

h2 {
    font-size: 1rem;
    color: rgb(255, 255, 255);
}

body {
    padding-top: 60px;
    font-family: "Saira Semi Condensed", sans-serif;
    font-weight: 400;


}


.container {
    display: grid;
    grid-template-columns: repeat(auto-fill, 25em);
}

/*
  *** fut-player-card styles ***
*/
.fut-player-card {
    width: 300px;
    height: 485px;
    background-image: url(images/lila-card.png);
    background-position: center center;
    background-size: 100% 100%;
    background-repeat: no-repeat;
    padding: 3.8rem 0;
    z-index: 2;
    transition: 200ms ease-in;
}

.fut-player-card .player-card-top {
    position: relative;
    display: flex;
    color: #e9cc74;
    padding: 0 1.5rem;
}

.fut-player-card .player-card-top .player-master-info {
    position: absolute;
    line-height: 2.2rem;
    font-weight: 300;
    padding: 1.5rem 0;
    text-transform: uppercase;
}

.fut-player-card .player-card-top .player-master-info .player-rating {
    font-size: 2rem;
}

.fut-player-card .player-card-top .player-master-info .player-position {
    font-size: 1.4rem;
}

.fut-player-card .player-card-top .player-master-info .player-nation {
    display: block;
    width: 2rem;
    height: 25px;
    margin: 0.3rem 0;
}

.fut-player-card .player-card-top .player-master-info .player-nation img {
    width: 100%;
    height: 100%;
    -o-object-fit: contain;
    object-fit: contain;
}

.fut-player-card .player-card-top .player-master-info .player-club {
    display: block;
    width: 2.1rem;
    height: 40px;
}

.fut-player-card .player-card-top .player-master-info .player-club img {
    width: 100%;
    height: 100%;
    -o-object-fit: contain;
    object-fit: contain;
}

.fut-player-card .player-card-top .player-picture {
    width: 200px;
    height: 200px;
    margin: 0 auto;
    overflow: hidden;
}

.fut-player-card .player-card-top .player-picture img {
    width: 100%;
    height: 100%;
    -o-object-fit: contain;
    object-fit: contain;
    position: relative;
    right: -1.5rem;
    bottom: 0;
}

.fut-player-card .player-card-top .player-picture .player-extra {
    position: absolute;
    right: 0;
    bottom: -0.5rem;
    overflow: hidden;
    font-size: 1rem;
    font-weight: 700;
    text-transform: uppercase;
    width: 100%;
    height: 2rem;
    padding: 0 1.5rem;
    text-align: right;
    background: none;
}

.fut-player-card .player-card-top .player-picture .player-extra span {
    margin-left: 0.6rem;
    text-shadow: 2px 2px #333;
}

.fut-player-card .player-card-bottom {
    position: relative;
}

.fut-player-card .player-card-bottom .player-info {
    display: block;
    padding: 0.3rem 0;
    color: #e9cc74;
    width: 90%;
    margin: 0 auto;
    height: auto;
    position: relative;
    z-index: 2;
}

.fut-player-card .player-card-bottom .player-info .player-name {
    width: 100%;
    display: block;
    text-align: center;
    font-size: 1.6rem;
    text-transform: uppercase;
    border-bottom: 2px solid rgba(233, 204, 116, 0.1);
    padding-bottom: 0.3rem;
    overflow: hidden;



}

.fut-player-card .player-card-bottom .player-info .player-name span {
    display: block;
    text-shadow: 2px 2px #111;

}

.fut-player-card .player-card-bottom .player-info .player-features {
    margin: 0.5rem auto;
    display: flex;
    justify-content: center;
}

.fut-player-card .player-card-bottom .player-info .player-features .player-features-col {
    border-right: 2px solid rgba(233, 204, 116, 0.1);
    padding: 0 2.3rem;

    white-space:nowrap;
    overflow:hidden;
    text-overflow:ellipsis;
}
.fut-player-card .player-card-bottom .player-info .player-features .player-features-col:hover {
    position: absolute;
    color: white;
    text-overflow: initial;
    white-space: normal;
    background-color: black;
    display: block;
}

.fut-player-card .player-card-bottom .player-info .player-features .player-features-col span {
    display: flex;
    font-size: 1.2rem;
    text-transform: uppercase;
}

.fut-player-card .player-card-bottom .player-info .player-features .player-features-col span .player-feature-value {
    margin-right: 0.3rem;
    font-weight: 700;
}

.fut-player-card .player-card-bottom .player-info .player-features .player-features-col span .player-feature-title {
    font-weight: 300;

}

.fut-player-card .player-card-bottom .player-info .player-features .player-features-col:last-child {
    border: 0;
}
a{
    color: hotpink;
}
</style>
