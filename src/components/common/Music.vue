<template>
  <div class="row sm-column">
    <div class="col-lg-6 col-xs-12">
      <div @click="$preview.open(0, [{
        src: `/assets/musicjacket/${data.jacketImage}_jacket.png`,
        title: data.title,
        w: 600,
        h: 600
      }], {
        fullscreenEl: true,
        zoomEl: true,
        shareEl: true,
        history: false
      })" v-lazy:background-image="`/assets/musicjacket/${data.jacketImage}_jacket.png`" class="jacket-img preview-img"></div>
      <a-player :music="{
        title: data.title,
        author: data.bandName,
        url: `/assets/sound/${data.bgmId}.mp3`,
        pic: `/assets/musicjacket/${data.jacketImage}_thumb.png`
      }" ref="player" mode="single"></a-player>
    </div>
    <div class="col-lg-6 col-xs-12">
      <h3>{{data.title}}</h3>
      <p>{{$t('composer')}}: {{data.composer}}</p>
      <p>{{$t('lyricist')}}: {{data.lyricist}}</p>
      <p>{{$t('arranger')}}: {{data.arranger}}</p>
      <p>{{$t('band')}}:
        <span v-if="Number(data.bandId) > 5">{{data.bandName}}</span>
        <img height="60px" width="100px" v-if="Number(data.bandId) <= 5" v-lazy="`/assets/band/logo/00${data.bandId}_logoL.png`">
      </p>
      <p>{{$t('combo')}}: {{data.combo}}</p>
      <p>{{$t('howtoget')}}: {{data.howToGet}}</p>
      <!-- <p>{{$t('difficulty')}}: {{getDifficulty(data.id)[0].level}} /
          {{getDifficulty(data.id)[3].level}} /
          {{getDifficulty(data.id)[2].level}} /
          {{getDifficulty(data.id)[1].level}}</p> -->
      <q-collapsible id="achievements" icon="move_to_inbox" :label="$t('achieve')">
        <div class="row">
          <div class="row items-center col-xl-6 col-12">
            <p class="col-12">Combo</p>
            <span class="row">
              <span class="col-md-3 col-sm-6 col-xs-6 column items-center">
                <img class="thumb-item" v-lazy="`/assets/thumb/common_${getRwardFileName(getAchievement('combo_easy'))}.png`">
                <p>{{getAchievement('combo_easy').quantity}}</p>
                <p>Easy</p>
              </span>
              <span class="col-md-3 col-sm-6 col-xs-6 column items-center">
                <img class="thumb-item" v-lazy="`/assets/thumb/common_${getRwardFileName(getAchievement('combo_normal'))}.png`">
                <p>{{getAchievement('combo_normal').quantity}}</p>
                <p>Normal</p>
              </span>
              <span class="col-md-3 col-sm-6 col-xs-6 column items-center">
                <img class="thumb-item" v-lazy="`/assets/thumb/common_${getRwardFileName(getAchievement('combo_hard'))}.png`">
                <p>{{getAchievement('combo_hard').quantity}}</p>
                <p>Hard</p>
              </span>
              <span class="col-md-3 col-sm-6 col-xs-6 column items-center">
                <img class="thumb-item" v-lazy="`/assets/thumb/common_${getRwardFileName(getAchievement('combo_expert'))}.png`">
                <p>{{getAchievement('combo_expert').quantity}}</p>
                <p>Expert</p>
              </span>
            </span>
          </div>
          <div class="row items-center col-xl-6 col-12">
            <p class="col-3 col-xs-12">Full combo</p>
            <span class="row">
              <span class="col-md-3 col-sm-6 col-xs-6 column items-center">
                <img class="thumb-item" v-lazy="`/assets/thumb/common_${getRwardFileName(getAchievement('full_combo_easy'))}.png`">
                <p>{{getAchievement('full_combo_easy').quantity}}</p>
                <p>Easy</p>
              </span>
              <span class="col-md-3 col-sm-6 col-xs-6 column items-center">
                <img class="thumb-item" v-lazy="`/assets/thumb/common_${getRwardFileName(getAchievement('full_combo_normal'))}.png`">
                <p>{{getAchievement('full_combo_normal').quantity}}</p>
                <p>Normal</p>
              </span>
              <span class="col-md-3 col-sm-6 col-xs-6 column items-center">
                <img class="thumb-item" v-lazy="`/assets/thumb/common_${getRwardFileName(getAchievement('full_combo_hard'))}.png`">
                <p>{{getAchievement('full_combo_hard').quantity}}</p>
                <p>Hard</p>
              </span>
              <span class="col-md-3 col-sm-6 col-xs-6 column items-center">
                <img class="thumb-item" v-lazy="`/assets/thumb/common_${getRwardFileName(getAchievement('full_combo_expert'))}.png`">
                <p>{{getAchievement('full_combo_expert').quantity}}</p>
                <p>Expert</p>
              </span>
            </span>
          </div>
          <div class="row items-center col-xl-6 col-12">
            <p class="col-3 col-xs-12">Score rank</p>
            <span class="row">
              <span class="col-md-3 col-sm-6 col-xs-6 column items-center">
                <img class="thumb-item" v-lazy="`/assets/thumb/common_${getRwardFileName(getAchievement('score_rank_c'))}.png`">
                <p>{{getAchievement('score_rank_c').quantity}}</p>
                <p>Rank C</p>
              </span>
              <span class="col-md-3 col-sm-6 col-xs-6 column items-center">
                <img class="thumb-item" v-lazy="`/assets/thumb/common_${getRwardFileName(getAchievement('score_rank_b'))}.png`">
                <p>{{getAchievement('score_rank_b').quantity}}</p>
                <p>Rank B</p>
              </span>
              <span class="col-md-3 col-sm-6 col-xs-6 column items-center">
                <img class="thumb-item" v-lazy="`/assets/thumb/common_${getRwardFileName(getAchievement('score_rank_a'))}.png`">
                <p>{{getAchievement('score_rank_a').quantity}}</p>
                <p>Rank A</p>
              </span>
              <span class="col-md-3 col-sm-6 col-xs-6 column items-center">
                <img class="thumb-item" v-lazy="`/assets/thumb/common_${getRwardFileName(getAchievement('score_rank_s'))}.png`">
                <p>{{getAchievement('score_rank_s').quantity}}</p>
                <p>Rank S</p>
              </span>
            </span>
          </div>
        </div>
      </q-collapsible>
    </div>
  </div>
</template>

<i18n>
{
  "en": {
    "composer": "Composer",
    "lyricist": "Lyricist",
    "arranger": "Arranger",
    "howtoget": "How to get",
    "difficulty": "Difficulty",
    "band": "Band",
    "achieve": "Live achievement reward",
    "combo": "Total notes"
  },
  "zh-CN": {
    "composer": "作曲",
    "lyricist": "作词",
    "arranger": "编曲",
    "howtoget": "获得方式",
    "difficulty": "难度",
    "band": "演奏者",
    "achieve": "歌曲成就",
    "combo": "音符数"
  },
  "zh-TW": {
    "composer": "作曲",
    "lyricist": "作詞",
    "arranger": "編曲",
    "howtoget": "獲得方式",
    "difficulty": "難度",
    "band": "演奏者",
    "achieve": "歌曲成就",
    "combo": "音符數"
  }
}
</i18n>

<script>
import {
  QCard,
  QCardTitle,
  QCardMedia,
  QCardMain,
  QCollapsible
} from 'quasar'
import VueAplayer from 'vue-aplayer'

export default {
  name: 'musicComponent',
  props: ['data', 'diffi', 'band'],
  components: {
    QCard,
    QCardTitle,
    QCardMedia,
    QCardMain,
    QCollapsible,
    aPlayer: VueAplayer
  },
  beforeDestroy () {
    let aplayer = this.$refs.player.control
    if (aplayer) aplayer.destroy()
  },
  methods: {
    getAchievement (name) {
      return this.data.achievements.find(elem => elem.name === name)
    },
    getRwardFileName (achievement) {
      if (achievement.rewardId) {
        const splitName = achievement.rewardType.split('_')
        splitName[1] = splitName[1].charAt(0).toUpperCase() + splitName[1].slice(1)
        return splitName.join('').concat(achievement.rewardId)
      }
      else {
        return achievement.rewardType
      }
    },
    getDifficulty (musicId) {
      return this.musicDifficultyList.filter(elem => elem.musicId === musicId)
    }
  }
}
</script>

<style lang="stylus" scoped>
.jacket-img
  width: 100%
  height: 500px
  background-size: contain
  background-repeat: no-repeat
  background-position: center

.thumb-item
  width 72px
  height 72px
</style>
