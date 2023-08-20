<template>
    <section>
        <AppBanner />
        <div class="container news_flex">
            <AppNewsCard
                v-for="news in newsArr"
                :key="news.code"
                :newsID="news.code"
                :newsImage="news.image"
                :newsTitle="news.name"
                :newsPrevText="news.previewText"
                :newsTag="news.type.value"
                :newsDate="news.date"
                :newsLink="news.link"
            />
            
        </div>
        <div
            class="container btn_flex"
            v-if="pages <= totalPages"
        >
            <button class="btn" @click="btnFetchNews">Загрузить еще</button>
        </div>
    </section>
</template>

<script>
import AppBanner from './AppBanner.vue';
import AppNewsCard from './AppNewsCard.vue';

export default {
    data () {
        return {
            newsArr: [],
            pages: 1,
            totalPages: 0
        }
    },
    mounted() {
        this.fetchFunc()
    },
    components: { AppBanner, AppNewsCard },
    methods: {
        async fetchFunc() {
            const url = `http://flems.github.io/test/api/news/${this.pages}`

            const response = await fetch(url)
                .then((res) => {
                    if (res.status !== 200) {
                        console.log('Looks like there was a problem. Status Code: ' +  response.status);
                        return
                    }
                    return res.json()
                })
                .catch((err) => {
                    console.log('Fetch Error :', err)
                })

            const data = await response;

            this.totalPages = data.nav.total
            
            if (this.pages <= data.nav.total) {
                this.pages = this.pages + 1
                this.newsArr = this.newsArr.concat(data.items) 
            }

        },
        btnFetchNews () {
            if (this.pages >this.totalPages) {
                console.log('News is over!')
            } else {
                this.fetchFunc()
            }
        }
    }
}
</script>

<style scoped>
    .news_flex {
        display: grid;
        grid-template-columns: auto auto auto;
        grid-auto-flow: row;
        grid-auto-rows: auto;
        align-items: stretch;
        justify-items: stretch;
        grid-gap: 48px;
        column-gap: 48px;
        margin-bottom: 72px;
    }

    .btn_flex {
        display: flex;
        justify-content: center;
    }

    .btn {
        width: 203px;
        height: 56px;
        box-sizing: border-box;
        border: 1px solid #002DBF;
        border-radius: 8px;
        background-color: white;
        color: #002DBF;
        font-size: 20px;
        font-style: normal;
        font-weight: 600;
        line-height: 24px;
        letter-spacing: -0.2px;
        cursor: pointer;
    }
</style>