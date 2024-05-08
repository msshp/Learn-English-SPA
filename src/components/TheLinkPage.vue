<template>
    <div class="page-link__container">
        <div class="form addlink-container">
            <p>Введите ссылку на плейлист</p>
            <input type="text" v-model.trim="playlistLink" v-bind:class="{ empty_input: linkIsEmpty }"
                placeholder="Ссылка">
            <button className="login-btn" @click="addPlaylist()">Добавить плейлист</button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            playlistLink: '',
            linkIsEmpty: false
        }
    },
    methods: {
        addPlaylist() {
            this.linkIsEmpty = !this.playlistLink || this.playlistLink.trim().length === 0;

            if (!this.linkIsEmpty) {
                console.log('добавить плейлист');
                this.$emit('openPlaylist');
            }

        }
    }
}
</script>

<style>
.page-link__container {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

.addlink-container p {
    font-size: 24px;
    font-weight: 600;
    line-height: 75%;
    text-align: center;
    color: #171802;
    margin: 0 0 32px;
}
</style>