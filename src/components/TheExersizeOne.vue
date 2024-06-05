<template>
    <div class="track-exercise ex">
        <div class="track-exercise__container">
            <div class="track-exercise__title">Задание 1</div>
        </div>
        <span>Послушайте строчку из песни и напишите на английском языке.</span>
        <div class="track-exercise__play-container">
            <div @click="toTrackPlay" class="track-exercise__play" v-bind:class="{ track_pause: trackPlay }"></div>
            Just A Lil Bit
        </div>
        <div><input type="text" v-model.trim="writeLine" placeholder="Напиши строку"><button>Проверить</button></div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            writeLine: '',
            trackPlay: false
        }
    },
    methods: {
        toTrackPlay() {
            const audioPlayer = new Audio('ссылка_на_аудиофайл');
            this.trackPlay = !this.trackPlay;
            if (this.trackPlay) {
                audioPlayer.play();
            } else {
                audioPlayer.pause();
            }
        }
    }
}
</script>