<template>
    <div class="page-content__container">
        <div class="user-info">
            <div class="user-info">
                <div class="user-photo"></div>
                <div class="user-info__text">
                    <p class="user-info__text-name">{{ playlistInfo.name }}</p>
                </div>
            </div>
            <div class="user-buttons">
                <button @click="pressAddPlaylist">Добавить плейлист</button>
                <button @click="pressList">Все плейлисты</button>
            </div>
        </div>
        <div class="table">
            <div class="line" v-for="(track, index) in playlistInfo.storage" :key="track"
                @click="openTrackPage(track.name)" :class="index % 2 === 0 ? 'grey' : 'white'">
                <div class="line-name">{{ track.name }}</div>
                <div class="line-author">{{ track.author }}</div>
                <div class="line-author">{{ track.year }}</div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return {
            playlistInfo: {
                name: 'Playlist',
                storage: [
                    {
                        name: 'Enjoy the Silence',
                        author: 'Depeche Mode',
                        year: '1990'
                    }, {
                        name: 'Enjoy the Silence',
                        author: 'Depeche Mode',
                        year: '1990'
                    }, {
                        name: 'Enjoy the Silence',
                        author: 'Depeche Mode',
                        year: '1990'
                    }, {
                        name: 'Enjoy the Silence',
                        author: 'Depeche Mode',
                        year: '1990'
                    }
                ]
            }
        }
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
        // Получить элемент input
        console.log('получить информацию о плейлисте')
    }
}
</script>