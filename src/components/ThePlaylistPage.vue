<template>
    <div class="page-content__container">
        <div class="user-info">
            <div class="user-info">
                <div class="user-photo"></div>
                <div class="user-info__text">
                    <p class="user-info__text-name">{{ playlistInfo.title }}</p>
                </div>
            </div>
            <div class="user-buttons">
                <button @click="pressAddPlaylist">Добавить плейлист</button>
                <button @click="pressList">Все плейлисты</button>
            </div>
        </div>
        <div class="table">
            <div class="line" v-for="(track, index) in playlistInfo.tracks" :key="track"
                @click="openTrackPage(track.title)" :class="index % 2 === 0 ? 'grey' : 'white'">
                <div class="line-name">{{ track.title }}</div>
                <div class="line-author">{{ track.authors[0] }}</div>
            </div>
        </div>
        <div class="progress-container progress-container-playlist">
            <div class="progress-value-playlist">прогресс<div>{{ playlistInfo.progress }}%</div>
            </div>
            <input class="slider-wrapper slider-progress" id="progress-playlist" type="range" min="0" max="100"
                disabled />
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return {
            // playlistInfo: {
            //     name: 'Playlist',
            //     storage: [
            //         {
            //             name: 'Enjoy the Silence',
            //             author: 'Depeche Mode'
            //         }, {
            //             name: 'Enjoy the Silence',
            //             author: 'Depeche Mode'
            //         }, {
            //             name: 'Enjoy the Silence',
            //             author: 'Depeche Mode'
            //         }, {
            //             name: 'Enjoy the Silence',
            //             author: 'Depeche Mode'
            //         }
            //     ]
            // },
            playlistInfo: {
                "id": "254306981:1017",
                "title": "debug matveezy",
                "progress": 30,
                "tracks": [
                    {
                        "id": "112047068:25129938",
                        "authors": [
                            "FENDIGLOCK"
                        ],
                        "title": "Памятник",
                        "content_warning": "explicit",
                        "lyrics_count": 35
                    },
                    {
                        "id": "4214:4241617",
                        "authors": [
                            "50 Cent"
                        ],
                        "title": "Just A Lil Bit",
                        "content_warning": "explicit",
                        "lyrics_count": 74
                    }
                ]
            },
            shift: 12
        }
    },
    props: {
        playlistStorage: Object
    },
    methods: {
        pressList() {
            this.$emit('openList');
        },
        pressAddPlaylist() {
            this.$emit('openLink');
        },
        openTrackPage(name) {
            this.$emit('openTrack', name);
        }
    },
    mounted() {
        this.playlistInfo = this.playlistStorage; // сохранение информации в локальное хранилище компонента

        // PROGRESS
        const progressInput = document.getElementById('progress-playlist');
        // Установить значение из data() в атрибут value элемента input
        progressInput.value = Number(this.playlistInfo.progress);

        progressInput.style.setProperty('background', `-webkit-linear-gradient(left, #DDEA4D 0%, #DDEA4D ${progressInput.value}%, #E6E7DF ${progressInput.value}%, #E6E7DF 100%)`, 'important');

        if (progressInput.value < 4) {
            this.shift = -4
        } else if (progressInput.value < 10) {
            this.shift = 0
        } else if (progressInput.value < 20) {
            this.shift = 5
        } else if (progressInput.value > 91) {
            this.shift = 20
        } else if (progressInput.value > 101) {
            this.shift = 30
        }

        let progressValue = document.querySelector('.progress-value-playlist');
        progressValue.style.marginLeft = `${progressInput.value - this.shift}%`;
    }
}
</script>

<style>
#progress-playlist {
    width: 90%;
    margin: 0 48px;
}

.progress-value-playlist {
    border-radius: 24px;
    width: 220px;
    height: 48px;
    background: #DDEA4D;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 16px;
    font-family: 'Open Sans';
    font-weight: 400;
    font-size: 20px;
    color: #171802;
}

.progress-value-playlist div {
    margin-left: 8px;
    margin-top: 5px;
    font-family: 'RockStar';
}

.progress-container-playlist {
    margin-top: 24px;
}
</style>