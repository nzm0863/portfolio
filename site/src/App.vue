<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue"; // ref をインポート
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);

// 動画リストを定義
const videoSources = [
  "./video/214409_tiny.mp4",
  "./video/246856_tiny.mp4",
  "./video/253423_small.mp4",
];

// 現在の動画インデックスを管理
const currentVideoIndex = ref(0);
const isFading = ref(false); // フェードアニメーションの状態を管理
// 動画の切り替えロジック
let intervalId: number | undefined;

const changeVideo = () => {
  isFading.value = true; // フェードアウト開始
  setTimeout(() => {
    currentVideoIndex.value =
      (currentVideoIndex.value + 1) % videoSources.length; // 次の動画に切り替え
    isFading.value = false; // フェードイン開始
  }, 1000); // フェードアウトの時間（1秒）
};

// コンポーネントがマウントされたときにタイマーを開始
onMounted(() => {
  intervalId = setInterval(changeVideo, 10000); // 10秒ごとに切り替え
});

// コンポーネントがアンマウントされたときにタイマーをクリア
onUnmounted(() => {
  if (intervalId) clearInterval(intervalId);
});

// ハンバーガー
const navOpen = ref(false);

// gsap
onMounted(() => {
  gsap.from("#headline", {
    duration: 1,
    x: -100,
    opacity: 0,
    ease: "bounce.out",
  });
  gsap.from("#header-home", {
    duration: 1,
    y: -100,
    opacity: 0,
    ease: "bounce.out",
    delay: 0.2,
  });
  gsap.from("#header-works", {
    duration: 1,
    y: -100,
    opacity: 0,
    ease: "bounce.out",
    delay: 0.4,
  });
  gsap.from("#header-skill", {
    duration: 1,
    y: -100,
    opacity: 0,
    ease: "bounce.out",
    delay: 0.6,
  });
  gsap.from("#header-Iot", {
    duration: 1,
    y: -100,
    opacity: 0,
    ease: "bounce.out",
    delay: 0.8,
  });
  gsap.from("#header-about", {
    duration: 1,
    y: -100,
    opacity: 0,
    ease: "bounce.out",
    delay: 1.0,
  });
  gsap.from("#header-contact", {
    duration: 1,
    y: -100,
    opacity: 0,
    ease: "bounce.out",
    delay: 1.2,
  });
  gsap.from(".hero h2", {
    duration: 3,
    y: -100,
    opacity: 0,
    delay: 1.4,
    rotation: 360,
    ease: "elastic.out(1, 0.3)",
  });
  gsap.from(".hamburger", {
    duration: 3,
    y: -100,
    opacity: 0,
    delay: 0.2,
    rotation: 360,
    ease: "elastic.out(1, 0.3)",
  });
  gsap.from(".video-container video", {
    scale: 2,
    duration: 3,
    ease: "power2.out",
  });

  gsap.utils.toArray(".skill-item").forEach((el) => {
    gsap.from(el as Element, {
      scale: 0.7, // 小さく
      opacity: 0, // 透明
      y: 80, // 下から
      rotate: 45, // 45度回転
      duration: 1.4, // ゆっくり
      ease: "elastic.out(1, 0.5)", // 弾むような動き
      scrollTrigger: {
        trigger: el as Element,
        start: "top 80%",
        toggleActions: "restart none none none",
        once: true,
      },
    });
  });

  gsap.from("#aboutImage", {
    scale: 0.4,
    opacity: 0,
    rotate: 720,
    duration: 4,
    y: 300,
    ease: "elastic.out(1, 0.5)",
    scrollTrigger: {
      trigger: "#aboutImage",
      start: "top 100%",
      once: true, // ← 追加
    },
  });
});
</script>

<template>
  <div class="hero">
    <header>
      <div class="header_wrap">
        <h1 id="headline"><a href="/">Nakamura</a></h1>
        <nav class="nav-pc" :class="{ open: navOpen }">
          <ul>
            <li id="header-home"><a href="/">Home</a></li>
            <li id="header-works"><a href="#works">Works</a></li>
            <li id="header-skill"><a href="#skill">Skill</a></li>
            <li id="header-Iot"><a href="#Iot">IoT</a></li>
            <li id="header-about"><a href="#about">About</a></li>
            <li id="header-contact"><a href="#contact">Contact</a></li>
          </ul>
        </nav>
        <!-- ハンバーガー -->
        <div
          class="hamburger"
          :class="{ active: navOpen }"
          @click="navOpen = !navOpen"
        >
          <div></div>
          <div></div>
          <div></div>
        </div>
        <nav class="nav-sp" :class="{ open: navOpen }">
          <ul>
            <li><a href="/" @click="navOpen = false">Home</a></li>
            <li><a href="#works" @click="navOpen = false">Works</a></li>
            <li><a href="#skill" @click="navOpen = false">Skill</a></li>
            <li><a href="#Iot" @click="navOpen = false">IoT</a></li>
            <li><a href="#about" @click="navOpen = false">About</a></li>
            <li><a href="#contact" @click="navOpen = false">Contact</a></li>
          </ul>
        </nav>
      </div>
    </header>
    <h2>Portfolio</h2>
    <div class="video-container">
      <video
        autoplay
        loop
        muted
        preload="auto"
        :src="videoSources[currentVideoIndex]"
        :class="{ fade: isFading }"
      ></video>
    </div>
  </div>

  <section class="works">
    <h2 class="works-headline" id="works">Works</h2>
    <div class="works-items">
      <div class="works-item">
        <a
          href="https://www.nnzzm.com/project_management/"
          target="_blank"
          rel="noopener noreferrer"
          ><img src="/img/TaskFlow.png" alt="TaskFlow"
        /></a>
        <p>
          案件情報の登録・管理ができるタスク管理アプリ <br />React / TypeScript
          / Vite
        </p>
      </div>
      <div class="works-item">
        <a
          href="https://www.nnzzm.com/sigotoru1"
          target="_blank"
          rel="noopener noreferrer"
          ><img src="/img/dentist.jpg" alt="dentist"
        /></a>
        <p>
          予約導線を意識した歯科医院向けサイト <br />React / TypeScript / Vite
        </p>
      </div>
      <div class="works-item">
        <a
          href="https://www.nnzzm.com/portfolio_wp"
          target="_blank"
          rel="noopener noreferrer"
          ><img src="/img/portfolio_wp.png" alt="portfolio_wp"
        /></a>
        <p>WordPressテーマ化ポートフォリオ<br />WordPress / PHP</p>
      </div>
      <div class="works-item">
        <a
          href="https://www.youtube.com/@nakamura-nnzzm/shorts"
          target="_blank"
          rel="noopener noreferrer"
          ><img src="/img/youtubeLink.png" alt="IoTYoutube"
        /></a>
        <p>ESP32を用いたIoT制作の過程を動画で公開 <br />ESP32 / Arduino IDE</p>
      </div>
    </div>
  </section>

  <section class="skill">
    <h2 class="skill-headline" id="skill">Web Skill</h2>
    <div class="skill-items">
      <div class="skill-item">
        <img src="/img/react.png" alt="TypeScript" />
        <p><span>React</span><br />コンポーネント設計を用いたUI開発を実践</p>
      </div>
      <div class="skill-item">
        <img src="/img/ts-img.png" alt="TypeScript" />
        <p>
          <span>TypeScript</span><br />型安全を意識したフロントエンド開発を経験
        </p>
      </div>
      <div class="skill-item">
        <img src="/img/PHP-img.png" alt="PHP" />
        <p><span>PHP</span><br />フォーム処理やデータベース連携を実装</p>
      </div>
      <div class="skill-item">
        <img src="/img/wordpress-img.png" alt="WordPress" />
        <p>
          <span>WordPress</span><br />オリジナルテーマ制作やカスタマイズを経験
        </p>
      </div>
      <div class="skill-item">
        <img src="/img/vue-img.png" alt="vue.js" />
        <p><span>vue.js</span><br />Vue + Viteを用いて本ポートフォリオを制作</p>
      </div>
      <div class="skill-item">
        <img src="/img/figma-img.png" alt="Figma" />
        <p><span>Figma</span><br />画面設計やプロトタイプ作成に活用</p>
      </div>
    </div>
  </section>

  <section class="Iot">
    <h2 class="Iot-headline" id="Iot">IoT</h2>
    <div class="TaskFlow-Iot">
      <div class="Iot-item">
        <a href="https://www.nnzzm.com/project_management/">
          <img src="/img/TaskFlow-Iot.png" alt="TaskFlow-IoT" />
        </a>
        <h3>
          ESP32とNeoPixelを用いて、案件管理アプリの状態に応じたLED制御を実装。<br />
          PC画面を開かなくても案件状況を把握できるよう工夫し、<br />
          視認性向上による業務効率化を目指して開発。<br />
          ESP32 / Arduino IDE / React / TypeScript / vite
        </h3>
        <a
          href="https://github.com/nzm0863/taskflow-app"
          class="TaskFlow-code-link"
          >GitHubで見る→</a
        >
      </div>
    </div>
    <div class="IotCar">
      <div class="Iot-item">
        <video
          src="/video/1000000932.mp4"
          aria-label="Iot-video"
          muted
          preload="metadata"
          controls
        />
        <h3 class="raspberry-headline">
          Raspberry Pi搭載メカナムホイールカー<br />
          試作機のトラブルをきっかけにESP32版へ移行
        </h3>
      </div>
      <div class="Iot-item">
        <a
          href="https://www.youtube.com/@nakamura-nnzzm/shorts"
          target="_blank"
          rel="noopener noreferrer"
          ><img src="/img/ESP32Car.jpg" alt="ESP32Car" />
        </a>
        <h3 class="raspberry-headline">
          ESP32搭載メカナムホイールカー<br />
          電源設計やモーター制御を見直し改良を継続
        </h3>
      </div>
    </div>
  </section>

  <section class="about">
    <h2 class="about-headline" id="about">About</h2>
    <figure class="about-figure">
      <img src="/img/me.jpg" alt="me" id="aboutImage" />
      <figure class="about-figcaption" id="aboutFigcaption">
        React / TypeScript を用いたフロントエンド開発を中心に、 Supabase や
        Next.js を活用したWebアプリケーション開発にも取り組んでいます。<br>
        　また、ESP32 や Raspberry Pi を活用した IoT 開発を通じて、 Web
        とハードウェアを組み合わせた課題解決を目指しています。
      </figure>
    </figure>
    <div class="sns-links">
      <a
        href="https://github.com/nzm0863/"
        class="github-link"
        target="_blank"
        rel="noopener noreferrer"
        ><img src="/img/GitHub_Lockup_White.png" alt="GitHub"
      /></a>
      <a
        href="https://www.youtube.com/@nakamura-nnzzm/shorts"
        class="youtube-link"
        target="_blank"
        rel="noopener noreferrer"
        ><img src="/img/youtube_link5.png" alt="YouTube"
      /></a>
    </div>
  </section>

  <section class="contact" id="contact">
    <h1 class="contact-headline">Contact</h1>
    <div class="wrapper">
      <form
        action="./assets/comfirm.php"
        method="post"
        id="contact_form"
        class="h-adr"
      >
        <span class="p-country-name" style="display: none">Japan</span>
        <div class="sp100 of_x">
          <table id="contactform_table" class="width81 mb_30">
            <tr>
              <th><label for="name">名前</label></th>
              <td>
                <input name="name" type="text" id="name" required />
              </td>
            </tr>
            <tr>
              <th><label for="email">メール</label></th>
              <td>
                <input
                  name="email"
                  type="email"
                  id="email"
                  size="45"
                  required
                />
              </td>
            </tr>

            <tr>
              <th><label for="tel">電話番号</label></th>
              <td>
                <input name="tel" type="tel" id="tel" required />
              </td>
            </tr>
            <tr>
              <th><label for="age">年齢</label></th>
              <td>
                <div class="select-group">
                  <select name="age" id="age">
                    <option value="" selected>-選択してください-</option>
                    <option value="10代">10代</option>
                    <option value="20代">20代</option>
                    <option value="30代">30代</option>
                    <option value="40代">40代</option>
                    <option value="50代">50代</option>
                    <option value="60代以上">60代以上</option>
                  </select>
                </div>
              </td>
            </tr>
            <tr>
              <th>希望連絡方法</th>

              <td class="radio">
                <div class="radio-group">
                  <input
                    type="radio"
                    name="contact_means"
                    value="電話"
                    id="contact_tel"
                    required
                  /><label for="contact_tel">電話</label>
                  <input
                    type="radio"
                    name="contact_means"
                    value="メール"
                    id="contact_email"
                    required
                  /><label for="contact_email">メール</label>
                  <input
                    type="radio"
                    name="contact_means"
                    value="希望なし"
                    id="contact_others"
                    required
                  /><label for="contact_others">希望なし</label>
                </div>
              </td>
            </tr>
            <tr>
              <th><label for="comment">メッセージ</label></th>
              <td>
                <textarea
                  name="comment"
                  cols="70"
                  rows="10"
                  id="comment"
                  required
                ></textarea>
              </td>
            </tr>
            <tr>
              <td colspan="2">
                <input
                  type="submit"
                  name="Submit"
                  value="送信"
                  id="submit"
                  class="form_btn"
                />
              </td>
            </tr>
          </table>
        </div>
      </form>
    </div>
  </section>

  <footer class="footer">
    <p class="footer-paragraph">&#169;Nakamura</p>
  </footer>
</template>

<style>
@charset "UTF-8";
html {
  scroll-behavior: smooth;
}

body {
  font-family: "游明朝", "Yu Mincho", YuMincho, "Hiragino Mincho Pro", serif;
  color: #fff;
  background: #2600ff;
  background: linear-gradient(
    90deg,
    rgba(38, 0, 255, 1) 0%,
    rgba(106, 0, 255, 1) 33%,
    rgba(38, 0, 255, 1) 50%,
    rgba(106, 0, 255, 1) 66%,
    rgba(38, 0, 255, 1) 100%
  );
  overflow-x: hidden;
  font-size: 20px;
}

.cursor-trail {
  position: fixed;
  top: 0;
  left: 0;
  width: 10px;
  height: 10px;
  background-color: rgba(150, 166, 0, 0.7); /* 半透明の赤色 */
  border-radius: 50%;
  pointer-events: none; /* 要素がクリックを妨げないようにする */
  transition: opacity 0.2s ease-out;
  opacity: 1;
  z-index: 9999; /* 最前面に表示 */
}

/* header */
header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: auto;
  background-color: rgba(0, 0, 0, 0.8);
  padding: 20px 0;
  z-index: 10;
}

.header_wrap {
  width: 100%;
  max-width: 1440px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
@media screen and (max-width: 1500px) and (min-width: 768px) {
  .header_wrap {
    width: 90vw;
  }
}
.header_wrap h1 {
  margin: 0;
}

header h1 a {
  color: #fff;
  text-decoration: none;
}

.nav-pc ul {
  padding: 0;
  list-style: none;
  display: flex;
}

.nav-pc ul li {
  margin-left: 45px;
}

.nav-pc ul li a {
  color: #fff;
  text-decoration: none;
  font-size: 20px;
  padding: 0 5px;
}

.nav-pc ul li a:hover {
  color: #89defb;
  background-color: rgba(105, 105, 105, 0.8);
  padding: 5px;
  border-radius: 5px;
  transition: all 0.2s;
}

.hamburger {
  display: none;
}

.nav-sp {
  display: none;
}

/* hero */
.hero {
  position: relative;
  width: 100%;
  height: 100vh;
  min-height: 100vh;
  max-height: 100vh;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0;
  padding: 0;
}

.video-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  min-height: 100vh;
  max-height: 100vh;
}
.hero h2 {
  font-size: 64px;
  color: rgb(255, 255, 255);
  font-weight: 600;
  text-shadow: 0 0 20px rgba(255, 255, 255, 1);
  z-index: 1;
}

.hero video {
  position: absolute;
  width: 100%;
  height: 100vh;
  display: block;
  transition: opacity 1s ease; /* フェードアニメーションの時間 */
  opacity: 1;
  overflow: hidden;
  z-index: -10; /* 背景に配置 */
  object-fit: cover;
}

video.fade {
  opacity: 0; /* フェードアウト時の透明度 */
}

#particles-js {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 2; /* 背景に配置 */
}
/* works */
.works {
  width: 100%;
  height: auto;
  text-align: center;
  /* padding: 50px 20px; */
}
.works-headline {
  text-align: center;
  font-size: 40px;
  margin-bottom: 30px;
  scroll-margin-top: 200px;
}
.works-items {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
  margin: 0 auto;
}
.works-item {
  height: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0 auto;
  position: relative;
}
.works-item a {
  width: fit-content;
  line-height: 0;
}
.works-item img {
  width: 35vw;
  height: 400px;
  object-fit: cover;
  transition: all 0.2s;
  margin: 10px;
}
@media screen and (max-width: 1200px) {
  .works-item img {
    height: 200px;
  }
}
.works-item img:hover {
  transform: scale(1.05);
  transition: all 0.2s;
}
.works-item p {
  margin-top: 10px;
  color: #fff;
}

/* skill */
.skill {
  width: 100%;
  height: auto;
  text-align: center;
}
.skill-headline {
  text-align: center;
  font-size: 40px;
  margin-bottom: 30px;
  scroll-margin-top: 200px;
}
.skill-items {
  display: flex;
  flex-wrap: wrap;
  gap: 40px;
  justify-content: center;
  margin: 0 auto;
}
.skill-item {
  flex: 0 1 calc(40% - 30px);
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.skill-item span {
  font-weight: 700;
}
.html-css {
  display: flex;
  justify-content: center;
  align-items: center;
}
.html-css img {
  width: 70%;
}

/* Iot */
.Iot {
  width: 100%;
  height: auto;
  text-align: center;
}
.Iot-headline {
  text-align: center;
  font-size: 40px;
  margin-bottom: 30px;
  scroll-margin-top: 200px;
}
.IotCar {
  display: flex;
  justify-content: center;
  gap: 20px;
}
@media (max-width: 1200px) {
  .IotCar {
    flex-direction: column;
    align-items: center;
  }
}
.Iot-items {
  display: flex;
  flex-wrap: wrap;
  gap: 100px;
  justify-content: center;
  margin: 0 auto;
}
.Iot-item {
  flex: 0 1 calc(25% - 30px);
  position: relative;
}
.Iot-item img {
  width: auto;
  height: 500px;
  max-width: 1000px;
  object-fit: cover;
  margin: 10px;
  transition: all 0.2s;
}
@media (max-width: 1200px) {
  .Iot-item img {
    width: 60vw;
    height: auto;
  }
}
.Iot-item img:hover {
  transform: scale(1.05) !important;
}
.Iot-item video {
  width: auto;
  height: 500px;
  object-fit: cover;
  margin: 10px;
}
.ESP32-headline {
  font-size: 20px;
  margin-bottom: 10px;
  color: #fff;
}
.raspberry-headline {
  font-size: 20px;
  color: #fff;
  margin-bottom: 50px;
  margin-top: 0;
}
.Iot-devices-headline {
  font-size: 30px;
  margin-bottom: 10px;
  color: #fff;
  margin-top: 0;
}
.Iot-devices {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 100px;
}
.Iot-devices-items {
  align-items: center;
  justify-content: center;
}
.Iot-device-img {
  width: 30vw;
  height: 50vh;
  object-fit: cover;
  margin: 20px 10px 10px 0;
  transition: all 0.2s !important;
}
.Iot-device-img:hover {
  transform: scale(1.05);
}
.Iot-device {
  font-size: 20px;
  color: #fff;
  margin-left: 10px;
}
.arduinoIDE-img {
  width: 50vw;
  height: 450px;
  object-fit: cover;
  margin: 70px 0 10px 10px;
  transition: all 0.2s !important;
}
.arduinoIDE-img:hover {
  transform: scale(1.05) !important;
}
.API-img {
  width: 80vw;
  height: auto;
  object-fit: cover;
  margin: 70px 0 10px 10px;
  transition: all 0.2s !important;
}
.API-img:hover {
  transform: scale(1.05) !important;
}
.API-link {
  color: #fff;
  text-decoration: none;
  margin-left: 10px;
  transition: all 0.2s;
}
.API-link:hover {
  transform: scale(1.05);
}

.TaskFlow-code-link {
  color: #fff;
  text-decoration: none;
  margin-left: 10px;
  margin-bottom: 50px;
  background-color: #00b60f;
  padding: 5px 10px;
  border-radius: 5px;
  border: 1px solid #003504;
  box-shadow: 0 5px 5px 0 #003504;
  transition: all 0.1s;
  display: inline-block;
}
.TaskFlow-code-link:hover {
  transform: scale(1.05);
}

/* about */
.about {
  width: 100%;
  text-align: center;
  margin-bottom: 50px;
}
.about-headline {
  text-align: center;
  font-size: 40px;
  margin-bottom: 30px;
  scroll-margin-top: 200px;
}
.about-figure {
  display: flex;
  align-items: center;
  margin: 0 auto;
}
.about-figure img {
  width: 250px;
  height: auto;
  border-radius: 50%;
  margin-left: 20%;
}
.about-figcaption {
  width: 900px;
  margin-left: 5%;
  line-height: 1.5;
  text-align: left;
  text-indent: 1em;
}

/* sns-links */
.sns-links {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 100px;
  margin-top: 50px;
}
.sns-links a {
  height: 50px;
  object-fit: cover;
  transition: all 0.2s;
}
.sns-links a:hover {
  transform: scale(1.05);
}
.sns-links a img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.API-device {
  align-items: center;
  margin-top: 10px;
}
.sns-links .github-link {
  width: 15vw;
  height: 100%;
  object-fit: cover;
  transition: all 0.2s;
}
.sns-links .github-link:hover {
  transform: scale(1.05);
}
.sns-links .github-link img {
  display: block;
  margin: 0 auto;
  width: 100%;
  height: 100%;
  object-fit: cover;
  margin-top: 30px;
  max-width: 200px;
}
.sns-links .youtube-link {
  object-fit: cover;
  transition: all 0.2s;
}
.sns-links .youtube-link:hover {
  transform: scale(1.05);
}
.sns-links .youtube-link img {
  width: 100%;
  height: 100px;
  object-fit: cover;
}
/* contact */
.contact {
  padding: 20px;
  text-align: center;
  background-color: #00b7ff55;
}
.contact-headline {
  font-size: 3em;
  margin: 20px 0;
  scroll-margin-top: 200px;
}
.contact table {
  margin: 0 auto;
  width: 80%;
  max-width: 800px;
  border-collapse: collapse;
}
.contact tr {
  border-bottom: 1px solid #ccc;
}
.contact tr th {
  text-align: center;
  padding: 10px;
  white-space: nowrap;
}
.contact tr td {
  padding: 10px;
}
.contact tr input,
.contact tr select,
.contact tr textarea {
  width: 100%;
  padding: 5px;
  border-radius: 4px;
}
.radio {
  display: flex;
  justify-content: center;
  align-items: center;
  white-space: nowrap;
  text-align: left;
}
.radio input[type="radio"] {
  margin: 0;
  width: 30px;
}
.radio label {
  margin-right: 40px;
}
.form_btn {
  cursor: pointer;
  transition: all 0.2s ease;
  outline: none;
  width: 80px !important;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem 3rem;
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  color: #fff;
  font-size: 1.5rem;
  box-shadow: 5px 5px 1px 0 rgba(0, 0, 0, 0.7);
  text-align: center;
}
.form_btn:hover {
  background-color: #0066ff;
  transform: translateY(-2px);
  box-shadow: 8px 8px 2px 0 rgba(0, 0, 0, 0.7);
}

.form_btn:active {
  transform: translateY(2px);
  box-shadow: 2px 2px 1px 0 rgba(0, 0, 0, 0.7);
  transition: all 0.1s ease;
}
.contact tr textarea {
  height: 100px;
}

/* footer */
.footer {
  text-align: center;
  width: 100%;
  border-top: #fff 1px solid;
  background-color: #000000;
}
.footer-paragraph {
  padding: 20px;
  margin: 0;
}

/* レスポンシブ */
@media screen and (max-width: 768px) {
  body {
    font-size: 16px;
  }
  /* header */
  header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    margin: 0;
    padding: 0;
    z-index: 10;
  }
  .header_wrap {
    width: 100%;
    padding: 20px;
    box-sizing: border-box;
  }
  .header_wrap h1 {
    font-size: 32px;
    outline: none;
    z-index: 100;
  }
  .header_wrap nav {
    display: none;
  }

  /* ハンバーガー */
  .hamburger {
    display: block;
    cursor: pointer;
    z-index: 100;
    position: fixed;
    top: 30px;
    right: 30px;
  }
  .hamburger div {
    width: 30px;
    height: 3px;
    background-color: #fff;
    margin: 5px 0;
    transition: all 0.3s ease;
  }
  .header_wrap nav.open {
    display: block;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: #2600ff;
    background: linear-gradient(
      90deg,
      rgba(38, 0, 255, 1) 0%,
      rgba(106, 0, 255, 1) 33%,
      rgba(38, 0, 255, 1) 50%,
      rgba(106, 0, 255, 1) 66%,
      rgba(38, 0, 255, 1) 100%
    );
    z-index: 10;
  }
  .header_wrap nav.open ul {
    display: flex;
    flex-direction: column;
    text-align: center;
    justify-content: center;
    height: 70%;
    margin-top: 120px;
  }
  .header_wrap nav.open ul li {
    margin: 30px 0;
  }
  .header_wrap nav.open ul li a {
    font-size: 20px;
    color: #fff;
    text-decoration: none;
  }
  .header_wrap .hamburger.active div:nth-child(1) {
    transform: rotate(225deg) translate(-6px, -6px);
  }
  .header_wrap .hamburger.active div:nth-child(2) {
    opacity: 0;
  }
  .header_wrap .hamburger.active div:nth-child(3) {
    transform: rotate(-225deg) translate(-5px, 5px);
  }

  /* hero */
  .hero h2 {
    font-size: 40px;
    outline: none;
  }
  .hero video {
    width: auto;
    height: 100vh;
    object-fit: cover;
  }

  /* works */
  .works-headline {
    font-size: 24px;
    margin: 20px 0;
    padding: 0;
    scroll-margin-top: 100px;
  }
  .works-items {
    grid-template-columns: repeat(1, 1fr);
  }
  .works-item {
    margin: 0;
  }
  .skill-items {
    grid-template-columns: repeat(2, 1fr);
  }
  .works-item img {
    width: 100%;
    height: 200px;
    object-fit: cover;
    transition: all 0.2s;
    margin: 0;
  }
  .works-item img:hover {
    transform: scale(1.05);
    transition: all 0.2s;
  }
  .works-item p {
    margin-top: 10px;
    color: #fff;
  }
  /* skill */
  .skill {
    width: 100%;
    text-align: center;
  }
  .skill-headline {
    font-size: 24px;
    margin: 40px 0 0 0;
    padding: 0;
    scroll-margin-top: 100px;
  }
  .skill-items {
    display: flex;
    flex-direction: column;
  }
  .skill-item {
    margin: 10px;
    display: flex;
    flex-direction: column;
  }
  .skill-p {
    font-size: 16px;
    text-align: center;
  }
  .skill-item img {
    width: 100px;
    height: auto;
    margin: 0 auto;
  }
  .html-css img {
    width: 100px;
    margin: 10px;
  }

  /* Iot */
  .Iot-headline,
  .Iot-devices-headline {
    font-size: 24px;
    margin: 20px 0;
    padding: 0;
    scroll-margin-top: 100px;
  }
  .Iot-items {
    gap: 20px;
  }
  .Iot-item img {
    width: 100%;
    height: auto;
    object-fit: cover;
    transition: all 0.2s;
    margin: 0;
  }

  .TaskFlow-code-link {
    margin-top: 10px;
  }
  .Iot-item video {
    object-fit: cover;
    transition: all 0.2s;
    margin: 0;
  }
  .Iot-devices-items {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 100px;
  }
  .Iot-item h3 {
    margin: 10px 10px 0;
    font-size: 16px;
  }
  .Iot-device-img {
    width: 100%;
    height: auto;
    object-fit: cover;
    transition: all 0.2s;
    margin: 0;
  }
  .Iot-device {
    font-size: 20px;
    color: #fff;
    margin-left: 10px;
  }
  .arduinoIDE-img {
    width: 100%;
    height: auto;
    object-fit: cover;
    transition: all 0.2s;
    margin: 0;
  }
  .Iot-devices {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 0;
  }
  .Iot-devices-items {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 0;
  }
  .Iot-device-img {
    width: 100%;
    height: 50vh;
    object-fit: cover;
    transition: all 0.2s;
    margin: 0;
  }
  .Iot-device {
    font-size: 20px;
    color: #fff;
    margin-left: 0;
    margin-top: 10px;
    margin-bottom: 50px;
  }
  .arduinoIDE-img {
    width: 100%;
    height: auto;
    object-fit: cover;
    transition: all 0.2s;
    margin: 0;
  }
  .API-img {
    width: 100%;
    height: auto;
    object-fit: cover;
    margin-top: 0;
    transition: all 0.2s;
    margin-left: 0;
  }

  /* about */
  .about-headline {
    font-size: 24px;
    margin: 50px 0 20px 0;
    padding: 0;
    scroll-margin-top: 100px;
  }
  .about-figure {
    display: flex;
    align-items: center;
    margin: 0 auto;
    flex-direction: column;
  }
  .about-figure img {
    width: 30%;
    height: auto;
    border-radius: 50%;
    margin: 0 0 20px 0;
  }
  .about-figcaption {
    width: 80%;
    margin-left: 10vw;
    line-height: 1.5;
    text-align: left;
    text-indent: 1em;
  }

  /* sns-links */
  .sns-links {
    gap: 30px;
    margin-top: 20px;
    display: block;
  }
  .sns-links a {
    height: 30px;
    margin: 0 auto;
  }
  .sns-links a img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  .sns-links a:hover {
    transform: scale(1.05);
  }
  .API-device a {
    padding: 0;
    position: absolute;
    right: 0;
    margin: 0;
  }
  .sns-links .github-link img {
    display: block;
    margin: 0 auto;
    width: 95vw;
    height: auto;
    margin: 0 auto;
  }
  .sns-links .youtube-link img {
    display: block;
    margin: 0 auto;
    width: 95vw;
    height: auto;
    margin-top: 30px;
  }
  /* contact */
  .contact-headline {
    font-size: 40px;
    margin: 20px 0;
    padding: 0;
    scroll-margin-top: 100px;
  }
  .contact table,
  .contact tr,
  .contact th,
  .contact td {
    display: block;
    width: 100%;
    box-sizing: border-box;
  }
  .contact tr {
    margin-bottom: 20px;
    border-bottom: none;
  }
  .contact tr th {
    text-align: left;
    font-size: 18px;
    padding-bottom: 0;
  }
  .contact tr td {
    padding-top: 0;
    border-bottom: #fff 1px solid;
  }

  .contact tr input,
  .contact tr select,
  .contact tr textarea {
    width: 100%;
    padding: 5px;
  }
  .contact tr textarea {
    height: 80px;
    min-height: 80px;
    resize: vertical;
  }
  .radio {
    width: 80%;
    margin-top: 10px;
    border-radius: 4px;
    font-size: 20px;
    transition: background-color 0.2s;
  }
  .form_btn {
    margin: 0 auto;
    width: 80%;
    display: block;
  }
  .radio-group label {
    margin: 0;
  }
}
</style>
