<template>
    <div class="page-content__container">
        <div class="user-info">
            <div class="user-info">
                <div class="user-photo"></div>
                <div class="user-info__text">
                    <p class="user-info__text-name">{{ trackStorage.title }}</p>
                </div>
            </div>
            <div class="user-buttons">
                <!-- <button @click="goToPlaylist">Перейти в плейлист</button> -->
                <button @click="pressList">Все плейлисты</button>
                <button v-if="track.exOne" @click="backToTrack">Назад</button>
                <button v-if="track.exTwo" @click="backToTrack">Назад</button>
            </div>
        </div>
        <div class="table" v-if="track.main">
            <div class="track-exercise">
                <div class="track-exercise__container">
                    <div class="track-exercise__title">Задание 1</div><button @click="openExOne">Выполнить</button>
                </div>
                <span>Послушайте строчку из песни и напишите на английском языке.</span>
            </div>
            <div class="track-exercise">
                <div class="track-exercise__container">
                    <div class="track-exercise__title">Задание 2</div><button @click="openExTwo">Выполнить</button>
                </div>
                <span>Соберите строку из слов (переставьте карточки).</span>
            </div>
        </div>
        <div v-if="track.main" class="progress-container progress-container-playlist">
            <div class="progress-value-playlist">прогресс<div>{{ trackStorage.progress }}%</div>
            </div>
            <input class="slider-wrapper slider-progress" id="progress-track" type="range" min="0" max="100" disabled />
        </div>
        <TheExersizeOne v-if="track.exOne" />
        <TheExersizeTwo v-if="track.exTwo" />
    </div>

</template>

<script>
import TheExersizeOne from './TheExersizeOne.vue'
import TheExersizeTwo from './TheExersizeTwo.vue'

export default {
    components: {
        TheExersizeOne,
        TheExersizeTwo
    },
    data() {
        return {
            trackStorage: {
                progress: 45,
                title: 'Just A Lil Bit'
            },
            shift: 12,
            track: {
                main: true,
                exOne: false,
                exTwo: false
            }
        }
    },
    methods: {
        goToPlaylist() {
            this.$emit('openPlaylist');
        },
        pressList() {
            this.$emit('openList');
        },
        openExOne() {
            for (let page in this.track) {
                this.track[page] = false;
            }
            this.track.exOne = true;
        },
        openExTwo() {
            for (let page in this.track) {
                this.track[page] = false;
            }
            this.track.exTwo = true;
        },
        backToTrack() {
            for (let page in this.track) {
                this.track[page] = false;
            }
            this.track.main = true;
            setTimeout(() => {
                this.drawInput();
            }, 100);
        },
        drawInput() {
            // PROGRESS
            const progressInput = document.getElementById('progress-track');
            // Установить значение из data() в атрибут value элемента input
            progressInput.value = Number(this.trackStorage.progress);

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
    },
    mounted() {
        this.drawInput();
    }
}
</script>

<style>
#progress-track {
    width: 90%;
    margin: 0 48px;
}

.track-exercise {
    border-radius: 24px;
    border: 1px solid #E6E7DF;
    padding: 24px 32px 40px 24px;
}

.track-exercise:first-child {
    margin-bottom: 24px;
}

.track-exercise__container {
    display: flex;
    align-items: center;
    margin-bottom: 24px;
}

.track-exercise__title {
    font-weight: 400;
    font-size: 24px;
    color: #171802;
    margin-right: 24px;
    font-family: 'Open Sans';
}

.track-exercise__container button {
    border-radius: 24px;
    width: 140px;
    height: 40px;
    background: #DDEA4D;
    font-weight: 400;
    font-size: 14px;
    line-height: 150%;
    text-align: center;
    font-family: 'Open Sans';
}

.track-exercise span {
    font-weight: 400;
    font-size: 14px;
    color: #171802;
    font-family: 'Open Sans';
}

.track-exercise__play-container {
    font-weight: 600;
    font-size: 24px;
    color: #171802;
    font-family: 'RockStar';
    margin-top: 48px;
    margin-bottom: 24px;
    display: flex;
    align-items: center;
}

.ex {
    margin-top: 32px;
}

.track-exercise input {
    border-radius: 24px;
    width: 60%;
    padding: 15px 24px;
    background-color: #E7E7DF;
    color: #171802;
    margin-bottom: 8px;
    font-family: 'Open Sans';
    font-weight: 400;
    font-size: 16px;
    line-height: 112%;
}

.track-exercise button {
    border-radius: 24px;
    width: 150px;
    height: 48px;
    background-color: #EED16D;
    font-weight: 400;
    font-size: 16px;
    line-height: 112%;
    font-family: 'Open Sans';
    margin-left: 16px;
}
</style>