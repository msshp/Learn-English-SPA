<template>
    <div class="track-exercise ex">
        <div class="track-exercise__container">
            <div class="track-exercise__title">Задание 2</div>
        </div>
        <span>Соберите строку из слов (переставьте карточки).</span>
        <div class="track-exercise__play-container">
            <div @click="toTrackPlay" class="track-exercise__play" v-bind:class="{ track_pause: trackPlay }"></div>
            Just A Lil Bit
        </div>
        <div class="word">
            <div>слово3</div>
            <div>слово1</div>
            <div>слово4</div>
            <div>слово2</div><button @click="checkLine">Проверить</button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            done: false,
            trackPlay: false
        }
    },
    methods: {
        checkLine() {
            if (this.done) {
                console.log('done');
            }
        },
        toTrackPlay() {
            const audioPlayer = new Audio('ссылка_на_аудиофайл');
            this.trackPlay = !this.trackPlay;
            if (this.trackPlay) {
                audioPlayer.play();
            } else {
                audioPlayer.pause();
            }
        }
    },
    mounted() {
        const container = document.querySelector('.word');
        const divs = container.querySelectorAll('div');

        let dragged;

        divs.forEach((div) => {
            div.draggable = true;

            div.addEventListener('dragstart', (e) => {
                dragged = e.target;
                e.target.style.opacity = '0.5';
            });

            div.addEventListener('dragend', (e) => {
                e.target.style.opacity = '';
            });

            div.addEventListener('dragover', (e) => {
                e.preventDefault();
            });

            div.addEventListener('drop', (e) => {
                e.preventDefault();
                if (e.target !== dragged) {
                    container.insertBefore(dragged, e.target);
                }

                const orderedWords = Array.from(container.querySelectorAll('div')).map(div => div.textContent.trim());
                if (orderedWords.join('') === 'слово1слово2слово3слово4') {
                    this.done = true;
                }
            });
        });
    }
}
</script>

<style>
.word {
    display: flex;
}

.word div {
    border-radius: 24px;
    padding: 8px 24px;
    height: 34px;
    background-color: #E8F08F;
    display: flex;
    align-items: center;
    margin-left: 8px;
    cursor: pointer;
}

.track_pause {
    background-image: url(../img/pause.svg);
}
</style>