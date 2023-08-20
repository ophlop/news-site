<template>
    <a :href="newsLink" target="_blank">
        <div
            class="news_card"
            :id="newsID"
            :class="withoutImage"
        >
            <div class="news_img" v-if="newsImage !== ''">
                <img :src="newsImage" alt="news_image">
            </div>

            <div class="news_info">
                <div class="news_date">
                    <h3 class="date_number">{{ newsDay }}</h3>
                    <div class="date_month_year">
                        <p class="date_month">{{ newsMonth }}</p>
                        <p class="date_year">{{ newsYear }}</p>
                    </div>
                </div>
                <div class="news_contents">
                    <h2 class="news_title">{{ newsTitle }}</h2>
                    <span class="news_text">{{ newsPrevText }}</span>
                </div>
                <div class="img-hover_height" v-if="newsImage"></div>
            </div>

            <div class="news_tag">
                <p class="tag_text">{{ newsTag }}</p>
            </div>
        </div>
    </a>
</template>

<script>
import moment from '../../node_modules/moment'

export default {
    data () {
        return {
            newsDay: "",
            newsMonth: "",
            newsYear: ""
        }
    },
    props: ['newsImage', 'newsTitle', 'newsPrevText', 'newsTag', 'newsDate', 'newsLink', 'newsID'],
    mounted() {
        this.rightDate()
    },
    methods: {
        rightDate() {
            const date = moment.unix(`${this.newsDate}`) // .format("D MMMM YYYY").split(' ');

            this.newsDay = date.format("D")
            this.newsMonth = date.format("MMMM")
            this.newsYear = date.format("YYYY")
        }
    },
    computed: {
        withoutImage () {
            return this.newsImage === '' ? 'news_card_top_padding' : ''
        }
    }
}
</script>

<style scoped>
    .news_card {
        position: relative;
        width: 536px;
        height: 100%;
        background-color: white;
        box-sizing: border-box;
        border: 1px solid #0F62FE;
        border-radius: 16px;
        display: flex;
        flex-direction: column;
    }

    .news_card_top_padding {
        padding-top: 48px;
    }

    .news_img {
        margin-bottom: 32px;
        display: flex;
        width: 536px;
        position: relative;
        top: -2px;
        left: -0.2px;
    }

    .news_img > img {
        width: 100%;
        height: 250px;
        border-radius: 16px 16px 0px 0px;
    } 
    
    .img-hover_height {
        height: 0px;
        width: 100%;
        margin: 0;
    }

    .news_card:hover > .news_img > img {
        display: none;
    } 

    .news_card:hover > .news_info > .img-hover_height {
        height: 250px;
    }

    .news_card:hover {
        height: calc(100% + 10px);
    }

    .news_info {
        width: 100%;
        height: fit-content;
        padding: 0px 32px 32px;
        box-sizing: border-box;
        position: relative;
    }

    .news_date {
        width: 254px;
        height: fit-content;
        display: flex;
        gap: 4px;
        margin-bottom: 14px;
    }

    .date_number {
        margin: 0;
        color: #A1A7B5;
        font-size: 36px;
        font-style: normal;
        font-weight: 400;
        line-height: 36px;
    }

    .date_month_year {
        width: fit-content;
        height: 100%;
    }
    
    .date_month, .date_year {
        margin: 0;
        color: #A1A7B5;
        font-size: 15px;
        font-style: normal;
        font-weight: 700;
        line-height: 16.5px;
        letter-spacing: -0.15px;
    }

    .news_contents {
        margin-bottom: 40px;
    }

    .news_title {
        margin: 0px 0px 16px 0px;
        color: #0C5BEF;
        font-size: 22px;
        font-style: normal;
        font-weight: 400;
        line-height: 26.4px;
    }

    .news_text {
        margin: 0px 0px 40px 0px;
        color: #222327;
        font-size: 20px;
        font-style: normal;
        font-weight: 400;
        line-height: 26px;
        letter-spacing: -0.2px;
    }

    .news_tag {
        position: relative;
        bottom: 0;
        display: flex;
        flex-grow: 1;
        align-items: flex-end;
        margin-bottom: 32px;
        width: 50px;
        height: 20px;
        padding: 4px 16px;
        margin-left: 32px;
        white-space: nowrap;
    }

    .tag_text {
        margin: 0;
        color: #00133A;
        font-size: 14px;
        font-style: normal;
        font-weight: 400;
        line-height: 19.6px;
    }

</style>

//v-on:mouseleave="hoverBack(newsID)"