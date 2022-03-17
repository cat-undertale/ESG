<!--<img src="../assets/homePage.jpg" width="1090">-->
<template>
  <div id="app">
    <b-carousel
      id="carousel-1"
      v-model="slide"
      :interval="4000"
      controls
      indicators
      background="#ababab"
      img-width="256"
      img-height="480"
      style="text-shadow: 1px 1px 2px #333;"
      @sliding-start="onSlideStart"
      @sliding-end="onSlideEnd"
    >
      <!-- Text slides with image -->
      <b-carousel-slide
        caption="什么是ESG"
        text="ESG是环境(Environmental)、社会(Social)和公司治理(Governance)的缩写，在此基础上细化各种指标体系，被公司用来规范和监督自身行为。2004年，联合国全球契约组织（UN Global Compact）发布《有心者胜》（《Who Cares Wins》）报告，首次提出ESG概念。"
        img-src="../assets/esg4.jpg"
      ></b-carousel-slide>

      <!-- Slides with custom text -->
      <b-carousel-slide img-src="../assets/esg1.jpg">
        <h1>环境（Environmental）</h1>
        <p>环境（Environmental）维度，主要关注企业生产经营中环境管理能力、环境信息披露和有关环境的负面事件；</p>
      </b-carousel-slide>

      <!-- Slides with image only -->
      <b-carousel-slide img-src="../assets/esg5.jpg">
        <h1>社会（Social）</h1>
        <p>主要通过关注企业在员工管理上合规性、包容性和多样性，员工薪酬与福利，在客户管理上是否注重保护隐私，在产品管理上是否符合相关标准和政策在公益事业上是否主动有所作为，来判断一家公司在社会责任方面是否具有积极正面的影响；</p>
      </b-carousel-slide>

      <!-- Slides with img slot -->
      <!-- Note the classes .d-block and .img-fluid to prevent browser default image alignment -->
      <b-carousel-slide img-src="../assets/esg3.jpg">
        <h1>公司治理（Governance）</h1>
        <p>主要关注包括董事会结构、股权结构、管理层薪酬及商业道德等问题，在公司治理方面是否及时进行信息披露，以及股东和管理层的利益与职责、避免腐败与财务欺诈、纳税透明、董事会构成的独立性与多样性等方面。</p>
      </b-carousel-slide>

      <!-- Slide with blank fluid image to maintain slide aspect ratio -->
      <b-carousel-slide caption="ESG理念在私募股权投资中的应用" img-src="../assets/esg2.jpg">
        <p>ESG理念在私募股权投资中的应用包括两个层面：一是投资者（LP）对私募股权基金进行配置资产时，将ESG作为考核因素。二是私募股权基金在对企业进行投资时将ESG作为投资决策的重要因素，并在企业自身管理运营和对被投企业的管理中将ESG贯穿至发展的各个方面和阶段。
        </p>
      </b-carousel-slide>
    </b-carousel>
    <br>
    <br>
    <div>
      <b-card>
        <b-media>
          <template #aside>
            <b-img src="../assets/esglogo.jpg" width="300" height="200"></b-img>
          </template>

          <h4 class="mt-0">ESG评级环节</h4>
          <div>
            <p align="left">►　首先，评级机构参照国际组织/交易所等所公布的标准/指引事先制定评级体系；</p>
            <p> </p>
            <p align="left">►　其次，通过截取企业社会责任报告的内容、通过公开渠道或者向企业发放问卷的方式采集相关信息和数据；</p>
            <p> </p>
            <p align="left">►　最后，评级机构给出评分和评级结果。</p>
          </div>
          <hr class="my-4">
          <b-media>
            <h5 class="mt-0">国际主流ESG评级体系</h5>
            <p class="mb-0">
              MSCI、富时罗素（FTSE Russell）、标普全球（S&P Global）、路孚特（Refinitiv）、汤姆森路透（Thomson Reuters）、晨星（Morningstar）
            </p>
            <small class="text-muted">
              但由于全球目前对于ESG并没有统一的标准定义，各家评级根据自身的理解对ESG提出不同的界定方法。各有特色，各具影响力。
            </small>

          </b-media>
        </b-media>
        <hr class="my-4">
      </b-card>
    </div>

    <b-jumbotron header="ESG Platform" lead="一款ESG资产估计平台">
      <p>欲了解更多信息，请访问网站</p>
      <b-button variant="primary" href="#">更多信息</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      slide: 0,
      sliding: null
    }
  },
  methods: {
    onSlideStart(slide) {
      this.sliding = true
    },
    onSlideEnd(slide) {
      this.sliding = false
    }
  }
}
</script>


<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}
</style>
