<template>
  <transition name="slide">
    <music-list :title="title" :bg-image="bgImage"></music-list>
  </transition>
</template>

<script>
import MusicList from '../../components/music-list/music-list'
import {mapGetters} from 'vuex'
import {ERR_OK} from '../../api/config'
import {getSongList} from '../../api/recommend'

export default {
  computed: {
    title () {
      return this.disc.dissname
    },
    bgImage () {
      return this.disc.imgurl
    },
    ...mapGetters([
      'disc'
    ])
  },
  created () {
    this._getSongList()
  },
  methods: {
    _getSongList () {
      getSongList(this.disc.disstid).then((res) => {
        if (res.code === ERR_OK) {
          console.log(res.cdlist[0].songlist)
        }
      })
    }
  },

  components: {
    MusicList
  }
}

</script>

<style scoped>

</style>
