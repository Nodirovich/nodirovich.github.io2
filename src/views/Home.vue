<template>
  <div class="home">
    <section class="top">
      <div class="top__content container">
        <h1 class="top__title">{{ api.title }}</h1>
        <h3 v-html="api.subTitle" class="top__sub-title"></h3>
        <div class="top__date">{{ api.date }}</div>
        <!-- <p>{{ api.utc }}</p> -->

        <ul class="top__timer">
          <li>
            <span>{{ time.days }}</span>
            {{ api.day }}
          </li>
          <li>
            <span>{{ time.hours }}</span>
            {{ api.hour }}
          </li>
          <li>
            <span>{{ time.minutes }}</span>
            {{ api.minute }}
          </li>
          <li>
            <span>{{ time.seconds }}</span>
            {{ api.second }}
          </li>
        </ul>
        <div class="top__btn">
          <a class="btn" href="https://show.innoweek.uz" target="_blank">{{
            api.regBtn
          }}</a>
          <a href="https://show.innoweek.uz" target="_blank" class="btn">{{
            api.regOfflineBtn
          }}</a>
        </div>
      </div>
    </section>

    <section class="ecosystem">
      <div class="container">
        <h2 class="title" data-aos="fade-up">{{ api.eco.title }}</h2>
        <div class="row">
          <div class="col-lg-6" data-aos="fade-right" data-aos-delay="200">
            <div v-html="api.eco.text" class="ecosystem__text"></div>
          </div>
          <div class="col-lg-6" data-aos="fade-left" data-aos-delay="200">
            <div class="ecosystem__video">
              <img src="@/assets/images/eco.jpg" alt />
              <a href="#" @click.prevent="play" class="ecosystem__btn">
                <div>
                  <span class="material-icons">play_arrow</span>
                </div>
              </a>
            </div>
          </div>
        </div>

        <div class="video" v-if="video" @click="videoHandler">
          <div class="container">
            <a href="#" @click.prevent="video = false" class="video__close"
              >&times;</a
            >
            <iframe
              :src="api.eco.video"
              frameborder="0"
              allow="autoplay; fullscreen"
              allowfullscreen
            ></iframe>
          </div>
        </div>
      </div>
    </section>

    <section class="list">
      <div class="container">
        <div class="row no-gutters">
          <div
            class="col-lg-6"
            data-aos="fade-in"
            v-for="(item, idx) in api.list.all"
            :key="idx"
          >
            <div class="list__block">
              <div class="title">{{ item.title }}</div>
              <p v-html="item.text"></p>
              <!-- <a :href="item.btn.link">
                {{ item.btn.text }}
                <span class="material-icons">double_arrow</span>
              </a> -->
            </div>
          </div>
          <div class="col-lg-12" data-aos="fade-in">
            <div class="list__block list__block-live">
              <div class="title">{{ api.list.live.title }}</div>
              <p>{{ api.list.live.text }}</p>
              <a
                href="https://www.youtube.com/channel/UC8EEHIOZ2avvHZy7Yat6ijg"
                target="_blank"
              >
                {{ api.list.live.btn }}
                <span class="material-icons">double_arrow</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="result" id="result">
      <div class="container">
        <div class="title" data-aos="fade-up">{{ api.result.title }}</div>

        <div class="row">
          <div
            class="col-lg-3 col-sm-6"
            v-for="(item, idx) in api.result.list"
            :key="idx"
            data-aos="flip-left"
            :data-aos-delay="200"
          >
            <div class="result__title" v-html="item.title"></div>
            <p>
              {{ item.text }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <section class="speaker">
      <div class="container">
        <div class="title" data-aos="fade-up">{{ api.speakers.title }}</div>

        <div class="row">
          <div
            class="col-lg-3 col-sm-6"
            v-for="(speaker, idx) in api.speakers.list"
            :key="idx"
            data-aos="flip-left"
            :data-aos-delay="200"
          >
            <div class="speaker__item">
              <div class="speaker__item-img" v-if="speaker.img">
                <img
                  :src="require(`@/assets/images/speakers/${speaker.img}.jpg`)"
                  alt
                />
              </div>
              <strong>{{ speaker.name }}</strong>
              <div class="speaker__info">
                <p>{{ speaker.position }}</p>
              </div>
            </div>
          </div>
        </div>
        <a
          href="#"
          v-if="showAll"
          @click.prevent="allSpeaker"
          class="speaker__all"
        >
          {{ api.speakers.btn }}
        </a>
      </div>
    </section>

    <section class="blog" ref="blog">
      <div class="container">
        <div class="title">{{ api.blog.title }}</div>
        <div class="sub-title">{{ api.blog.text }}</div>
        <Blog :details="api.blog.postBtn" />
        <a href="https://blog.innoweek.uz" target="_blank" class="btn">{{
          api.blog.btn
        }}</a>
      </div>
    </section>

    <section class="history">
      <div class="container">
        <div class="title" data-aos="fade-up">{{ api.history.title }}</div>
        <div
          class="history__text"
          v-for="(text, index) in api.history.text"
          :key="index"
          data-aos="fade-up"
        >
          {{ text }}
        </div>
        <div class="row">
          <div class="col-lg-4" data-aos="fade-in">
            <iframe
              width="100%"
              src="https://www.youtube.com/embed/qFi4OYuUeQI"
              frameborder="0"
              allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen
            ></iframe>
          </div>
          <div class="col-lg-4" data-aos="fade-in">
            <iframe
              width="100%"
              src="https://www.youtube.com/embed/UaaEkX5GF-Y"
              frameborder="0"
              allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen
            ></iframe>
          </div>
          <div class="col-lg-4" data-aos="fade-in">
            <iframe
              width="100%"
              src="https://www.youtube.com/embed/Tg0hxyjiqDQ"
              frameborder="0"
              allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen
            ></iframe>
          </div>
        </div>
      </div>
    </section>

    <div class="partners">
      <div class="container">
        <div class="title" data-aos="fade-up">
          {{ api.partners.organizerTitle }}
        </div>
        <div class="row">
          <div
            class="col-md-3 col-6"
            v-for="(organizer, idx) in api.partners.organizer"
            :key="organizer.img"
            data-aos="fade-in"
            :data-aos-delay="idx * 100"
          >
            <a :href="organizer.link" target="_blank">
              <div class="partners__img">
                <img
                  :src="
                    require(`@/assets/images/partners/${organizer.img}.png`)
                  "
                />
              </div>
            </a>
          </div>
        </div>

        <div class="title" data-aos="fade-up">
          {{ api.partners.generalTitle }}
        </div>
        <div class="row">
          <div
            class="col-md-3 col-6"
            v-for="(partner, idx) in api.partners.generalList"
            :key="partner.img"
            data-aos="fade-in"
            :data-aos-delay="idx * 100"
          >
            <div class="partners__img">
              <img
                :src="require(`@/assets/images/partners/${partner.img}.png`)"
              />
            </div>
          </div>
        </div>

        <div class="title" data-aos="fade-up">
          {{ api.partners.texTitle }}
        </div>
        <div class="row">
          <div
            class="col-md-3 col-6"
            v-for="(partner, idx) in api.partners.texList"
            :key="partner.img"
            data-aos="fade-in"
            :data-aos-delay="idx * 100"
          >
            <a :href="partner.link" target="_blank">
              <img
                :src="require(`@/assets/images/partners/${partner.img}.png`)"
              />
            </a>
          </div>
        </div>

        <div class="title" data-aos="fade-up">{{ api.partners.title }}</div>
        <div class="row">
          <div
            class="col-md-3 col-6"
            v-for="(partner, idx) in api.partners.list"
            :key="partner.img"
            data-aos="fade-in"
            :data-aos-delay="idx * 100"
          >
            <a :href="partner.link" target="_blank">
              <img
                :src="require(`@/assets/images/partners/${partner.img}.png`)"
              />
            </a>
          </div>
        </div>

        <div class="title" data-aos="fade-up">{{ api.partners.infoTitle }}</div>
        <div class="row">
          <div
            class="col-md-3 col-6"
            v-for="(partner, idx) in api.partners.infoList"
            :key="partner.img"
            data-aos="fade-in"
            :data-aos-delay="idx * 100"
          >
            <div class="partners__img">
              <img
                :src="require(`@/assets/images/partners/${partner.img}.png`)"
              />
            </div>
          </div>
        </div>
      </div>
    </div>

    <section class="contact" id="contact">
      <div class="row no-gutters">
        <div class="col-lg-6" data-aos="slide-right">
          <div class="contact__container">
            <div class="contact__content">
              <div class="title">
                {{ api.contact.title }}
              </div>
              <div class="contact__info">
                <img src="@/assets/images/phone.png" alt />
                <a href="tel:+998712033223">+998(71) 203-32-23</a>
              </div>

              <div class="sub-title">{{ api.contact.subTitle }}</div>

              <div class="contact__info">
                <img src="@/assets/images/location.png" alt />
                <span v-html="api.contact.location"></span>
              </div>
              <a href="mailto:innoweek@mininnovation.uz">
                innoweek@mininnovation.uz
              </a>
            </div>
          </div>
        </div>
        <div class="col-lg-6">
          <iframe
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d1497.5818813065143!2d69.2071301582462!3d41.348794108357005!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x38ae8d755132b921%3A0x3d2c94a22bdea876!2sInnovatsiya%20Vazirligi!5e0!3m2!1sru!2s!4v1598004364454!5m2!1sru!2s"
            height="458"
            frameborder="0"
            style="border: 0"
            allowfullscreen
            aria-hidden="false"
            tabindex="0"
          ></iframe>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import AOS from "aos";
import API from "../static/API";
import Blog from "@/components/Blog";

export default {
  name: "Home",
  components: { Blog },
  data() {
    return {
      time: {
        days: null,
        hours: null,
        minutes: null,
        seconds: null,
      },
      video: false,
      speakerModal: {
        name: "",
        about: "",
        text: "",
        img: "",
      },
      showAll: true,
      showAllWinners: true,
      modal: false,
    };
  },
  computed: {
    api() {
      const lang = this.$store.state.curLang;
      return API[lang];
    },
  },
  methods: {
    play() {
      this.video = true;
    },
    videoHandler(event) {
      if (event.target.className === "video") {
        this.video = false;
      }
    },
    allSpeaker() {
      this.showAll = false;
      this.api.speakers.list.push(...this.api.speakers.all);
    },
    allWinners() {
      this.showAllWinners = false;
      this.api.winners.list.push(...this.api.winners.all);
    },
    scrollTo(el) {
      let element = document.querySelector(`.${el}`);
      let top = element.offsetTop;
      window.scrollTo({
        top: top,
        behavior: "smooth",
      });
    },
    setView() {
      try {
        this.$axios.get("https://show.innoweek.uz/api/innoview");
      } catch (e) {
        console.log(e);
      }
    },
    countdown() {
      const second = 1000,
        minute = second * 60,
        hour = minute * 60,
        day = hour * 24;

      const countDown = new Date(1637521200000).getTime();
      const now = new Date().getTime(),
        distance = countDown - now;

      this.time.days = Math.floor(distance / day);
      this.time.hours = Math.floor((distance % day) / hour);
      this.time.minutes = Math.floor((distance % hour) / minute);
      this.time.seconds = Math.floor((distance % minute) / second);
    },
  },
  created() {
    AOS.init({
      duration: 600,
      disable: "mobile",
      // once: true,
    });
    this.countdown();
  },
  mounted() {
    this.setView();
    setInterval(() => {
      this.countdown();
    }, 1000);
  },
  watch: {
    api() {
      this.showAll = true;
      this.showAllWinners = true;
    },
  },
};
</script>
